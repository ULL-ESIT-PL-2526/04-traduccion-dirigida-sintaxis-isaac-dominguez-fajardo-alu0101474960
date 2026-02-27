# Pratcica 4 informe
Esta práctica tiene como objetivo desarrollar una calculadora utilizando una gramática independiente del contexto y una Definición Dirigida por la Sintaxis (SDD) implementada en Jison. El programa analizará expresiones matemáticas y calculará su valor en el momento de procesarlas.


## Objetivos principales

1. Configurar el entorno: Instalar dependencias, generar el parser con Jison y ejecutar las pruebas con Jest.
2. Comprender el Lexer: Analizar el bloque %lex actual y responder a preguntas teóricas sobre el reconocimiento de tokens.
3. Añadir comentarios: Modificar el analizador léxico para omitir los comentarios de una sola línea que comiencen por //.
4. Soportar números flotantes: Extender el analizador para reconocer números en formato de punto flotante y notación científica (ej. 2.35e-3).
5. Añadir pruebas: Escribir nuevas pruebas en Jest para validar estas modificacion

## Solución a las preguntas teóricas

1. **Diferencia entre /* skip whitespace */ y devolver un token:** Cuando se omite un texto, le estamos diciendo al analizador léxico que lo ignore y no se lo pase al analizador sintáctico. En cambio, al devolver un token, se envía esa pieza de información al parser para que evalúe las reglas gramaticales (como $E\rightarrow T$ ).
2. **Secuencia para $123**45+0$:** El analizador generará los siguientes tokens en orden: NUMBER (123), OP (**), NUMBER (45), OP (+), NUMBER (0).
3. **¿Por qué $**$ debe aparecer antes que [-+$*$/]?:** Jison evalúa las expresiones regulares en orden de arriba a abajo. Si el grupo [-+$*$/] estuviera primero, Jison leería el primer $*$ de $**$ y lo clasificaría como un operador de multiplicación, dejando el segundo $*$ huérfano y rompiendo la lógica de la potencia.
4. **¿Cuándo se devuelve EOF?:** Se devuelve cuando el analizador alcanza el final del archivo o de la cadena de texto de entrada, indicando que no hay más caracteres por procesar.
5. **Regla INVALID:** Actúa como una red de seguridad. Si el analizador encuentra un carácter extraño (por ejemplo, un @) que no encaja con ningún token válido, esta regla evita que el programa se bloquee silenciosamente, permitiendo manejar el error léxico adecuadamente.
