
# Buenas Prácticas en el Desarrollo de Software

En esta sección abordamos las principales buenas prácticas que todo desarrollador debería seguir para escribir código limpio, mantenible y escalable. También veremos los principios SOLID y el enfoque de Clean Code.

---

# Buenas Prácticas Generales

| Práctica                    | Descripción                                                                 |
|----------------------------|-----------------------------------------------------------------------------|
| 🔠 Nombres claros           | Usar nombres descriptivos para variables, funciones y clases.              |
| 📦 Organización del proyecto| Mantener una estructura de carpetas coherente.                             |
| 🧪 Probar el código         | Escribir pruebas unitarias y de integración.                               |
| 📝 Documentar               | Comentar lo necesario y crear archivos como README.md.                     |
| 🔁 No repetir código (DRY)  | Reutilizar funciones en lugar de copiar y pegar lógica.                    |
| 🔧 Manejo de errores        | Usar try/except y logs para detectar errores de forma controlada.          |
| 📚 Control de versiones     | Utilizar Git para rastrear cambios y colaborar.                            |
| 🤝 Revisiones de código     | Revisar código entre compañeros (code review) para detectar mejoras.       |

---



# Principios SOLID

Los principios SOLID son cinco principios fundamentales para un diseño orientado a objetos mantenible y escalable.

### 1. **🧱 S - Single Responsibility Principle**

Una clase debe tener una sola razón para cambiar.

Este principio nos invita a dividir responsabilidades. Una clase no debe encargarse de múltiples cosas, porque si una cambia, afecta a toda la clase.

🔧 Ejemplo:
Una clase Factura no debería encargarse de imprimir y enviar la factura. Mejor, delegar esas tareas a otras clases como ImpresoraFactura o NotificadorFactura.

**Ejemplo:**
```python
# Mala práctica
class Report:
    def generate(self): ...
    def save_to_pdf(self): ...

# Buena práctica
class ReportGenerator:
    def generate(self): ...

class PDFExporter:
    def save_to_pdf(self): ...
```

---

### 2. **🔌 O - Open/Closed Principle**

Las entidades deben estar abiertas para su extensión, pero cerradas para su modificación.

Esto significa que puedes agregar nueva funcionalidad sin modificar el código existente. Se logra con herencia o composición.

🔧 Ejemplo:
Si agregas nuevos tipos de usuarios en un sistema, no necesitas modificar la clase original Usuario, sino extenderla creando UsuarioPremium, UsuarioAdmin, etc.

**Ejemplo:**
```python
# ✅ Buena práctica
class Saludo:
    def mensaje(self):
        return "Hola"

class SaludoFormal(Saludo):
    def mensaje(self):
        return "Buenos días"
```

---

### 3. **🎯 L - Liskov Substitution Principle (LSP)**

Las subclases deben poder reemplazar a sus clases base sin alterar el comportamiento esperado.

Este principio garantiza que una clase hija mantenga el comportamiento de su clase padre, sin generar errores.

🔧 Ejemplo:
Si una clase Ave tiene un método volar(), no deberías hacer que Pingüino herede de Ave, porque no puede volar. Romperías el contrato lógico.

**Ejemplo:**
```python
# ✅ Buena práctica
class Ave:
    def volar(self): pass

class Aguila(Ave):
    def volar(self): print("Vuela alto")

# Si creamos una subclase que no puede volar (como un pingüino), rompe el principio
```

---

### 4. **🔗 I - Interface Segregation Principle (ISP)**

Los clientes no deben estar obligados a depender de interfaces que no utilizan.

En lugar de tener una gran interfaz con muchos métodos, se recomienda crear interfaces más pequeñas y específicas para cada tipo de cliente.

🔧 Ejemplo:
Separar Imprimible, Escaneable y Faxable en interfaces distintas, en lugar de una interfaz Multifuncional.

**Ejemplo:**
```python
# ✅ Interfaces pequeñas para roles específicos
class Imprimible:
    def imprimir(self): pass

class Escaneable:
    def escanear(self): pass
```
---

### 5. **🧱 D - Dependency Inversion Principle (DIP)**
Las clases deben depender de abstracciones, no de implementaciones concretas.

Este principio fomenta la desacoplación del código, lo cual facilita el mantenimiento y la prueba. Las clases de alto nivel no deben depender directamente de clases de bajo nivel.

🔧 Ejemplo:
En lugar de que una clase Auto cree su propio Motor, debe recibirlo como parámetro, usando una interfaz IMotor.

**Ejemplo:**
```python
# ❌
class Motor:
    def encender(self): pass

class Auto:
    def __init__(self):
        self.motor = Motor()

# ✅
class IMotor:
    def encender(self): pass

class Motor(IMotor): ...
class Auto:
    def __init__(self, motor: IMotor):
        self.motor = motor
```
---

# 🧼 Principios de Clean Code

Clean Code, o código limpio, es un enfoque de escritura de código que prioriza la claridad, la simplicidad y la legibilidad, más allá de que el código simplemente funcione.


### 📌 Principios Clave

| Principio                   | Descripción                                                                 |
|----------------------------|-----------------------------------------------------------------------------|
| 🏷️ Nombres significativos    | Usa nombres que describan claramente lo que hacen o representan.             |
| 🔁 No te repitas (DRY)       | Extrae funciones o clases comunes, evita copiar código.                      |
| 🧩 Funciones pequeñas        | De preferencia menos de 20-30 líneas.                                        |
| 🧼 Una función = una tarea   | No mezcles responsabilidades en la misma función.                            |
| 🧠 Comentarios útiles        | Comenta el "por qué", no el "qué".                                           |
| 🧱 Modulariza tu código      | Divide en funciones, módulos y clases según sus responsabilidades.           |
| 🧪 Escribe pruebas           | Asegura que el código funciona correctamente al modificarlo.                 |
| 📚 Documentación mínima      | Usa README, docstrings, comentarios clave y guías de uso.                    |
| 🎯 Consistencia              | Sigue una convención (PEP8 en Python, por ejemplo).                          |


### Ejemplo de Clean Code:

```python
# Código confuso
# ❌ Código desordenado y poco claro
def p(l):
    for i in l:
        if i[1] == 1:
            print(i[0])

# ✅ Código limpio y entendible
def imprimir_usuarios_activos(usuarios):
    for nombre, activo in usuarios:
        if activo == 1:
            print(nombre)
```

---

Aplicar estas prácticas y principios no solo mejora la calidad del software, sino que también facilita el trabajo en equipo y la escalabilidad de los proyectos.
