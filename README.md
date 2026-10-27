# ZAPEL 3D

Programa web para el análisis de **pórticos espaciales (3D)** por el **método de los elementos finitos**, con soporte de **fundación elástica tipo Winkler**. Se dibuja la estructura sobre planos de trabajo, se asignan apoyos, cargas y propiedades, y se obtienen deformada, reacciones y diagramas de esfuerzos, con una forma de trabajo parecida a la de Robot Structural Analysis.

Es la versión tridimensional de **ZAPEL Frame (2D)** y una actualización gráfica del programa Fortran **ZAPEL77P** (vigas sobre fundación elástica).

> Es un único archivo HTML autocontenido: no requiere instalación, servidor, base de datos ni conexión a internet para funcionar.

## Instalación

### Opción A: publicarlo como página web con GitHub Pages

1. Crea una cuenta en [github.com](https://github.com) si aún no tienes una.
2. Pulsa **New repository**, ponle un nombre (por ejemplo `zapel-3d`) y déjalo en **Public**.
3. Descarga el programa y **renómbralo a `index.html`**, porque GitHub Pages busca ese nombre.
4. Sube los archivos a la **raíz** del repositorio con **Add file → Upload files**:
   - `index.html` (el programa)
   - `README.md`
   - `LICENSE` (ver la sección *Licencia*)

   Pulsa **Commit changes**.
5. Ve a **Settings → Pages**. En *Build and deployment* elige **Deploy from a branch**, la rama **main** y la carpeta **/ (root)**, y pulsa **Save**.
6. Espera uno o dos minutos. El programa quedará en:

   `https://TU-USUARIO.github.io/zapel-3d/`

**Si ves un error 404:** comprueba que el archivo se llame exactamente `index.html` (en minúsculas, sin `.html.html`), que esté en la raíz y no dentro de una carpeta, y que en la pestaña **Actions** el despliegue *pages build and deployment* tenga el check verde. Recarga con Ctrl+F5.

**Para actualizar:** sube el archivo nuevo con el mismo nombre y reemplaza el anterior. La página se actualiza sola en uno o dos minutos.

### Opción B: usarlo en tu computadora, sin internet

1. Descarga `index.html`, con **Code → Download ZIP** o descargando el archivo directamente.
2. Haz doble clic en el archivo para abrirlo con cualquier navegador moderno (Chrome, Edge, Firefox, Safari).

### Opción C: desde la terminal

```bash
git clone https://github.com/TU-USUARIO/zapel-3d.git
cd zapel-3d
# abre index.html en tu navegador
```

## Características

- **Cálculo espacial:** 6 grados de libertad por nodo (3 desplazamientos y 3 giros). Cada barra tiene rigidez axial, torsional y de flexión en los dos planos.
- **Dibujo en planos de trabajo:** se elige el plano (XY, XZ o YZ) y su nivel, y las barras se dibujan sobre él, con ajuste a nodos y a la cuadrícula.
- **Vista 3D:** gira, desplaza y haz zoom libremente. Vistas rápidas: Iso, Planta, Frente y Lateral, con el triedro de ejes en la esquina.
- **Unidades:** **SI (kN · m)** e **Imperial (kip · ft)**, intercambiables en cualquier momento.
- **Secciones transversales** de hormigón, acero o forma irregular:
  - hormigón: rectangular, viga T y circular maciza;
  - acero: perfil I, tubo rectangular y tubo circular, con una lista de perfiles predefinidos (W12×26 a W24×76 e IPE 200, 300 y 400);
  - irregular: se escriben los vértices (x = ancho, y = canto) y el programa calcula el área, las inercias Iy e Iz y la constante de torsión J.
- **Materiales:** hormigón (con f’c, y E = 4.7·√f’c en GPa), acero (E = 200 GPa) u otro. El módulo E siempre se puede corregir a mano.
- **Ver sección:** dibuja cada barra como un prisma 3D con su perfil real a escala, en la vista de modelo.
- **Guardar y abrir** el modelo en tu computadora, en un archivo `.json`.
- **Apoyos:** las seis restricciones por nodo (Ux, Uy, Uz, Rx, Ry, Rz), con atajos para empotrado, articulado y rodillo.
- **Cargas nodales:** Fx, Fy, Fz, Mx, My y Mz.
- **Cargas distribuidas por barra**, con valor al inicio y al final:
  - de gravedad (`w`, positiva hacia abajo);
  - laterales en X (`wx`) y en Y (`wy`), por ejemplo sobre columnas.
- **Articulaciones** en el inicio o en el final de cada barra (liberación del momento flector).
- **Fundación Winkler** en las dos direcciones transversales de la barra (`ks` vertical y `ks` lateral).
- **Subdivisión** de cada barra en varios elementos finitos.
- **Resultados:**
  - deformada 3D, con el valor máximo por barra y **animación**;
  - diagramas de axial **N**, cortantes **Vy** y **Vz**, torsión **T** y momentos **My** y **Mz**;
  - reacción vertical y lateral del suelo;
  - tabla de reacciones, valores máximos y comprobación del equilibrio.
- **En el teléfono:** pellizca con dos dedos para hacer zoom, o usa los botones **＋** y **－**.

## Uso básico

1. Elige el **plano de trabajo** (XY, XZ o YZ) y su **nivel**.
2. Pulsa **Dibujar barra** y haz clic en cada nodo. Termina con clic derecho o `Esc`.
3. Con **Seleccionar**, elige un nodo o una barra y edítalos en el panel derecho:
   - nodo: coordenadas, apoyo y cargas;
   - barra: material, tipo de sección y dimensiones, módulo `E`, giro de la sección, cargas, `ks`, subdivisiones y articulaciones. Debajo de la sección aparecen A, Iy, Iz, J, el canto y el ancho.
4. Pulsa **▶ Calcular** y alterna entre *Deformada* y los diagramas **N, Vy, Vz, T, My, Mz** y *Suelo*.
5. Pulsa **▶ Animar** para ver la deformada en movimiento.
6. Activa o desactiva **Ver sección** para mostrar o no la forma de la sección en cada barra.
7. Usa **💾 Guardar** y **📂 Abrir** para conservar tu modelo.

**Mover la vista:**

| Acción | Ordenador | Teléfono |
|---|---|---|
| Girar | Clic derecho y arrastrar, o arrastrar en un espacio vacío con «Seleccionar» | Arrastrar con un dedo en un espacio vacío con «Seleccionar» |
| Desplazar | Mayús + arrastrar | Arrastrar con dos dedos |
| Zoom | Rueda del ratón | Pellizcar, o botones ＋ y － |

El botón **Encuadrar** ajusta la vista al modelo. Hay dos ejemplos cargados: un pórtico espacial y una viga sobre suelo.

## Guardar y abrir modelos

- **💾 Guardar** descarga el archivo `zapel-3d-modelo.json` con todo el modelo: nodos, apoyos, cargas, barras, secciones, materiales, suelo, articulaciones y unidades.
- **📂 Abrir** carga un archivo guardado, restaura las unidades y recalcula.
- Los resultados no se guardan, porque se recalculan al abrir. Tampoco se guarda la posición de la vista.
- Cada programa solo abre sus propios archivos: un `.json` de ZAPEL Frame no se puede abrir en ZAPEL 3D y aparece un aviso.
- La descarga y la apertura funcionan al usar el programa desde GitHub Pages o como archivo local. Algunos entornos de vista previa bloquean la descarga de archivos.

## Convenciones

| Magnitud | Convención |
|---|---|
| Ejes globales | X, Y horizontales; **Z vertical hacia arriba** |
| Fx, Fy, Fz | Positivas hacia +X, +Y y +Z |
| Mx, My, Mz | Positivos según la regla de la mano derecha |
| Carga `w` | Positiva hacia abajo (gravedad), por unidad de longitud de la barra |
| Cargas `wx`, `wy` | Positivas hacia +X y hacia +Y, por unidad de longitud de la barra |
| Eje local x | Del nodo inicial al nodo final de la barra |
| Eje local z | Vertical en las barras horizontales; el canto de la sección se mide en esta dirección y el ancho, en el eje local y |
| Giro de la sección | Ángulo en grados alrededor del eje de la barra |
| Axial | Positivo en tracción |
| Momentos | Se dibujan del lado de la tracción |
| Reacción del suelo | Positiva en el sentido del eje local correspondiente |

## Limitaciones

- Análisis lineal elástico, sin efectos de segundo orden.
- Sección de propiedades constantes en cada barra. Los perfiles de acero se calculan con dimensiones nominales y sin los radios de acuerdo, por lo que el área y las inercias salen entre 3 y 4 % por debajo de las tablas del fabricante.
- El módulo de corte se toma como `G = E / 2.4`. La constante de torsión J se calcula con fórmulas aproximadas (secciones macizas, de paredes delgadas y cerradas), y en perfiles I sale por debajo del valor de tabla (en la IPE 300, 15.0 cm⁴ frente a 20.1 cm⁴). Afecta solo a la torsión.
- El módulo de balasto `ks` es constante en cada barra.
- Las articulaciones liberan solo el momento flector; la torsión se transmite.
- No incluye losas, muros ni elementos de placa, ni lectura de archivos `.DAT` de ZAPEL, resortes nodales ni asentamientos impuestos.
- Para vigas sobre suelo conviene subdividir las barras en varios elementos para obtener buena precisión.

> Los resultados deben verificarse con casos de solución conocida antes de usarse en un proyecto real. El software se ofrece sin garantía de ningún tipo.

## Licencia

Este trabajo se distribuye bajo la licencia **Creative Commons Atribución-CompartirIgual 4.0 Internacional (CC BY-SA 4.0)**.

[![CC BY-SA 4.0](https://licensebuttons.net/l/by-sa/4.0/88x31.png)](https://creativecommons.org/licenses/by-sa/4.0/deed.es)

**Qué significa:**

- **Compartir:** puedes copiar y redistribuir el material en cualquier medio o formato.
- **Adaptar:** puedes remezclar, transformar y construir a partir del material, incluso con fines comerciales.
- **Atribución:** debes dar crédito a los autores, incluir un enlace a la licencia e indicar si hiciste cambios.
- **CompartirIgual (SA, *ShareAlike*):** si adaptas o transformas el material, debes distribuir tus contribuciones bajo **la misma licencia** que el original.

Texto completo de la licencia: <https://creativecommons.org/licenses/by-sa/4.0/legalcode.es>

**Cómo añadir el archivo `LICENSE` al repositorio:** en GitHub pulsa **Add file → Create new file**, escribe `LICENSE` como nombre y pulsa **Choose a license template**. Elige *Creative Commons Attribution Share Alike 4.0 International* y confirma con **Commit changes**. También puedes copiar el texto desde el enlace anterior.

## Créditos

- Programa original **ZAPEL77P**: Dr. Bernardo Deschapelles.
- Versión web gráfica (ZAPEL 3D): actualizada por el Prof. Raymond Rosa Ávila.

Al reutilizar este trabajo, conserva estos créditos, enlaza la licencia e indica los cambios que hagas.
