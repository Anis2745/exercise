# exercise

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport"
        content="width=device-width, initial-scale=1.0">
  <title>3D Pyramid</title>
  <style>
    body {
      margin: 0;
      overflow: hidden;
      background: #f0f0f0;
    }
  </style>
</head>
<body>

<script type="module">
  import * as THREE from
  "https://esm.sh/three@0.160.0";

  import { OrbitControls } from
  "https://esm.sh/three@0.160.0/examples/jsm/controls/OrbitControls.js";

  const scene = new THREE.Scene();
  scene.background = new THREE.Color(0xf0f0f0);

  const camera = new THREE.PerspectiveCamera(
    75,
    window.innerWidth / window.innerHeight,
    0.1,
    1000
  );

  camera.position.set(4, 3, 5);

  const renderer = new THREE.WebGLRenderer({
    antialias: true
  });

  renderer.setSize(
    window.innerWidth,
    window.innerHeight
  );

  document.body.appendChild(renderer.domElement);

  // Create pyramid
  const geometry = new THREE.ConeGeometry(
    2, 3, 4
  );

  const material = new THREE.MeshStandardMaterial({
    color: 0x9b59b6,
    flatShading: true
  });

  const pyramid = new THREE.Mesh(
    geometry,
    material
  );

  pyramid.rotation.y = Math.PI / 4;
  scene.add(pyramid);

  // Lighting
  const light = new THREE.DirectionalLight(
    0xffffff, 3
  );

  light.position.set(5, 5, 5);
  scene.add(light);

  scene.add(
    new THREE.AmbientLight(0xffffff, 1)
  );

  // Rotate with mouse or finger
  const controls = new OrbitControls(
    camera,
    renderer.domElement
  );

  controls.enableDamping = true;

  function animate() {
    requestAnimationFrame(animate);
    controls.update();
    renderer.render(scene, camera);
  }

  animate();

  window.addEventListener("resize", () => {
    camera.aspect =
      window.innerWidth / window.innerHeight;

    camera.updateProjectionMatrix();

    renderer.setSize(
      window.innerWidth,
      window.innerHeight
    );
  });
</script>

</body>
</html>
