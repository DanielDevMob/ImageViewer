# ImageViewer

Visor de imágenes de escritorio desarrollado en Java.

Este proyecto forma parte de la asignatura de Ingeniería del Software II. El propósito principal es la implementación de una arquitectura de software desacoplada (Clean Architecture), demostrando cómo separar la lógica de visualización y manipulación de imágenes de la interfaz de usuario concreta.

## Estructura del Proyecto

El código fuente se divide en dos paquetes para garantizar el cumplimiento del Principio de Inversión de Dependencias:

1. **software.ulpgc.imageviewer.architecture**
   Contiene el núcleo del dominio: interfaces (`Image`, `ImageDisplay`, `ImageStore`) y la lógica de control (`Command`, `NextCommand`, `PrevCommand`). Este paquete no tiene dependencias de librerías gráficas ni externas.

2. **software.ulpgc.imageviewer.application**
   Contiene las implementaciones concretas:
   * **SwingImageDisplay:** Componente gráfico personalizado que extiende `JPanel`. Gestiona el renderizado mediante `Graphics2D` y transformaciones afines.
   * **FileImageStore:** Acceso al sistema de archivos con filtrado de extensiones.
   * **Desktop:** Ventana principal (JFrame) y configuración de eventos.

## Funcionalidad Implementada

A diferencia de un visor estático, esta implementación incluye un motor de interacción avanzado en la clase `SwingImageDisplay`:

* **Zoom:** Implementado mediante `AffineTransform`. Permite acercar y alejar la imagen usando la rueda del ratón.
* **Panning (Desplazamiento):** Cuando la imagen tiene zoom, el usuario puede arrastrarla con el ratón para ver diferentes áreas.
* **Gestos (Swipe):** Si la imagen está en su escala original, arrastrar horizontalmente funciona como gesto para cambiar a la imagen anterior o siguiente.
* **Interfaz Superpuesta:** Los controles de navegación se renderizan en una capa superior (`JLayeredPane`), maximizando el área de visualización.

## Decisiones de Diseño

* **Command Pattern:** Las acciones de navegación están encapsuladas en comandos, permitiendo que sean invocadas desde botones, teclas o gestos sin acoplamiento.
* **Observer Pattern (Listener):** Se ha definido una interfaz interna en el display para notificar al contenedor (`Desktop`) cuando se completa un gesto de cambio de imagen.
* **Single Responsibility:** La clase `FileImageStore` se encarga exclusivamente de la lectura y filtrado de archivos, mientras que `SwingImageDisplay` se encarga únicamente de la lógica geométrica de visualización.

## Requisitos y Ejecución

* Java 21
* Maven

Pasos para ejecutar el proyecto:

1. Clonar el repositorio.
2. Crear una carpeta llamada "images" en la raíz del proyecto y añadir archivos de imagen (.jpg, .png).
3. Compilar el proyecto:
   mvn clean install
4. Ejecutar la clase principal:
   software.ulpgc.imageviewer.application.gui.Main
