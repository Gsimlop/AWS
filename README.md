
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
