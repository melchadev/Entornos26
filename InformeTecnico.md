</> Markdown

# Informe técnico - Inicidencia formulario de contacto (BuggyWebApp)

## 1. Descripción del problema:
El formulario de contacto se procesa auqnue los campos name y email estén vacíos. El sistema finaliza como si los datos fueran válidos.

## 2. Cómo se produce:

1. Ejecutamos la aplicación (MainApp).
2. Enviamos el formulario con name = "" y email= "".
3. Podemos observar que el sistema procesa el formulario igualmente.

## 3. Análisis técnico:

Mediante el uso de Debugger observamos que el método 'submitContactForm' recibe 'name= "" ' y 'email="" '.
El controlador crea un objeto 'ContactForm' con esos valores y llama al método 'processForm' del servicio.

Una vez dentro de 'processForm' se ejecuta una validación del email usando 'Validator.validateEmail(email)'.
Cuando el email está vacío, la función devuelve 'false', pero obervamos que el sistema no deja de ejecutarse y continúa con el procesando el formulario.

## 4. Causa raíz:
La validación del email no controla el flujo del programa. Aunque el método de validación devuelve 'false', el sistema no tiene ninguna condición que impida continuar con el procesamiento del formulario.

## 5. Solución:
Añadir una validación que compruebe si los campos de 'name' y 'email' están vacíos.
En el caso de que la validación falle, el sistema debe mostrar un mensaje de error y detener el procesamiento.