# ITK

# ITK 


ITK es una libreria especializada en el tratamiento y procesamiento de imagenes con fines medicos.


## Pasos de instalación: 

* Descargar **cMake** (compilador de C++). https://cmake.org/download/
* Descargar el código fuente de la libreria **ITK** (InsightToolkit-5.1.2.tar.gz). https://itk.org/download/
* Descomprimir el ZIP descargado de la libreria **ITK** y al interior de este, crear una carpeta llamada **build**
* Abrir **cMake**, con el fin de compilar la libreria descargada:


![Captura_de_pantalla_2021-02-04_a_la_s__11.10.27_p._m.](/uploads/e66234c069efc5f4bd860690acb4ea1f/Captura_de_pantalla_2021-02-04_a_la_s__11.10.27_p._m..png)

* Dentro de **cMake** sera necesario configurar 2 rutas, la primera de ellas (**Where is the source code**) es la carpeta de donde deseamos extraer el codigo a compilar (ruta a la carpeta de **ITK**).

![Captura_de_pantalla_2021-02-04_a_la_s__11.11.07_p._m.](/uploads/137b9d074d21ee9f667d4953b222ee95/Captura_de_pantalla_2021-02-04_a_la_s__11.11.07_p._m..png)

* En la segunda ruta sera necesario configurar la ubicación donde requerimos guardar los archivos de compilación (**Where to build binaries**), estos seran almacenados en la carpeta **build** creada anteriormente (en el interior de la carpeta **ITK**)

![Captura_de_pantalla_2021-02-04_a_la_s__11.11.39_p._m.](/uploads/95c342b1dcd98c2b16e4a86058373565/Captura_de_pantalla_2021-02-04_a_la_s__11.11.39_p._m..png)

* La sección de rutas debe aparecer diligenciada:

![Captura_de_pantalla_2021-02-04_a_la_s__11.44.51_p._m.](/uploads/4548aba2b0831d87f8edba3d60511bca/Captura_de_pantalla_2021-02-04_a_la_s__11.44.51_p._m..png)

* Una vez configuradas las rutas, sera necesario presionar el botón **Generate**, el cual arrojara una ventana solicitando la opción con la que se desea compilar el proyecto, en donde sera necesario dejar la opción por defecto (**Unix MakeFiles**)

![Captura_de_pantalla_2021-02-04_a_la_s__11.19.52_p._m.](/uploads/9cf111704223d22e9027613c366a20a2/Captura_de_pantalla_2021-02-04_a_la_s__11.19.52_p._m..png)

* El proceso de compilación es un poco extenso, pero habra terminado satisfactoriamente cuando arroje los textos:

![Captura_de_pantalla_2021-02-04_a_la_s__11.45.46_p._m.](/uploads/f8600ad5451834d3c167636805f8cdc6/Captura_de_pantalla_2021-02-04_a_la_s__11.45.46_p._m..png)

* Una vez terminado el proceso de compilación, sera necesario desde la consola de comandos, ingresar a la carpeta **build** (al interior de la carpeta **ITK**) y ejecutar el comandos: **make -j4** y **sudo make install**.

![Captura_de_pantalla_2021-02-05_a_la_s__12.01.25_a._m.](/uploads/198f2446c786305ec7b6ceecc17a3789/Captura_de_pantalla_2021-02-05_a_la_s__12.01.25_a._m..png)

![Captura_de_pantalla_2021-02-04_a_la_s__11.58.58_p._m.](/uploads/d2ae15f082a6fc27054f3e794c6f77b8/Captura_de_pantalla_2021-02-04_a_la_s__11.58.58_p._m..png)


* Una vez alcanzado este paso, la libreria estara disponible para ser utilizada desde cualquier proyecto C++. Por lo que ahora crearemos una carpeta nueva (en cualquier ubicación de nuestro PC) y alli sera necesario crear un directorio llamado **build** y dos archivos: 

    - CMakeLists.txt 
    - Example.cxx
    
* El archivo **CMakeLists.txt** deberia tener la estructura presentada a continuación: 

```c++
#RUTA A LA LIBRERIA ITK (ESTA DEBE SER EDITADA SEGÚN LA UBICACIÓN EN DONDE SE INSTALO Y COMPILO ITK)
SET(ITK_DIR "/Users/jorgeluisquinterogomez/Desktop/Mis\ papeles/Jorge/Maestria/Procesamiento\ Imagenes/Imagenes\ Medicas/InsightToolkit-5.1.2/build")

#MINIMA VERSION DE CMAKE QUE DESEAMOS USAR
cmake_minimum_required(VERSION 2.8)

#NOMBRE DEL PROYECTO 
project(Example)

#IMPORTAR ITK 
find_package(ITK REQUIRED)
include(${ITK_USE_FILE})

add_executable(Example Example.cxx)

#ENLAZAR A LIBRERIA ITK
target_link_libraries(Example ${ITK_LIBRARIES})
```

* El archivo **Example.cxx** es nuestro script en C++ e inicialmente unicamente importara la libreria de **ITK** para validar que funcione correctamente.

```c++
#include <iostream>
#include "itkImage.h"
#include "itkImageFileReader.h"
#include "itkGradientMagnitudeImageFilter.h"

int main() {
    std::cout << "Hello World!";
    return 0;
}
```

* Una vez implementados los scripts, sera necesario compilarlos al igual que se realizo con la libreria **ITK**. Desde **cMake** se configura el **source**, al igual que la ruta de destino del **build**.

![Captura_de_pantalla_2021-02-05_a_la_s__12.15.34_a._m.](/uploads/250936067b7ff0760fbc72f0767b2150/Captura_de_pantalla_2021-02-05_a_la_s__12.15.34_a._m..png)

* Finalmente se presiona el botón **Generate** y se dejan las opciones por defecto. La compilación habra terminado cuando se reciban los resultados: 

![Captura_de_pantalla_2021-02-05_a_la_s__12.15.39_a._m.](/uploads/0e029deb5f08e2ced4b6387623d43a00/Captura_de_pantalla_2021-02-05_a_la_s__12.15.39_a._m..png)


* Desde la consola de comandos y al interior de la carpeta **build** se ejecutara el comando **make**.

![Captura_de_pantalla_2021-02-05_a_la_s__12.23.00_a._m.](/uploads/ba22ffadd1a2efed036857886de53b03/Captura_de_pantalla_2021-02-05_a_la_s__12.23.00_a._m..png)

* Finalmente, el ejecutable ya estara disponible y podra lanzarce con el comando: 

![Captura_de_pantalla_2021-02-05_a_la_s__12.26.49_a._m.](/uploads/d237ee5a88a246473e1bd99522171f84/Captura_de_pantalla_2021-02-05_a_la_s__12.26.49_a._m..png)

