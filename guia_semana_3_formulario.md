# Guía Paso a Paso: Tu Primer Formulario en Android (Semana 3)

¡Bienvenido! En esta guía vamos a aprender a diseñar pantallas en Android "a la antigua usanza" (usando **XML**), que es fundamental para entender cómo funciona Android por debajo y cumplir con el temario de la Semana 3.

Vamos a crear una pantalla de **Registro de Usuario** desde cero. No necesitas ser un experto, ¡te lo explicaré todo con peras y manzanas! 🍎🍏

---

## 🛠️ ¿Qué vamos a usar?

Para esta práctica usaremos los bloques de construcción clásicos de Android:
1.  **ConstraintLayout**: Es como un lienzo elástico. Los elementos se "atan" a los bordes o a otros elementos con "muelles" invisibles (constraints).
2.  **EditText**: Cajas donde el usuario puede escribir texto (Nombre, Email).
3.  **RadioButtons**: Botones redondos para elegir **una** opción entre varias (ej. Género).
4.  **CheckBox**: Casilla cuadrada para marcar "Sí" o "No" (ej. Aceptar términos).
5.  **Button**: El botón para confirmar la acción.

---

## 📝 Paso 1: Preparando el Lienzo (Crear el archivo XML)

En tu proyecto de Android Studio, las pantallas visuales viven en la carpeta `res/layout`.

1.  En el panel izquierdo (Project), navega a: `app` > `src` > `main` > `res` > `layout`.
2.  Haz clic derecho sobre la carpeta `layout` -> **New** -> **Layout Resource File**.
3.  En "File name" escribe: `activity_registro`.
4.  En "Root element" asegúrate que diga: `androidx.constraintlayout.widget.ConstraintLayout`.
5.  Dale a **OK**.

¡Listo! Ahora verás una pantalla blanca vacía. Ese es tu lienzo.
*Truco: Arriba a la derecha verás tres botones: "Code", "Split" y "Design". Te recomiendo usar **Split** para ver el código y el resultado visual a la vez.*

---

## 🏗️ Paso 2: Entendiendo el ConstraintLayout

Imagina que `ConstraintLayout` es una pared. Si pegas un cuadro (un botón) sin clavos, se caerá al suelo (o en Android, se irá a la esquina superior izquierda `0,0`).
Para que se quede donde quieres, necesitas ponerle "clavos" o "cuerdas" (constraints) que tiren de él hacia los lados.

*   **Regla de Oro**: Cada elemento necesita al menos **una atadura vertical** (arriba/abajo) y **una atadura horizontal** (izquierda/derecha).

---

## ⌨️ Paso 3: Tu primer campo (Nombre)

Vamos a añadir una caja para que el usuario escriba su nombre.

Copia y pega este código dentro de las etiquetas `<androidx.constraintlayout...>`:

```xml
<EditText
    android:id="@+id/etNombre"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    android:hint="Escribe tu nombre"
    android:inputType="textPersonName"
    
    app:layout_constraintTop_toTopOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    android:layout_margin="16dp" />
```

### 🔍 ¿Qué significa esto? (Explicación para Dummies)
- `id`: Es el nombre único del control (`etNombre`). Lo usaremos luego para buscarlo.
- `width="0dp"`: ¡Ojo aquí! En ConstraintLayout, `0dp` significa "Match Constraints". Le dice al elemento: *"Estírate tanto como te permitan tus ataduras"*.
- `hint`: Es el texto fantasma que desaparece cuando escribes.
- **Las Ataduras (Constraints)**:
    - `layout_constraintTop_toTopOf="parent"`: "Mi parte de **ARRIBA** se pega a la parte de **ARRIBA** de la **PANTALLA** (parent)".
    - `layout_constraintStart...` y `layout_constraintEnd...`: "Mis lados se pegan a los lados de la pantalla".
- `margin="16dp"`: Deja un espacio de respiración alrededor para que no quede pegado al borde.

---

## 🔘 Paso 4: Opciones de Género (RadioGroup)

