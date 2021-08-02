
<html>
    <head>
        <meta charset="utf-8"/>
        <style>
            canvas,body,html{height: 100%; width: 100%; padding: 0; margin: 0; }
        
        </style>
    </head>
    <body>
        <canvas id="renderCanvas" touch-action="none"></canvas>
        <script src="https://cdn.babylonjs.com/babylon.js"></script>
        <script src="https://cdn.babylonjs.com/babylon.max.js"></script>
        <script src="https://doc.babylonjs.com/how_to/gui"></script>
        <script src="https://code.jquery.com/pep/0.4.3/pep.js"></script>
        <script src="https://doc.babylonjs.com/api/modules/gui"></script>
        <script src="https://cdn.jsdelivr.net/npm/cannon@0.6.2/build/cannon.min.js"></script>
        <script src="https://cdn.jsdelivr.net/npm/babylonjs@3.3.0/babylon.min.js"></script>
        <script src="https://cdn.jsdelivr.net/npm/babylonjs-gui@3.3.0/babylon.gui.min.js"></script>
        <script type="text/javascript">
        const canvas = document.getElementById('renderCanvas');

        const engine = new BABYLON.Engine(canvas, true);

        const scene = new BABYLON.Scene(engine);

        const camera = new BABYLON.ArcRotateCamera('Camera', 1.2, 1.1, 60, BABYLON.Vector3.Zero(), scene);
        camera.attachControl(canvas);

        var advancedTexture = BABYLON.GUI.AdvancedDynamicTexture.CreateFullscreenUI("UI");
        var label = new BABYLON.GUI.Rectangle("label");
        label.background = "#00ffff";
        label.height = "30px";
        label.alpha = 0.5;
        label.width = "60px";
        label.cornerRadius = 25;
        label.thickness = 1;
        
        
        label.top = "5%";
        label.paddingLeft = "10px";
        label.paddingRight = "10px";
        advancedTexture.addControl(label); 
        
        
        var text = new BABYLON.GUI.TextBlock();
        text.text = "Sun";
        text.color = "black";
        text.fontSize = "20px";
        label.addControl(text); 

        
        

        
       

        




        const light = new BABYLON.HemisphericLight('light1', new BABYLON.Vector3(0,1,0), scene);
        light.intensity = 0.5;
        light.groundColor = new BABYLON.Color3(0, 0, 1);

        scene.clearColor = new BABYLON.Color3(0,0,0);


        const sunMaterial = new BABYLON.StandardMaterial('sunMaterial', scene);
        sunMaterial.emissiveTexture = new BABYLON.Texture('sun.png', scene);
        sunMaterial.diffuseColor = new BABYLON.Color3(0, 0, 0);
        sunMaterial.specularColor = new BABYLON.Color3(0, 0, 0);



        const mercuryMaterial = new BABYLON.StandardMaterial('mercuryMat', scene);
        mercuryMaterial.diffuseTexture = new BABYLON.Texture('mercury.jpg', scene);
        mercuryMaterial.specularColor = new BABYLON.Color3(0, 0, 0);

        const venusMaterial = new BABYLON.StandardMaterial('venusMat', scene);
        venusMaterial.diffuseTexture = new BABYLON.Texture('venus.jpg', scene);
        venusMaterial.specularColor = new BABYLON.Color3(0, 0, 0);

        const earthMaterial = new BABYLON.StandardMaterial('earthMat', scene);
        earthMaterial.diffuseTexture = new BABYLON.Texture('earth.jpg', scene);
        earthMaterial.specularColor = new BABYLON.Color3(0, 0, 0);

        const marsMaterial = new BABYLON.StandardMaterial('marsMat', scene);
        marsMaterial.diffuseTexture = new BABYLON.Texture('mars.jpg', scene);
        marsMaterial.specularColor = new BABYLON.Color3(0, 0, 0);

        const jupiterMaterial = new BABYLON.StandardMaterial('jupiterMat', scene);
        jupiterMaterial.diffuseTexture = new BABYLON.Texture('jupiter.jpg', scene);
        jupiterMaterial.specularColor = new BABYLON.Color3(0, 0, 0);

        const saturnMaterial = new BABYLON.StandardMaterial('saturnMat', scene);
        saturnMaterial.diffuseTexture = new BABYLON.Texture('saturn.jpg', scene);
        saturnMaterial.specularColor = new BABYLON.Color3(0, 0, 0);

        const ringMaterial = new BABYLON.StandardMaterial('ringMat', scene);
        ringMaterial.diffuseTexture = new BABYLON.Texture('ring.jpg', scene);
        ringMaterial.specularColor = new BABYLON.Color3(0, 0, 0);

        const uranusMaterial = new BABYLON.StandardMaterial('uranusMat', scene);
        uranusMaterial.diffuseTexture = new BABYLON.Texture('uranus.jpg', scene);
        uranusMaterial.specularColor = new BABYLON.Color3(0, 0, 0);

        const neptuneMaterial = new BABYLON.StandardMaterial('neptuneMat', scene);
        neptuneMaterial.diffuseTexture = new BABYLON.Texture('neptune.jpg', scene);
        neptuneMaterial.specularColor = new BABYLON.Color3(0, 0, 0);

        const moonMaterial = new BABYLON.StandardMaterial('moonMat', scene);
        moonMaterial.diffuseTexture = new BABYLON.Texture('moon.jpg', scene);
        moonMaterial.specularColor = new BABYLON.Color3(0, 0, 0);


        const sunLight = new BABYLON.PointLight('sunLight', BABYLON.Vector3.Zero(), scene);
        sunLight.intensity = 2;



        const sun = BABYLON.Mesh.CreateSphere('sun', 16, 8, scene);
        sun.material = sunMaterial;



        const mercury = BABYLON.Mesh.CreateSphere('mercury', 16, 1, scene);
        mercury.position.x = 6;
        mercury.material = mercuryMaterial;
        mercury.orbit = {
        radius: mercury.position.x,
        speed: 0.03,
        angle: 0
        };
        var points = [];
        var n = 40; 
        var r = 6; 
        for (var i = 0; i < n ; i++) {
        points.push( new BABYLON.Vector3(
        r * Math.cos(i * 2 * Math.PI / n),
        0,
        r * Math.sin(i * 2 * Math.PI / n)
        ));
        }
        points.push(points[0]); 
        var lines = BABYLON.MeshBuilder.CreateLines("lines", {points: points}, scene); //draw path of track
        points.pop(); 

        const venus = BABYLON.Mesh.CreateSphere('venus', 16, 1.5, scene);
        venus.position.x = 8.5;
        venus.material = venusMaterial;
        venus.orbit = {
        radius: venus.position.x,
        speed: 0.01,
        angle: 0
        };
        var points = [];
        var n = 4000; 
        var r = 8.5; 
        for (var i = 0; i < n ; i++) {
        points.push( new BABYLON.Vector3(
        r * Math.cos(i * 2 * Math.PI / n),
        0,
        r * Math.sin(i * 2 * Math.PI / n)
        ));
        }
        points.push(points[0]); 
        var lines = BABYLON.MeshBuilder.CreateLines("lines", {points: points}, scene); //draw path of track
        points.pop(); 

        const earth = BABYLON.Mesh.CreateSphere('earth', 16, 2.5, scene);
        earth.position.x = 12;
        earth.material = earthMaterial;
        earth.orbit = {
        radius: earth.position.x,
        speed: 0.015,
        angle: 0
        };
        var points = [];
        var n = 4000; 
        var r = 12; 
        for (var i = 0; i < n ; i++) {
        points.push( new BABYLON.Vector3(
        r * Math.cos(i * 2 * Math.PI / n),
        0,
        r * Math.sin(i * 2 * Math.PI / n)
        ));
        }
        points.push(points[0]); 
        var lines = BABYLON.MeshBuilder.CreateLines("lines", {points: points}, scene); //draw path of track
        points.pop(); 

        const moon = BABYLON.Mesh.CreateSphere('moon', 16, 0.4, scene);
        moon.parent=earth;
        moon.position.x = 1.5;
        moon.material = moonMaterial;
        moon.orbit = {
        radius: moon.position.x,
        speed: 0.03,
        angle: 0
        };

        const mars = BABYLON.Mesh.CreateSphere('mars', 16, 1, scene);
        mars.position.x = 16;
        mars.material = marsMaterial;
        mars.orbit = {
        radius: mars.position.x,
        speed: 0.017,
        angle: 0
        };
        var points = [];
        var n = 4000; 
        var r = 16; 
        for (var i = 0; i < n ; i++) {
        points.push( new BABYLON.Vector3(
        r * Math.cos(i * 2 * Math.PI / n),
        0,
        r * Math.sin(i * 2 * Math.PI / n)
        ));
        }
        points.push(points[0]); 
        var lines = BABYLON.MeshBuilder.CreateLines("lines", {points: points}, scene); //draw path of track
        points.pop(); 

        const jupiter = BABYLON.Mesh.CreateSphere('jupiter', 16, 4, scene);
        jupiter.position.x = 21;
        jupiter.material = jupiterMaterial;
        jupiter.orbit = {
        radius: jupiter.position.x,
        speed: 0.005,
        angle: 0
        };
        var points = [];
        var n = 4000; 
        var r = 21; 
        for (var i = 0; i < n ; i++) {
        points.push( new BABYLON.Vector3(
        r * Math.cos(i * 2 * Math.PI / n),
        0,
        r * Math.sin(i * 2 * Math.PI / n)
        ));
        }
        points.push(points[0]); 
        var lines = BABYLON.MeshBuilder.CreateLines("lines", {points: points}, scene); //draw path of track
        points.pop(); 

        const saturn = BABYLON.Mesh.CreateSphere('saturn', 14, 4, scene);
        saturn.position.x = 28;
        saturn.material = saturnMaterial;
        saturn.orbit = {
        radius: saturn.position.x,
        speed: 0.002,
        angle: 0
        };
        var points = [];
        var n = 4000; 
        var r = 28; 
        for (var i = 0; i < n ; i++) {
        points.push( new BABYLON.Vector3(
        r * Math.cos(i * 2 * Math.PI / n),
        0,
        r * Math.sin(i * 2 * Math.PI / n)
        ));
        }
        points.push(points[0]); 
        var lines = BABYLON.MeshBuilder.CreateLines("lines", {points: points}, scene); //draw path of track
        points.pop(); 

        
        const ring = BABYLON.MeshBuilder.CreateTorus("ring", {thickness: 0.3, diameter: 5}, scene);
        ring.parent= saturn;
        ring.material = ringMaterial;


        const uranus = BABYLON.Mesh.CreateSphere('uranus', 17, 4, scene);
        uranus.position.x = 32;
        uranus.material = uranusMaterial;
        uranus.orbit = {
        radius: uranus.position.x,
        speed: 0.011,
        angle: 0
        };
        var points = [];
        var n = 4000; 
        var r = 32; 
        for (var i = 0; i < n ; i++) {
        points.push( new BABYLON.Vector3(
        r * Math.cos(i * 2 * Math.PI / n),
        0,
        r * Math.sin(i * 2 * Math.PI / n)
        ));
        }
        points.push(points[0]); 
        var lines = BABYLON.MeshBuilder.CreateLines("lines", {points: points}, scene); //draw path of track
        points.pop(); 

        const neptune = BABYLON.Mesh.CreateSphere('neptune', 16, 4, scene);
        neptune.position.x = 36;
        neptune.material = neptuneMaterial;
        neptune.orbit = {
        radius: neptune.position.x,
        speed: 0.009,
        angle: 0
        };
        var points = [];
        var n = 4000; 
        var r = 36; 
        for (var i = 0; i < n ; i++) {
        points.push( new BABYLON.Vector3(
        r * Math.cos(i * 2 * Math.PI / n),
        0,
        r * Math.sin(i * 2 * Math.PI / n)
        ));
        }
        points.push(points[0]); 
        var lines = BABYLON.MeshBuilder.CreateLines("lines", {points: points}, scene); //draw path of track
        points.pop(); 

        const pluto = BABYLON.Mesh.CreateSphere('pluto', 16, 0.5, scene);
        pluto.position.x = 40;
        pluto.material = mercuryMaterial;
        pluto.orbit = {
        radius: pluto.position.x,
        speed: 0.007,
        angle: 0
        };
        var points = [];
        var n = 4000; 
        var r = 40; 
        for (var i = 0; i < n ; i++) {
        points.push( new BABYLON.Vector3(
        r * Math.cos(i * 2 * Math.PI / n),
        0,
        r * Math.sin(i * 2 * Math.PI / n)
        ));
        }
        points.push(points[0]); 
        var lines = BABYLON.MeshBuilder.CreateLines("lines", {points: points}, scene); //draw path of track
        points.pop(); 

        const skybox = BABYLON.Mesh.CreateBox('skybox', 1000, scene);
        const skyboxMaterial = new BABYLON.StandardMaterial('skyboxMat', scene);

        skyboxMaterial.backFaceCulling = false;

        skybox.infiniteDistance = true;

        skybox.material = skyboxMaterial;

        skyboxMaterial.diffuseColor = new BABYLON.Color3(0, 0, 0);
        skyboxMaterial.specularColor = new BABYLON.Color3(0, 0, 0);

        skyboxMaterial.reflectionTexture = new BABYLON.CubeTexture('skybox.jpg', scene);
        skyboxMaterial.reflectionTexture.coordinatesMode = BABYLON.Texture.SKYBOX_MODE;

        

        scene.beforeRender = function() {

        sun.rotation.y = sun.rotation.y + 0.01;

        mercury.position.x = mercury.orbit.radius * Math.sin(mercury.orbit.angle);
        mercury.position.z = mercury.orbit.radius * Math.cos(mercury.orbit.angle);
        mercury.orbit.angle = mercury.orbit.speed + mercury.orbit.angle;
        mercury.rotation.y = mercury.rotation.y + 0.05;

        venus.position.x = venus.orbit.radius * Math.sin(venus.orbit.angle);
        venus.position.z = venus.orbit.radius * Math.cos(venus.orbit.angle);
        venus.orbit.angle += venus.orbit.speed;
        venus.rotation.y = venus.rotation.y + 0.05;

        earth.position.x = earth.orbit.radius * Math.sin(earth.orbit.angle);
        earth.position.z = earth.orbit.radius * Math.cos(earth.orbit.angle);
        earth.orbit.angle += earth.orbit.speed;
        earth.rotation.y =earth.rotation.y + 0.05;

        moon.position.x = moon.orbit.radius * Math.sin(moon.orbit.angle);
        moon.position.z = moon.orbit.radius * Math.cos(moon.orbit.angle);
        moon.position.y = moon.orbit.radius * Math.cos(moon.orbit.angle);
        moon.orbit.angle = moon.orbit.speed + moon.orbit.angle;
        moon.rotation.y = moon.rotation.y + 0.05;

        mars.position.x = mars.orbit.radius * Math.sin(mars.orbit.angle);
        mars.position.z = mars.orbit.radius * Math.cos(mars.orbit.angle);
        mars.orbit.angle += mars.orbit.speed;
        mars.rotation.y = mars.rotation.y + 0.05;


        jupiter.position.x = jupiter.orbit.radius * Math.sin(jupiter.orbit.angle);
        jupiter.position.z = jupiter.orbit.radius * Math.cos(jupiter.orbit.angle);
        jupiter.orbit.angle += jupiter.orbit.speed;
        jupiter.rotation.y = jupiter.rotation.y + 0.05;

        saturn.position.x = saturn.orbit.radius * Math.sin(saturn.orbit.angle);
        saturn.position.z = saturn.orbit.radius * Math.cos(saturn.orbit.angle);
        saturn.orbit.angle += saturn.orbit.speed;
        saturn.rotation.y = saturn.rotation.y + 0.05;
        
        


        uranus.position.x = uranus.orbit.radius * Math.sin(uranus.orbit.angle);
        uranus.position.z = uranus.orbit.radius * Math.cos(uranus.orbit.angle);
        uranus.orbit.angle += uranus.orbit.speed;
        uranus.rotation.y = uranus.rotation.y + 0.05;

        neptune.position.x = neptune.orbit.radius * Math.sin(neptune.orbit.angle);
        neptune.position.z = neptune.orbit.radius * Math.cos(neptune.orbit.angle);
        neptune.orbit.angle += neptune.orbit.speed;
        neptune.rotation.y = neptune.rotation.y + 0.05;

        pluto.position.x = pluto.orbit.radius * Math.sin(pluto.orbit.angle);
        pluto.position.z = pluto.orbit.radius * Math.cos(pluto.orbit.angle);
        pluto.orbit.angle += pluto.orbit.speed;
        pluto.rotation.y = pluto.rotation.y + 0.05;
        };

        engine.runRenderLoop(function () {
        scene.render();
        });

        window.addEventListener('resize', function(){
        engine.resize();
        });

        </script>


    </body>
</html>
