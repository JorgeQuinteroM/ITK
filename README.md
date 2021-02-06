# ITK

ITK es una libreria especializada en el tratamiento y procesamiento de imagenes con fines medicos.


## Pasos de instalación: 

* Descargar **cMake** (compilador de C++). https://cmake.org/download/
* Descargar el código fuente de la libreria **ITK** (InsightToolkit-5.1.2.tar.gz). https://itk.org/download/
* Descomprimir el ZIP descargado de la libreria **ITK** y al interior de este, crear una carpeta llamada **build**
* Abrir **cMake**, con el fin de compilar la libreria descargada:

![image](https://user-images.githubusercontent.com/17130267/107123751-47c8d480-686d-11eb-840a-79ec9cb90161.png)

* Dentro de **cMake** sera necesario configurar 2 rutas, la primera de ellas (**Where is the source code**) es la carpeta de donde deseamos extraer el codigo a compilar (ruta a la carpeta de **ITK**).

![image](https://user-images.githubusercontent.com/17130267/107124008-02a5a200-686f-11eb-8d15-ae6fe035909b.png)

* En la segunda ruta sera necesario configurar la ubicación donde requerimos guardar los archivos de compilación (**Where to build binaries**), estos seran almacenados en la carpeta **build** creada anteriormente (en el interior de la carpeta **ITK**)

![image](https://user-images.githubusercontent.com/17130267/107125866-4c47ba00-687a-11eb-9f38-a1d9c4b902fa.png)

* La sección de rutas debe aparecer diligenciada:

![image](https://user-images.githubusercontent.com/17130267/107125878-58cc1280-687a-11eb-88b5-cf5f293456d7.png)

* Una vez configuradas las rutas, sera necesario presionar el botón **Generate**, el cual arrojara una ventana solicitando la opción con la que se desea compilar el proyecto, en donde sera necesario dejar la opción por defecto (**Unix MakeFiles**)

![image](https://user-images.githubusercontent.com/17130267/107125881-61244d80-687a-11eb-85a6-caf41335225b.png)

* El proceso de compilación es un poco extenso, pero habra terminado satisfactoriamente cuando arroje los resultados:

![image](https://user-images.githubusercontent.com/17130267/107125887-6bdee280-687a-11eb-8726-eba323bc1fb7.png)

* Una vez terminado el proceso de compilación, sera necesario desde la consola de comandos, ingresar a la carpeta **build** (al interior de la carpeta **ITK**) y ejecutar el comandos: **make -j4** y **sudo make install**.

![image](https://user-images.githubusercontent.com/17130267/107125896-74371d80-687a-11eb-8f82-1329af583271.png)

![image](https://user-images.githubusercontent.com/17130267/107125903-7bf6c200-687a-11eb-9b05-041deb08e941.png)

* Una vez alcanzado este paso, la libreria estara disponible para ser utilizada desde cualquier proyecto C++. Por lo que ahora crearemos una carpeta nueva (en cualquier ubicación de nuestro PC) y alli sera necesario crear un directorio llamado **build** y dos archivos: 

    - CMakeLists.txt 
    - Example.cxx
    
* La estructura de esta carpeta finalmente sera como:

<img width="696" alt="Captura de pantalla 2021-02-06 a la(s) 1 02 56 p  m" src="https://user-images.githubusercontent.com/17130267/107126084-c593dc80-687b-11eb-9bc1-55e23ac8187b.png">
    
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

![image](https://user-images.githubusercontent.com/17130267/107125915-89ac4780-687a-11eb-8edb-ca4bba6e6186.png)

* Finalmente se presiona el botón **Generate** y se dejan las opciones por defecto. La compilación habra terminado cuando se reciban los resultados: 

![image](https://user-images.githubusercontent.com/17130267/107125918-929d1900-687a-11eb-85e4-ee7025c664c9.png)

* Desde la consola de comandos y al interior de la carpeta **build** se ejecutara el comando **make**.

![image](https://user-images.githubusercontent.com/17130267/107125934-ad6f8d80-687a-11eb-8711-500428702489.png)

* Finalmente, el ejecutable ya estara disponible y podra lanzarce con el comando: 

![image](https://user-images.githubusercontent.com/17130267/107125938-b2ccd800-687a-11eb-9e6f-af93eea8d85c.png)

