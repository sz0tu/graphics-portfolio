<template>
    <div class="blob">
        <canvas></canvas>
    </div>

</template>

<script>

    //https://threejs.org/examples/#webgl_lightprobe
    //https://threejs.org/examples/#webgl_materials
    //https://threejs.org/examples/#webgl_materials_channels
    var yellow = 0xffed18;
    var coral = 0xFF8066;
    var red = 0xff4533;
    var orange = 0xff8833;
    var cyan = 0x18ffed;
    var green = 0x33ff45;
    var magenta = 0xed18ff;
    var blue = 0x189eff;
    var dark_blue = 0x4533ff;

    $(document).ready(function() {
        let $canvas = $('.blob canvas'),
            canvas = $canvas[0],
            renderer = new THREE.WebGLRenderer({
                canvas: canvas,
                context: canvas.getContext('webgl2'),
                antialias: true,
                alpha: true
            }),
            simplex = new SimplexNoise();

        renderer.setSize(500, 500);
        renderer.setPixelRatio(window.devicePixelRatio || 1);

        let scene = new THREE.Scene();
        camera = new THREE.PerspectiveCamera(45, $canvas.width() / $canvas.height(), 0.1, 1000);
        camera.position.z = 5;

        let geometry = new THREE.SphereGeometry(.8, 128, 128);
        let material = new THREE.MeshPhongMaterial({
            color: blue,
            shininess: 100,
        });

        let lightTop = new THREE.DirectionalLight(0xFFFFFF, .7);
        lightTop.position.set(0, 500, 200);
        lightTop.castShadow = true;
        scene.add(lightTop);

        let lightBottom = new THREE.DirectionalLight(dark_blue, .25);
        lightBottom.position.set(0, -500, 400);
        lightBottom.castShadow = true;
        scene.add(lightBottom);

        let ambientLight = new THREE.AmbientLight(0x798296);
        scene.add(ambientLight);

        let sphere = new THREE.Mesh(geometry, material);

        scene.add(sphere);

        var pointLight = new THREE.PointLight( magenta, 0.5 );
        pointLight.position.z = 2500;
        scene.add( pointLight );

        var pointLight2 = new THREE.PointLight( magenta, 1 );
        camera.add( pointLight2 );

        var pointLight3 = new THREE.PointLight( magenta, 0.5 );
        pointLight3.position.x = - 1000;
        pointLight3.position.z = 1000;
        scene.add( pointLight3 );

        var pointLight4 = new THREE.PointLight( magenta, 1);
        pointLight4.position.x = - 500;
        pointLight4.position.z = 500;
        scene.add( pointLight4 );

        var pointLight5 = new THREE.PointLight( magenta, 1);
        pointLight5.position.x = 500;
        pointLight5.position.z = 500;
        scene.add( pointLight5 );

        var spotLight = new THREE.SpotLight( magenta );
        spotLight.position.set( 100, 1000, 100 );
        spotLight.castShadow = true;
        spotLight.shadow.mapSize.width = 1024;
        spotLight.shadow.mapSize.height = 1024;
        spotLight.shadow.camera.near = 500;
        spotLight.shadow.camera.far = 4000;
        spotLight.shadow.camera.fov = 30;
        scene.add( spotLight );

        let wiggle = () => {
            let time = performance.now() * 0.00001 * 13 * Math.pow(1.3, 3);
            for(let i = 0; i < sphere.geometry.vertices.length; i++) {
                let p = sphere.geometry.vertices[i];
                p.normalize().multiplyScalar(
                    1 + 0.3 * simplex.noise3D(p.x * 0.975, p.y * 0.975, p.z * 0.975 + time));
            }

            sphere.geometry.computeVertexNormals();
            sphere.geometry.normalsNeedUpdate = true;
            sphere.geometry.verticesNeedUpdate = true;
        }

        function animate() {
            wiggle();
            renderer.render(scene, camera);
            requestAnimationFrame(animate);
        }
        requestAnimationFrame(animate);
    });

    export default {
        name: "Bloom"
    }
</script>

<style scoped>
    .blob {
        overflow: hidden;
        position: absolute;
        width: 500px;
        justify-content: center;
        align-items: center;
    }

    html, body {
        overflow: hidden;
    }

    body {
        min-height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        background: #FFFFFF;
    }

</style>