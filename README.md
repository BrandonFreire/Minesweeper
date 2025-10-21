# 🎮 Buscaminas con Inteligencia Artificial

<div align="center">

![Python](https://img.shields.io/badge/Python-3.12-blue.svg)
![Pygame](https://img.shields.io/badge/Pygame-2.x-green.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

**Un juego clásico de Buscaminas con un agente de IA que utiliza lógica proposicional para resolver el juego**

[Características](#-características) •
[Instalación](#-instalación) •
[Uso](#-uso) •
[Cómo Funciona](#-cómo-funciona-la-ia) •
[Estructura](#-estructura-del-proyecto)

</div>

---

## 📋 Descripción

Este proyecto implementa el clásico juego del Buscaminas con una interfaz gráfica interactiva construida con Pygame. Lo que hace especial a este proyecto es la inclusión de un **Agente de Inteligencia Artificial** que puede jugar automáticamente utilizando inferencia lógica y razonamiento proposicional.

El juego permite tanto el juego manual como observar cómo la IA toma decisiones inteligentes para despejar el tablero sin tocar minas.

## ✨ Características

### 🎯 Modo de Juego Manual
- **Click izquierdo**: Revelar una celda
- **Click derecho**: Marcar/desmarcar una celda como mina
- Interfaz gráfica intuitiva y limpia
- Contador visual de minas cercanas
- Banderas para marcar minas sospechosas

### 🤖 Agente de IA Inteligente
- Utiliza **lógica proposicional** para tomar decisiones
- Mantiene una **base de conocimiento** sobre el estado del tablero
- Realiza **inferencias** para identificar celdas seguras y minas
- Toma decisiones aleatorias informadas cuando no hay movimientos seguros obvios
- Visualización en tiempo real de las decisiones de la IA

### 🎨 Interfaz Gráfica
- Diseño limpio y profesional
- Sprites para minas y banderas
- Animaciones suaves
- Pantalla de instrucciones inicial
- Mensajes de victoria/derrota

## 🚀 Instalación

### Requisitos Previos
- Python 3.8 o superior
- pip (gestor de paquetes de Python)

### Pasos de Instalación

1. **Clonar o descargar el proyecto**
   ```bash
   cd buscaminas
   ```

2. **Instalar dependencias**
   ```bash
   pip install -r requirements.txt
   ```

   O instalar Pygame directamente:
   ```bash
   pip install pygame
   ```

## 🎮 Uso

### Ejecutar el Juego

```bash
python runner.py
```

### Controles del Juego

| Acción | Control |
|--------|---------|
| Revelar celda | Click izquierdo |
| Marcar como mina | Click derecho |
| Activar/desactivar IA | Botón "AI Agent" |
| Reiniciar juego | Botón "Reset" |

### Modos de Juego

1. **Modo Manual**: Juega tú mismo haciendo clic en las celdas
2. **Modo IA**: Activa el agente de IA y observa cómo resuelve el tablero
3. **Modo Mixto**: Juega algunas movidas y luego deja que la IA continúe

## 🧠 Cómo Funciona la IA

### Algoritmo de Razonamiento

La IA utiliza un enfoque basado en **lógica proposicional** para resolver el Buscaminas:

#### 1. **Representación del Conocimiento**
```python
Sentence(cells, count)
```
- **cells**: Conjunto de celdas
- **count**: Número de minas en ese conjunto

Ejemplo: `{(0,1), (0,2), (1,1)} = 2` significa "2 de estas 3 celdas contienen minas"

#### 2. **Proceso de Inferencia**

```
┌─────────────────────────────────────┐
│  1. Marcar celda como movimiento    │
│     realizado                       │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│  2. Agregar nueva sentencia a la    │
│     base de conocimiento            │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│  3. Identificar minas conocidas:    │
│     Si |células| = count            │
│     → todas son minas               │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│  4. Identificar celdas seguras:     │
│     Si count = 0                    │
│     → todas son seguras             │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│  5. Inferir nuevas sentencias:      │
│     Si S1 ⊂ S2, entonces            │
│     S2 - S1 = count2 - count1       │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│  6. Repetir hasta convergencia      │
└─────────────────────────────────────┘
```

#### 3. **Toma de Decisiones**

La IA prioriza sus movimientos:

1. **Movimiento Seguro**: Si hay celdas conocidas como seguras
2. **Movimiento Aleatorio**: Si no hay información suficiente, elige aleatoriamente entre celdas no exploradas

### Ejemplo de Inferencia

```
Situación inicial:
  Celda A revelada: 1 mina cercana en {B, C, D}
  → Sentencia: {B, C, D} = 1

Nueva información:
  Celda E revelada: 2 minas cercanas en {B, C, D, F, G}
  → Sentencia: {B, C, D, F, G} = 2

Inferencia:
  {B, C, D, F, G} - {B, C, D} = {F, G}
  2 - 1 = 1
  → Nueva sentencia: {F, G} = 1
```

## 📁 Estructura del Proyecto

```
buscaminas/
│
├── minesweeper.py          # Lógica del juego y del agente de IA
│   ├── Minesweeper         # Clase del tablero del juego
│   ├── Sentence            # Representación de sentencias lógicas
│   └── MinesweeperAI       # Agente de IA
│
├── runner.py               # Interfaz gráfica con Pygame
│   ├── Inicialización      # Configuración de Pygame
│   ├── Game Loop           # Bucle principal del juego
│   └── Event Handling      # Manejo de eventos del usuario
│
├── requirements.txt        # Dependencias del proyecto
│
├── assets/                 # Recursos gráficos
│   ├── fonts/
│   │   └── OpenSans-Regular.ttf
│   └── images/
│       ├── flag.png        # Imagen de la bandera
│       └── mine.png        # Imagen de la mina
│
└── README.md              # Este archivo
```

## 🔧 Configuración Personalizada

Puedes modificar los parámetros del juego editando las constantes en `runner.py`:

```python
HEIGHT = 8      # Altura del tablero (filas)
WIDTH = 8       # Ancho del tablero (columnas)
MINES = 8       # Número de minas
```

### Niveles de Dificultad Sugeridos

| Nivel | Dimensiones | Minas | Configuración |
|-------|-------------|-------|---------------|
| Principiante | 8×8 | 8 | `HEIGHT=8, WIDTH=8, MINES=8` |
| Intermedio | 10×10 | 15 | `HEIGHT=10, WIDTH=10, MINES=15` |
| Experto | 12×12 | 25 | `HEIGHT=12, WIDTH=12, MINES=25` |
| Extremo | 16×16 | 40 | `HEIGHT=16, WIDTH=16, MINES=40` |

## 🎓 Conceptos de IA Implementados

### 1. **Representación del Conocimiento**
- Uso de sentencias lógicas para representar información sobre el tablero
- Base de conocimiento dinámica que se actualiza con cada movimiento

### 2. **Inferencia Lógica**
- Deducción de información nueva a partir de conocimiento existente
- Identificación de subconjuntos para generar nuevas sentencias

### 3. **Toma de Decisiones**
- Estrategia determinística: priorizar movimientos seguros
- Estrategia probabilística: movimientos aleatorios cuando no hay certeza

### 4. **Actualización de Creencias**
- Propagación de información a través de todas las sentencias
- Eliminación de información redundante

## 📊 Algoritmo de la IA en Pseudocódigo

```
FUNCIÓN add_knowledge(celda, contador):
    // 1. Marcar movimiento
    moves_made.add(celda)
    mark_safe(celda)
    
    // 2. Crear nueva sentencia con vecinos
    vecinos = obtener_vecinos_no_revelados(celda)
    nueva_sentencia = Sentencia(vecinos, contador)
    knowledge.add(nueva_sentencia)
    
    // 3. Inferir conocimiento
    MIENTRAS haya cambios:
        PARA CADA sentencia EN knowledge:
            SI sentencia.count == 0:
                marcar todas las celdas como seguras
            SI |sentencia.cells| == sentencia.count:
                marcar todas las celdas como minas
        
        // 4. Generar nuevas sentencias por subconjunto
        PARA CADA par (S1, S2) EN knowledge:
            SI S1 ⊂ S2:
                nueva = Sentencia(S2.cells - S1.cells, S2.count - S1.count)
                knowledge.add(nueva)

FUNCIÓN make_safe_move():
    movimientos_seguros = safes - moves_made
    SI movimientos_seguros no está vacío:
        RETORNAR uno aleatorio de movimientos_seguros
    RETORNAR None

FUNCIÓN make_random_move():
    movimientos_posibles = todas_las_celdas - moves_made - mines
    SI movimientos_posibles no está vacío:
        RETORNAR uno aleatorio de movimientos_posibles
    RETORNAR None
```

## 🐛 Solución de Problemas

### El juego no inicia
- Verifica que Pygame está instalado: `pip list | findstr pygame`
- Asegúrate de estar usando Python 3.8+: `python --version`

### La IA no toma decisiones
- Verifica que has presionado el botón "AI Agent"
- Si el tablero es muy difícil, la IA puede necesitar hacer movimientos aleatorios

### Errores de visualización
- Asegúrate de que la carpeta `assets/` existe con todas las imágenes
- Verifica que la fuente OpenSans-Regular.ttf está presente

## 🤝 Contribuciones

¡Las contribuciones son bienvenidas! Algunas ideas para mejorar:

- [ ] Implementar diferentes niveles de dificultad en el menú
- [ ] Agregar contador de tiempo
- [ ] Sistema de puntuación
- [ ] Guardar mejores tiempos
- [ ] Modo oscuro/claro
- [ ] Sonidos y efectos
- [ ] Mejoras en el algoritmo de la IA
- [ ] Visualización del proceso de razonamiento de la IA
- [ ] Modo multijugador

## 📝 Licencia

Este proyecto es de código abierto y está disponible bajo la licencia MIT.

## 👨‍💻 Autor

Desarrollado como proyecto educativo para aprender sobre:
- Desarrollo de juegos con Pygame
- Implementación de algoritmos de IA
- Lógica proposicional
- Sistemas de inferencia

## 🙏 Agradecimientos

- **Pygame** - Por la excelente biblioteca de desarrollo de juegos
- **CS50's Introduction to AI** - Por la inspiración del proyecto
- Comunidad de Python por las herramientas y recursos

---

<div align="center">

**¿Te gustó este proyecto? ¡Dale una ⭐ estrella!**

Hecho con ❤️ y Python

</div>

