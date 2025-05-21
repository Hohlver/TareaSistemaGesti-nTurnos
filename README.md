# Sistema de Gestión de Turnos Digitales

## 📌 Descripcion general

El sistema tunomatico presenta una solucion para la gestion automatizada de turnos en entornos que requieren de atencion secuencial de clientes, ya sean bancos, hospitales o servicios publicos en general. El sistema permite asignar turnos de manera inteligente, notificar a usuarios y gestionar colas de atencion, optimizando tiempos de espera y mejorando la experiencia de usuario.


## 🖼️ Diagramas UML 

### 1. Diagrama de Casos de Uso 
![CASOUSO](https://github.com/user-attachments/assets/824e6433-8c79-4ab9-87d8-8f7209651b56)
- `Cliente` puede **ingresar datos**, lo que puede **extenderse** a **solicitar turno** o **cancelar turno**.
- Ambas acciones principales (**solicitar** y **cancelar turno**) utilizan `<<include>>` para **verificar disponibilidad** y **enviar notificación**, reflejando lógica de negocio reutilizable.
- `Admin` tiene acceso especial al sistema mediante **iniciar sesión como admin**, lo cual puede **extenderse** a **gestionar reportes** y **gestionar horarios**.
- El actor `Sistema` es responsable de procesos internos automatizados como notificaciones o validaciones de disponibilidad.

### 2. Diagrama de Clases
![CLASES](https://github.com/user-attachments/assets/348cbe05-f630-4e78-b8c1-4692974ad65a)
- `GestorTurnosSingleton` aplica el patrón **Singleton**, asegurando que haya una única instancia controladora de la lógica de turnos.
- `TurnoPrototype` implementa el patrón **Prototype**, permitiendo la clonación eficiente de estructuras base de turnos según demanda.
- `NotificadorAdapter` actúa como un puente entre el sistema y un servicio externo de notificaciones, aplicando el patrón **Adapter** para desacoplar dependencias de APIs externas.
- La clase `DatosCliente` encapsula la información básica provista por el cliente al solicitar un turno.

Todos los métodos relevantes están definidos, y no hay clases aisladas o sin responsabilidad clara.

### 3. Diagrama de Implementación
![IMPLEMENTACION](https://github.com/user-attachments/assets/868fd619-94f7-49d1-9c33-594fd859cb41)
- **Cliente Web** accede a la **Interfaz de Usuario** mediante protocolo **HTTPS**, garantizando seguridad en la comunicación.
- El **Servidor Central** aloja el componente `GestorTurnos`, que:
  - Consulta y persiste datos en la **Base de Datos** vía **JDBC**, incluyendo las tablas de `Turnos` y `Reportes`.
  - Interactúa con `NotificadorAdapter`, que sirve de intermediario para consumir el **Sistema Externo** mediante **API REST**.
- La comunicación con el sistema de notificaciones externas está desacoplada y permite cambios en la tecnología sin afectar la lógica interna del sistema.

Este diseño promueve **separación de responsabilidades**, **alta cohesión** y **bajo acoplamiento**, pilares fundamentales de la arquitectura de software profesional.


## 🧠 Reflexiones Finales del Modelado

El proceso de modelado arquitectónico permitió aplicar las buenas prácticas de la ingeniería de software y además demostrar la posible evolución de una visión funcional inicial a una implementación realista en base a los patrones de diseño aplicados, no solo mejorando la claridad estructural de un proyecto, sino que facilitando también la decisiones arquitectónicas clave que se presentan en su desarrollo, tales como la reutilización (Prototype), la unicidad de control (Singleton) y la interoperabilidad con servicios externos (Adapter).

----