Los `RadioButton` no les gusta estar solos. Necesitan un "padre" que los vigile para asegurar que solo puedas marcar uno a la vez. Ese padre es el `RadioGroup`.

Añade esto DEBAJO del EditText anterior:

```xml
<RadioGroup
    android:id="@+id/rgGenero"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:orientation="horizontal"
    
    app:layout_constraintTop_toBottomOf="@id/etNombre"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    android:layout_marginTop="16dp">

    <RadioButton
        android:id="@+id/rbMasculino"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Masculino" />

    <RadioButton
        android:id="@+id/rbFemenino"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Femenino" />
</RadioGroup>
```

### 🔍 Análisis
- `layout_constraintTop_toBottomOf="@id/etNombre"`: Esta es la clave. Le dice al grupo: *"Ponte DEBAJO del campo de Nombre"*. Así vamos construyendo una escalera visual.
- `orientation="horizontal"`: Pone los botones uno al lado del otro.

---

## ✅ Paso 5: Términos y Condiciones (CheckBox)

Ahora una casilla simple.

```xml
<CheckBox
    android:id="@+id/cbTerminos"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Acepto los términos y condiciones"
    
    app:layout_constraintTop_toBottomOf="@id/rgGenero"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    android:layout_marginTop="24dp" />
```

### 🔍 Análisis
- Fíjate que seguimos la cadena: `constraintTop_toBottomOf="@id/rgGenero"`. Cada elemento se apoya en el anterior.

---

## 🚀 Paso 6: El Botón Final

Por último, el botón para enviar todo.

```xml
<Button
    android:id="@+id/btnRegistrar"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    android:text="REGISTRARME"
    android:backgroundTint="#6200EE"
    android:textColor="#FFFFFF"
    
    app:layout_constraintTop_toBottomOf="@id/cbTerminos"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    android:layout_margin="16dp" />
```

### 🔍 Análisis
- `width="0dp"`: De nuevo, le decimos que se estire a lo ancho de la pantalla (respetando los márgenes).
- `backgroundTint`: Cambia el color de fondo del botón.

---

## 🏁 Resultado Final (El Código Completo)

Si has seguido los pasos, tu archivo `activity_registro.xml` debería verse así. ¡Puedes copiar y pegar esto si algo falló!

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <!-- 1. Campo Nombre -->
    <EditText
        android:id="@+id/etNombre"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:hint="Nombre Completo"
        android:inputType="textPersonName"
        android:layout_margin="16dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>

    <!-- 2. Grupo de Género -->
    <RadioGroup
        android:id="@+id/rgGenero"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:layout_marginTop="16dp"
        app:layout_constraintTop_toBottomOf="@id/etNombre"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent">

        <RadioButton
            android:id="@+id/rbMasculino"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Masculino" />

        <RadioButton
            android:id="@+id/rbFemenino"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Femenino" />
    </RadioGroup>

    <!-- 3. Checkbox Términos -->
    <CheckBox
        android:id="@+id/cbTerminos"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="He leído y acepto los términos"
        android:layout_marginTop="24dp"
        app:layout_constraintTop_toBottomOf="@id/rgGenero"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>

    <!-- 4. Botón Registrar -->
    <Button
        android:id="@+id/btnRegistrar"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:text="REGISTRARME"
        android:layout_margin="16dp"
        app:layout_constraintTop_toBottomOf="@id/cbTerminos"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>

</androidx.constraintlayout.widget.ConstraintLayout>
```

### 🎓 Resumen para Dummies
1.  **ConstraintLayout** es tu mesa de trabajo.
2.  Cada elemento necesita saber **dónde sentarse** (arriba, abajo, izquierda, derecha).
3.  Usamos `id` para que los elementos se reconozcan entre sí ("Ponte debajo de `@id/etNombre`").
4.  `0dp` es el truco mágico para que los elementos ocupen todo el ancho disponible.

¡Felicidades! Acabas de diseñar tu primera interfaz profesional en Android. 🎉
