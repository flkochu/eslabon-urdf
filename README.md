# Eslabón URDF

Arma el URDF de tu robot para **ROS 2** sin escribir XML. Sube los STL de tus piezas, únelas por el centro de sus agujeros como en un ensamble de Fusion 360 o SolidWorks, elige el grado de libertad de cada unión y descarga un paquete ROS 2 listo para RViz. El mismo robot sale también para **Blender** (`.glb`) y **MuJoCo** (MJCF), y de cada pieza puedes sacar su **hoja de despiece**.

**Úsalo aquí → https://flkochu.github.io/eslabon-urdf/**

## Qué hace

- Importa STL (mm, cm, m o pulgadas) y detecta solo el centro y el eje de agujeros, flechas y bordes circulares.
- Une piezas en dos clics. *Encajar piezas* las acomoda como un joint de Fusion; *Ya están en posición* respeta las coordenadas de tu ensamble.
- Fusiona componentes fijos (servos, tapas, soportes, tornillería) con la pieza a la que van pegados: en el URDF quedan como un solo link con varios visuales y una masa e inercia combinadas.
- Seis grados de libertad por unión (girar o deslizar en X, Y o Z), unión fija o giro continuo, con vista previa animada antes de elegir.
- Materiales (PLA, PETG, aluminio, acero, latón…) con relleno de impresión: calcula masa, centro de masa e inercia de cada malla.
- Límites, actuadores comunes (SG90, MG996R, DS3218, Dynamixel, NEMA 17/23), pose home y elección de la pieza base.
- Jerarquía del robot en árbol y vista tipo `check_urdf`.
- Exporta un paquete ROS 2 completo: URDF, mallas, `display.launch.py` con RViz y sliders, `initial_positions.yaml`, SRDF para MoveIt y README.
- Exporta a **Blender** (`.glb`, glTF 2.0): cada link es un objeto que gira sobre su unión con los mismos ejes del URDF, con sus límites como propiedades y una animación que prueba cada articulación. Desde Blender puedes sacar FBX.
- Exporta a **MuJoCo** (MJCF): mismo árbol, masas e inercias, un actuador con slider por articulación y la pose home.
- **Hoja de despiece** de cualquier pieza: vistas frontal, superior y lateral (sistema europeo o americano) con líneas ocultas, isométrico, cotas generales, radios y tabla de agujeros y cilindros. Sale en PDF o SVG para imprimir a escala, y en DXF 1:1 con una capa por vista para redibujarla en Fusion 360 o SolidWorks.

## Cómo se usa

1. Sube tus STL con el botón o arrastrándolos al visor.
2. Presiona **J**: clic en el agujero de la pieza que se mueve y luego en el de la pieza fija.
3. Elige el grado de libertad y pruébalo con el slider.
4. Asigna material, límites y home.
5. **Generar URDF** → descarga el `.zip` y en tu workspace:

```bash
cd ~/ros2_ws/src && unzip ~/Descargas/mi_robot_description.zip
cd ~/ros2_ws && colcon build --packages-select mi_robot_description
source install/setup.bash
ros2 launch mi_robot_description display.launch.py
```

## Otros formatos

**Blender.** En *Generar URDF › Otros formatos › Blender (.glb)*. En Blender: *Archivo › Importar › glTF 2.0*. Cada link es un Empty: selecciónalo y gíralo sobre su eje local (por ejemplo `R Z Z`) para mover la unión; sus límites están en *Propiedades del objeto › Propiedades personalizadas*. Dale Play para ver la animación de prueba. Para FBX: *Archivo › Exportar › FBX*.

**MuJoCo.** En *Generar URDF › Otros formatos › MuJoCo (.zip)*:

```bash
pip install mujoco
python -m mujoco.viewer --mjcf=mi_robot.xml
```

**Hoja de despiece.** Selecciona una pieza y, en el inspector, *Plano de la pieza › Hoja de despiece*. Para rehacerla en Fusion 360: *Insertar › Insertar DXF*, elige un plano, unidades mm y "Un boceto por capa"; cada vista llega como boceto con los agujeros como círculos exactos y los redondeos como arcos. Las medidas salen de la malla STL: verifica las críticas con calibrador.

## Privacidad

Todo corre en tu navegador. Tus STL no se suben a ningún servidor: el proyecto se guarda solo en tu navegador o en el `.json` que tú descargues.

## Reportar errores o ideas

Usa el botón **Reportar** dentro de la página: arma el reporte con los datos técnicos (navegador, número de piezas, errores recientes) y lo abre aquí como issue o en tu correo. También puedes [abrir un issue](https://github.com/flkochu/eslabon-urdf/issues/new) directamente.

## Desarrollo

Es un solo `index.html` que carga [three.js](https://threejs.org) desde CDN; no necesita compilación. Para probarlo en tu computadora:

```bash
python3 -m http.server 8000   # y abre http://localhost:8000
```

## Licencia

MIT © 2026 Adán López Lozano
