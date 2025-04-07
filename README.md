
# Prácticas con Servicios de AWS

Este repositorio contiene una serie de ejercicios prácticos realizados con diferentes servicios de AWS, con el objetivo de aprender y reforzar conceptos clave en la computación en la nube. A continuación se documentan los ejercicios realizados, sus pasos y aprendizajes.

---

## 1. Creación de un Bucket en Amazon S3

Este ejercicio explora **Amazon S3**, el servicio de almacenamiento de objetos de AWS.

**Pasos:**
- Acceder a la consola de S3.
- Crear un nuevo bucket con configuraciones como:
  - Nombre único
  - Propiedad de objetos
  - Habilitación del **versionado** para restaurar versiones anteriores.
- Subir un archivo al bucket.
- Revisar propiedades del objeto, incluyendo la **clase de almacenamiento**.

**Conceptos aprendidos:** almacenamiento escalable, versionado, control de acceso, clases de almacenamiento.

---

## 2. Lanzamiento de un Servidor Web en EC2

Aquí se configura una instancia EC2 para actuar como servidor web.

**Pasos:**
- Acceder a EC2 y seleccionar una **Amazon Machine Image (AMI)**.
- Elegir el tipo de instancia y par de claves para SSH.
- Asociar un **grupo de seguridad** (security group) existente.
- Incluir un script bash en la sección **User data** para automatizar la instalación del servidor web.

**Resultado esperado:** una instancia EC2 corriendo un servidor web al iniciarse.

---

## 3. Configuración de una Launch Template

Primera parte del proceso de configuración para autoescalado.

**Pasos:**
- Crear una **Launch Template** con:
  - AMI
  - Tipo de instancia
  - Par de claves
  - Grupo de seguridad
- Esta plantilla permite lanzar instancias de manera consistente.

 **Objetivo:** establecer una configuración reutilizable para instancias EC2.

---

## 4. Creación de un Auto Scaling Group

Segunda parte de la configuración para autoescalado automático.

**Pasos:**
- Crear un **Auto Scaling Group** en EC2.
- Seleccionar la plantilla creada anteriormente.
- Configurar múltiples zonas de disponibilidad (alta disponibilidad).
- Establecer límites de escalado:
  - Capacidad mínima
  - Capacidad máxima
  - Capacidad deseada

 **Resultado:** escalado automático basado en la demanda, garantizando disponibilidad y eficiencia.

---

## 5. Función Lambda para Manipulación de Cadenas

Desarrollo de una función Lambda para realizar manipulaciones sobre cadenas de texto.

**Funcionalidad:**
- Recibir una cadena vía evento
- Retornar:
  - Cadena original
  - Cadena en mayúsculas
  - Cadena invertida

**Código:**
```python
import json

def lambda_handler(event, context):
    input_string = event.get('input_string', '')
    reversed_string = input_string[::-1]
    uppercase_string = input_string.upper()

    return {
        'statusCode': 200,
        'body': json.dumps({
            'original': input_string,
            'reversed': reversed_string,
            'uppercase': uppercase_string
        })
    }
```
---

## 6. Lanzamiento de una Base de Datos NoSQL con DynamoDB

Configuración de una tabla DynamoDB para almacenar perfiles de clientes.

- Acceder al servicio **DynamoDB** y crear una tabla:
  - **Nombre de la tabla**: `CustomerProfiles`
  - **Clave de partición**: `CustomerID` (tipo string)

- Crear un ítem con los siguientes atributos:

| Atributo   | Valor                  |
|------------|------------------------|
| CustomerID | CUST001                |
| Name       | Jane Doe               |
| Email      | jane.doe@example.com   |

- Usar la opción **Query** para buscar al cliente con `CustomerID = CUST001`.

> **Nota**: las búsquedas son **sensible a mayúsculas y minúsculas**.

** Aprendizajes:**  
Bases de datos NoSQL, claves de partición, estructura de datos flexible, consultas eficientes con claves.

---

##  7. Creación de una VPC

Creación de una red privada virtual (VPC) segura para lanzar recursos dentro de un entorno controlado.

- Acceder al servicio **VPC** y elegir `VPC and more`.
- Configurar los siguientes parámetros:
  - **Nombre**: `datacampvpc`
  - **Número de subredes públicas**: `0` (para mantenerlo aislado)

> Esta VPC permite mayor control sobre la red, ideal para entornos seguros o de producción.

** Aprendizajes:**  
Segmentación de red, configuración de subredes, aislamiento de recursos, bases para seguridad de red.

---

##  8. Optimización de S3 con Intelligent-Tiering

Configuración de almacenamiento inteligente en S3 para manejar patrones de acceso impredecibles y reducir costos.

- Crear un bucket en S3 con:
  - **Tipo**: General purpose
  - **Nombre único**
  - **Propiedad de objetos**: ACLs desactivadas
  - **Habilitar versionado**

- Subir un archivo (`datacamp-logo.png`) y antes de cargarlo:
  - Cambiar la clase de almacenamiento a **Intelligent-Tiering**

- Configurar una **regla de ciclo de vida**:
  - Aplicar a **todos los objetos**
  - Transicionar versiones actuales de objetos a **Intelligent-Tiering**
  - **Días después de la creación**: 0

>  Ideal para datos cuyo patrón de acceso cambia con el tiempo.

** Aprendizajes:**  
Clases de almacenamiento en S3, automatización mediante políticas de ciclo de vida, optimización de costos.

---

##  Aprendizajes Generales ## 

Durante estos ejercicios se exploraron y aplicaron varios conceptos clave del ecosistema AWS:

- 🔹 **Amazon S3**: almacenamiento de objetos, versionado, clases de almacenamiento.
- 🔹 **Amazon EC2**: despliegue de servidores, plantillas de lanzamiento, autoescalado.
- 🔹 **AWS Lambda**: computación sin servidor y lógica de backend.
- 🔹 **Amazon DynamoDB**: bases de datos NoSQL con rendimiento escalable.
- 🔹 **Amazon VPC**: control total sobre la red y seguridad de recursos.
- 🔹 **Gestión de costos**: uso de almacenamiento inteligente y automatizaciones para eficiencia operativa.

Estos ejercicios refuerzan habilidades prácticas en arquitectura, despliegue y administración de soluciones en la nube con AWS.
