<template>
  <div id="home"></div>
</template>

<script>
import * as THREE from "three";
import Stats from "three/examples/jsm/libs/stats.module.js";
import gsap from "gsap";
import fragmentShader from "raw-loader!glslify-loader!@/assets/glsl/fragmentShader.glsl";
import vertexShader from "raw-loader!glslify-loader!@/assets/glsl/vertexShader.glsl";

export default {
  data() {
    return {
      animReq: null,
    };
  },
  mounted() {
    //* INIT VARIABLES
    let container;
    let renderer;
    let transition;
    let stats;
    let mouse;

    //* Init THREE Clock
    const clock = new THREE.Clock();

    /**
     ** init
     *? init function for initialize THREE basics
     */
    const init = () => {
      //! Init GUI
      //initGUI();

      mouse = new THREE.Vector2(0, 0);
      window.addEventListener("mousemove", (ev) => {
        onMouseMove(ev);
      });

      function onMouseMove(event) {
        // mouse.x = event.clientX / window.innerWidth;
        // mouse.y = event.clientY / window.innerHeight;
        gsap.to(mouse, {
            duration: 0.5,
            x: (event.clientX / window.innerWidth) * 2 - 1,
            y: -(event.clientY / window.innerHeight)* - 2
        })
      }

      //* Init Container
      container = document.getElementById("home");

      //* Init Renderer
      renderer = new THREE.WebGLRenderer({ antialias: true });
      renderer.setPixelRatio(window.devicePixelRatio);
      renderer.setSize(window.innerWidth, window.innerHeight);
      container.appendChild(renderer.domElement);

      //* Init stats
      stats = new Stats();
      container.appendChild(stats.dom);

      //* Init Scenes
      const sceneA = new FXScene(3, 120, 0xffffff, true);
      const sceneB = new FXScene(3, 120, 0xffffff, false);

      //* init Transition
      transition = new Transition(sceneA, sceneB);
    };

    /**
     ** animate
     *? animate function for render loop
     */
    const animate = () => {
      this.animReq = requestAnimationFrame(animate);
      render();
      stats.update();
      console.log("animating scene");
    };

    /**
     ** render
     *? ---------------
     */
    const render = () => {
      transition.render(clock.getDelta());
    };

    /**
     ** FXScene
     *? create scene with camera and box mesh
     * @param cameraZ camera position in Z axis
     * @param fov camera field of view
     * @param clearColor color for setClearColor renderer
     */
    function FXScene(cameraZ, fov, clearColor, sceneID) {
      this.clearColor = clearColor;

      //* Init scene Camera
      this.camera = new THREE.PerspectiveCamera(
        fov,
        window.innerWidth / window.innerHeight,
        1,
        10000
      );
      this.camera.position.z = cameraZ;

      //* Setup Scene
      this.scene = new THREE.Scene();

      //* Init AmbientLight
      this.scene.add(new THREE.AmbientLight(0x555555));

      //* Init Light
      const light = new THREE.SpotLight(0xffffff, 1.5);
      light.position.set(0, 500, 2000);
      this.scene.add(light);

      //* Init Box mesh
      const defaultMaterial = new THREE.MeshPhongMaterial({
        color: sceneID ? 0xff00ff : 0xcccccc,
        flatShading: true,
        vertexColors: true,
      });
      this.mesh = new THREE.Mesh(new THREE.TorusGeometry(), defaultMaterial);
      this.scene.add(this.mesh);

      const renderTargetParameters = {
        minFilter: THREE.LinearFilter,
        magFilter: THREE.LinearFilter,
        format: THREE.RGBFormat,
      };
      this.fbo = new THREE.WebGLRenderTarget(
        window.innerWidth,
        window.innerHeight,
        renderTargetParameters
      );

      this.render = (delta, rtt) => {
        renderer.setClearColor(this.clearColor);
        this.mesh.rotation.x += 0.01;
        if (rtt) {
          renderer.setRenderTarget(this.fbo);
          renderer.clear();
          renderer.render(this.scene, this.camera);
        } else {
          renderer.setRenderTarget(null);
          renderer.render(this.scene, this.camera);
        }
      };
    }

    function Transition(sceneA, sceneB) {
      this.scene = new THREE.Scene();
      this.cameraOrtho = new THREE.OrthographicCamera(
        window.innerWidth / -2,
        window.innerWidth / 2,
        window.innerHeight / 2,
        window.innerHeight / -2,
        -10,
        10
      );

      this.quadmaterial = new THREE.ShaderMaterial({
        uniforms: {
          //   u_resolution: {
          //     value: {
          //       x: window.innerWidth,
          //       y: window.innerHeight,
          //     },
          //   },
          //   u_mouse: {
          //     value: {
          //       x: 0.5,
          //       y: 0.5,
          //     },
          //   },
          //   tDiffuse1: {
          //     value: null,
          //   },
          //   tDiffuse2: {
          //     value: null,
          //   },
          //   mixRatio: {
          //     value: 0.0,
          //   },
          //   threshold: {
          //     value: 0.1,
          //   },
          u_image: { type: "t", value: null },
          u_imagehover: { type: "t", value: null },
          u_time: { value: 0 },
          u_mouse: {
            value: {
              x: 0.5,
              y: 0.5,
            },
          },
          u_res: {
            value: new THREE.Vector2(window.innerWidth, window.innerHeight),
          },
        },
        vertexShader: vertexShader,
        // [
        //   "varying vec2 vUv;",

        //   "void main() {",

        //   "vUv = vec2( uv.x, uv.y );",
        //   "gl_Position = projectionMatrix * modelViewMatrix * vec4( position, 1.0 );",

        //   "}",
        // ].join("\n"),
        fragmentShader: fragmentShader,
        // [
        //   "#pragma glslify: snoise2 = require('glsl-noise/simplex/2d')",
        //   "uniform vec2 u_resolution;",
        //   "uniform vec2 u_mouse;",
        //   "uniform float mixRatio;",

        //   "uniform sampler2D tDiffuse1;",
        //   "uniform sampler2D tDiffuse2;",

        //   "uniform float threshold;",

        //   "varying vec2 vUv;",

        //   "float circle(in vec2 _st, in float _radius, in float blurriness){",
        //   "vec2 dist = _st;",
        //   "return 1.-smoothstep(_radius-(_radius*blurriness), _radius+(_radius*blurriness), dot(dist,dist)*4.0);",
        //   "}",

        //   "void main() {",

        //   "	vec4 texel1 = texture2D( tDiffuse1, vUv );",
        //   "	vec4 texel2 = texture2D( tDiffuse2, vUv );",
        //   " //vec2 res = u_resolution * PR;",
        //   " vec2 st = gl_FragCoord.xy/u_resolution.xy;",
        //   " st.y *= u_resolution.y / u_resolution.x;",

        //   " vec2 mouse = u_mouse * - 1.;",
        //   " float r = 0.05;",

        //   " mouse.y *= u_resolution.y / u_resolution.x;",
        //   " //mouse *= -.5;",
        //   " vec2 circlePos = st + mouse;",

        //   " float color = circle(circlePos,r,1.);",

        //   " float n = snoise2(vec2(v_uv.x, v_uv.y));",
        //   " gl_FragColor = vec4(vec3(n), 1.);",

        //   " //gl_FragColor = mix( texel2, texel1, color);",

        //   "}",
        // ].join("\n"),
        defines: {
          PR: window.devicePixelRatio.toFixed(1),
        },
      });

      const quadgeometry = new THREE.PlaneBufferGeometry(
        window.innerWidth,
        window.innerHeight
      );
      this.quad = new THREE.Mesh(quadgeometry, this.quadmaterial);
      this.scene.add(this.quad);

      //* Link both scenes and their FBOs
      this.sceneA = sceneA;
      this.sceneB = sceneB;
      console.log("sceneA: ", this.sceneA);
      //   this.quadmaterial.uniforms.tDiffuse1.value = this.sceneA.fbo.texture;
      //   this.quadmaterial.uniforms.tDiffuse2.value = this.sceneB.fbo.texture;
      this.quadmaterial.uniforms.u_imagehover.value = this.sceneA.fbo.texture;
      this.quadmaterial.uniforms.u_image.value = this.sceneB.fbo.texture;

      this.needChange = false;

      this.render = (delta) => {
        // this.quadmaterial.uniforms.mixRatio.value = 0.5;
        this.quadmaterial.uniforms.u_mouse.value.x = mouse.x;
        this.quadmaterial.uniforms.u_mouse.value.y =
          ((mouse.y - 0) * (0 - 1)) / (1 - 0) + 1;
        this.quadmaterial.uniforms.u_time.value += 0.001;

        // // Prevent render both scenes when it's not necessary
        // if (this.quadmaterial.uniforms.mixRatio.value == 0) {
        //   this.sceneB.render(delta, false);
        // } else if (this.quadmaterial.uniforms.mixRatio.value == 1) {
        //   this.sceneA.render(delta, false);
        // } else {
        //   // When 0<transition<1 render transition between two scenes

        //   this.sceneA.render(delta, true);
        //   this.sceneB.render(delta, true);
        //   renderer.setRenderTarget(null);
        //   renderer.clear();
        //   renderer.render(this.scene, this.cameraOrtho);
        // }
        this.sceneA.render(delta, true);
        this.sceneB.render(delta, true);
        renderer.setRenderTarget(null);
        renderer.clear();
        renderer.render(this.scene, this.cameraOrtho);
      };
    }

    //* call main functions for THREE behavior
    init();
    animate();
  },
  unmounted() {
    cancelAnimationFrame(this.animReq);
  },
};
</script>

<style lang="scss" scoped>
#home {
  position: fixed;
  width: 100%;
  height: 100%;
}
</style>