# 📘 Unidad Didáctica 2: Crea tu propio Examen Online con Python y Streamlit

**Asignatura:** Tecnología y Digitalización (3º ESO)  
**Herramienta:** Python + Streamlit  
**Objetivo:** Aprender a usar formularios, listas y diccionarios

# 🚀 Introducción

Vamos a crear una aplicación que hace exámenes y se corrige sola de forma automática. Para ello usaremos **Streamlit**, una herramienta que convierte código Python en páginas web.

---

## 📂 1. Concepto Clave: El "Archivador" de Datos

Para que nuestro programa sepa qué preguntar, usamos una **lista de diccionarios**. Imaginalo como un **archivador de oficina**:

- **La Lista `[ ]`**: Es el mueble entero. Cada cajón tiene un número de posición (empezando siempre por el **0**).
  
- **El Diccionario `{ }`**: Es la ficha que hay dentro de cada cajón. Cada ficha tiene etiquetas (llamadas **claves**) como `"texto"`, `"opciones"` o `"correcta"`.
  

**¿Cómo sacamos la información?** Si quieres la pregunta del segundo cajón, escribirías: `preguntas[1]["texto"]`. *(Recuerda: el índice 1 es el segundo cajón porque en programación empezamos a contar desde el cero).*

---

## 📝 2. El Código del Proyecto

Crea un archivo llamado `examen.py` y pega el siguiente código. Lee los comentarios (el texto que empieza por `#`) para entender qué hace cada parte:

```
import streamlit as st

# 1. EL ARCHIVADOR (Nuestra base de datos de preguntas)
# Cada bloque entre { } es una pregunta distinta. Creamos la lista
preguntas = [
    {
        "texto": "¿Cuál es el lenguaje de programación que estamos usando?",
        "opciones": ["Java", "Python", "C++", "JavaScript"],
        "correcta": "Python"
    },
    {
        "texto": "¿Qué comando se usa para ejecutar una app de Streamlit?",
        "opciones": ["python run", "streamlit run", "start streamlit"],
        "correcta": "streamlit run"
    },
    {
        "texto": "¿En qué año se lanzó la Web 1.0?",
        "opciones": ["1983", "1990", "2005"],
        "correcta": "1990"
    }
]

# Configuración visual de la página
st.title("🎓 Mi Primer Examen Interactivo")
st.write("Responde a las preguntas y pulsa el botón al final para saber tu nota.")

# 2. EL FORMULARIO (Agrupamos todo para que no se recargue la web a cada clic)
# Eso se consigue con el comando with

with st.form("quiz_form"):

    # Aquí guardaremos las respuestas que elija el alumno. Será una lista.
    respuestas_usuario = []

    # Recorremos el archivador usando un bucle 'for' para crear las preguntas
    # Con sus opciones
    for pregunta in preguntas:
        st.subheader(pregunta["texto"]) # Ponemos el texto de la pregunta

        # Creamos los botones de opción (radio)
        eleccion = st.radio("Elige una opción:", pregunta["opciones"], key=p["texto"])

        # Guardamos la elección en nuestra lista usando append ()
        respuestas_usuario.append(eleccion)
        st.write("---") # Una línea para separar preguntas

    # Botón obligatorio para cerrar el formulario
    boton_enviar = st.form_submit_button("Entregar Examen")

# 3. LA CORRECCIÓN (Solo ocurre cuando pulsamos el botón)
if boton_enviar:
    aciertos = 0
    # Total es número de preguntas (usa el método len)
    total = len(preguntas)

    # Comparamos las respuestas del usuario con las 'correctas' del archivador
    for i in range(total):
        if respuestas_usuario[i] == preguntas[i]["correcta"]:
            aciertos = aciertos + 1

    # Calculamos la nota sobre 10
    nota = (aciertos / total) * 10

    # Mostramos el resultado con colores
    st.divider()
    st.header(f"Resultado final: {nota} / 10")

    if nota >= 5:
        st.success(f"¡Felicidades! Has aprobado con {aciertos} aciertos.")
        st.balloons() # ¡Efecto de globos!
    else:
        st.error(f"Has sacado un {nota}. ¡Toca estudiar un poco más!")
```
