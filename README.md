# Python Signals / Events

Este proyecto implementa un sistema de eventos en Python similar al de C#, permitiendo suscribir y desuscribir manejadores de eventos (handlers) de forma sencilla utilizando operadores.

## Características

- **Sintaxis intuitiva**: Uso de `+=` para agregar suscriptores y `-=` para removerlos.
- **Desacoplamiento**: Permite separar la lógica de disparo de eventos de la lógica de manejo.
- **Flexibilidad**: Soporta múltiples manejadores para un mismo evento.

## Estructura

- `events.py`: Contiene la implementación base del sistema de eventos (`Event`, `IEvent`, `EventHandler`).
- `main.py`: Ejemplo de uso con clases como `Button`, `Label` y `User`.

## Ejemplo de uso

```python
from events import Event

def mi_handler(mensaje):
    print(f"Evento recibido: {mensaje}")

evento = Event()
evento += mi_handler  # Suscribirse
evento.emit("Hola!")  # Disparar evento
evento -= mi_handler  # Desuscribirse
```
> ### También podemos heredar de la calse event
```python

from events import Event 

class Label(Event):
    def __init__(self):
        self.text_changed = Event()

    def set_text(self, text):
        self.text = text
        self.text_changed.emit(self.text)

def print_label(text):
    print("Label printed:", text)

def main():
    label = Label()
    label.text_changed += print_label
    label.set_text("Hola mundo")
    label.set_text("Adios mundo")
    label.text_changed -= print_label
    label.set_text("No se imprimira")
```
