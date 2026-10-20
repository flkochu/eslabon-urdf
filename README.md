# Eslabón URDF

Arma el URDF de tu robot para **ROS 2** sin escribir XML. Sube los STL de tus piezas, únelas por el centro de sus agujeros como en un ensamble de Fusion 360 o SolidWorks, elige el grado de libertad de cada unión y descarga un paquete ROS 2 listo para RViz.

**Úsalo aquí → https://flkochu.github.io/eslabon-urdf/**

## Qué hace

- Importa STL (mm, cm, m o pulgadas) y detecta solo el centro y el eje de agujeros, flechas y bordes circulares.
- Une piezas en dos clics. *Encajar piezas* las acomoda como un joint de Fusion; *Ya están en posición* respeta las coordenadas de tu ensamble.
- Seis grados de libertad por unión (girar o deslizar en X, Y o Z), unión fija o giro continuo, con vista previa animada antes de elegir.
- Materiales (PLA, PETG, aluminio, acero, latón…) con relleno de impresión: calcula masa, centro de masa e inercia de cada malla.
- Límites, actuadores comunes (SG90, MG996R, DS3218, Dynamixel, NEMA 17/23), pose home y elección de la pieza base.
- Jerarquía del robot en árbol y vista tipo `check_urdf`.
- Exporta un paquete ROS 2 completo: URDF, mallas, `display.launch.py` con RViz y sliders, `initial_positions.yaml`, SRDF para MoveIt y README.

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
