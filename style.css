<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Juego 3D en PlayCanvas</title>
    <!-- Importamos el motor 3D de PlayCanvas -->
    <script src="https://code.playcanvas.com/playcanvas-stable.min.js"></script>
    <style>
        body { margin: 0; padding: 0; overflow: hidden; background-color: #000; }
        canvas { display: block; width: 100vw; height: 100vh; }
        #interfaz {
            position: absolute;
            top: 20px;
            left: 20px;
            color: white;
            font-family: system-ui, sans-serif;
            background: rgba(0, 0, 0, 0.7);
            padding: 15px;
            border-radius: 8px;
            border: 1px solid #56f5d2;
        }
    </style>
</head>
<body>

    <div id="interfaz">
        <strong>Explorador 3D</strong><br>
        <span style="font-size: 14px; color: #a2aec9;">Usa las flechas o WASD para moverte</span>
    </div>

    <!-- El lienzo donde el motor renderizará el mundo 3D -->
    <canvas id="mundo3D"></canvas>

    <script>
        // 1. INICIALIZAR EL MOTOR PLAYCANVAS Y EL TECLADO
        const canvas = document.getElementById('mundo3D');
        const app = new pc.Application(canvas, {
            keyboard: new pc.Keyboard(window) // Habilitamos la lectura del teclado
        });
        app.start();
        app.setCanvasFillMode(pc.FILLMODE_FILL_WINDOW);
        app.setCanvasResolution(pc.RESOLUTION_AUTO);
        window.addEventListener('resize', () => app.resizeCanvas());

        // 2. CREAR LA CÁMARA (Nuestra vista del mundo)
        const camara = new pc.Entity();
        camara.addComponent('camera', {
            clearColor: new pc.Color(0.1, 0.15, 0.2) // Color del "cielo"
        });
        camara.setPosition(0, 6, 10); // La subimos (Y) y la alejamos (Z)
        camara.lookAt(0, 0, 0); // Hacemos que mire hacia el centro del mundo
        app.root.addChild(camara);

        // 3. CREAR LA LUZ (Para que haya sombras y volumen)
        const luz = new pc.Entity();
        luz.addComponent('light', {
            type: 'directional',
            color: new pc.Color(1, 1, 1)
        });
        luz.setEulerAngles(45, 30, 0); // Inclinación del "sol"
        app.root.addChild(luz);

        // 4. CREAR EL SUELO (Plano 3D verde)
        const suelo = new pc.Entity();
        suelo.addComponent('render', { type: 'plane' });
        suelo.setLocalScale(15, 1, 15); // Hacemos el plano grande
        
        // Pintar el suelo
        const materialSuelo = new pc.StandardMaterial();
        materialSuelo.diffuse.set(0.2, 0.8, 0.3); // Verde
        materialSuelo.update();
        suelo.render.material = materialSuelo;
        app.root.addChild(suelo);

        // 5. CREAR EL JUGADOR (Cubo 3D rojo)
        const jugador = new pc.Entity();
        jugador.addComponent('render', { type: 'box' });
        jugador.setPosition(0, 0.5, 0); // Lo subimos medio metro para que no atraviese el suelo
        
        // Pintar el jugador
        const materialJugador = new pc.StandardMaterial();
        materialJugador.diffuse.set(0.9, 0.2, 0.2); // Rojo
        materialJugador.update();
        jugador.render.material = materialJugador;
        app.root.addChild(jugador);

        // 6. LÓGICA DE MOVIMIENTO 3D (Bucle del juego)
        app.on('update', function (dt) {
            let velocidad = 5 * dt; // dt = delta time (tiempo entre fotogramas)
            let x = 0; // Movimiento lateral
            let z = 0; // Movimiento de profundidad

            // Detectar teclas
            if (app.keyboard.isPressed(pc.KEY_LEFT) || app.keyboard.isPressed(pc.KEY_A)) x -= velocidad;
            if (app.keyboard.isPressed(pc.KEY_RIGHT) || app.keyboard.isPressed(pc.KEY_D)) x += velocidad;
            if (app.keyboard.isPressed(pc.KEY_UP) || app.keyboard.isPressed(pc.KEY_W)) z -= velocidad;
            if (app.keyboard.isPressed(pc.KEY_DOWN) || app.keyboard.isPressed(pc.KEY_S)) z += velocidad;

            // Mover el objeto en los 3 ejes (X, Y, Z). Dejamos la Y en 0 para no volar.
            jugador.translate(x, 0, z);

            // Efecto extra: Hacer que el cubo gire levemente al moverse para que se vea dinámico
            if (x !== 0 || z !== 0) {
                jugador.rotate(0, x * 20, z * 20);
            }
        });
    </script>
</body>
</html>