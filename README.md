# TaskManager2 - Gestor de Tareas Inteligente

## 📋 Descripción

TaskManager2 es una aplicación de línea de comandos para gestionar tareas de forma eficiente. Integra inteligencia artificial (OpenAI GPT) para ayudarte a desglosar tareas complejas en subtareas simples y accionables. 

Es un proyecto práctico desarrollado como parte del Máster en Desarrollo de IA de BigSchool, diseñado para demostrar conceptos fundamentales de desarrollo de software incluyendo programación orientada a objetos, persistencia de datos, integración con APIs externas y testing.

## ✨ Características

- ✅ **Gestión CRUD de tareas**: Crear, listar, completar y eliminar tareas
- 🤖 **Asistencia con IA**: Desglosa tareas complejas en subtareas simples usando GPT-5
- 💾 **Persistencia de datos**: Almacenamiento automático en archivo JSON
- 📊 **Visualización clara**: Muestra el estado de las tareas con iconos (✓ completada)
- 🧪 **Testing completo**: Suite de pruebas unitarias con pytest
- 🎯 **ID automático**: Asignación inteligente de IDs a las tareas
- 🔄 **Sincronización automática**: Guardado automático después de cada operación

## 🛠️ Requisitos Previos

- Python 3.8 o superior
- pip (gestor de paquetes de Python)
- Clave API de OpenAI (para la funcionalidad de IA)

## 📦 Instalación

### 1. Clonar o descargar el proyecto

```bash
git clone <url-del-repositorio>
cd TaskManager2
```

### 2. Crear un entorno virtual (recomendado)

```bash
python -m venv .venv
```

### 3. Activar el entorno virtual

**En Windows:**
```bash
.venv\Scripts\activate
```

**En macOS/Linux:**
```bash
source .venv/bin/activate
```

### 4. Instalar dependencias

```bash
pip install -r requirements.txt
```

### 5. Configurar variables de entorno

Crea un archivo `.env` en la raíz del proyecto con tu clave API de OpenAI:

```env
OPENAI_API_KEY=tu_clave_api_aqui
```

## 🚀 Uso

### Ejecutar la aplicación

```bash
python main.py
```

### Menú de opciones

```
--- Gestor de Tareas Inteligente ---
1. Añadir tarea
2. Añadir tarea compleja (con IA)
3. Listar tareas
4. Completar tarea
5. Eliminar tarea
6. Salir
```

### Ejemplos de uso

#### Ejemplo 1: Añadir una tarea simple
```
Elige una opción: 1
Descripción de la tarea: Comprar leche
Tarea añadida: Comprar leche
```

#### Ejemplo 2: Añadir tarea compleja con IA
```
Elige una opción: 2
Descripción de la tarea compleja: Planificar un viaje a Barcelona
```
La IA desglosa automáticamente en subtareas como:
- Investigar vuelos y reservar
- Buscar y reservar alojamiento
- Planificar itinerario turístico
- Etc.

#### Ejemplo 3: Listar tareas
```
Elige una opción: 3
[✓] #1: Comprar leche
[ ] #2: Investigar vuelos
[ ] #3: Buscar alojamiento
```

#### Ejemplo 4: Completar una tarea
```
Elige una opción: 4
ID de la tarea a completar: 1
Tarea completada: [✓] #1: Comprar leche
```

#### Ejemplo 5: Eliminar una tarea
```
Elige una opción: 5
ID de la tarea a eliminar: 3
Tarea eliminada: #3
```

## 📁 Estructura del Proyecto

```
TaskManager2/
├── main.py                      # Punto de entrada de la aplicación
├── task_manager.py              # Clase TaskManager y Task
├── ai_service.py                # Integración con OpenAI
├── test_task_manager_init.py    # Suite de tests unitarios
├── tasks.json                   # Base de datos de tareas (generado)
├── requirements.txt             # Dependencias del proyecto
├── .env                         # Variables de entorno (no versionar)
├── .gitignore                   # Archivos a ignorar en git
├── pytest.py                    # Configuración de pytest
└── README.md                    # Este archivo
```

## 🧪 Testing

### Ejecutar todos los tests

```bash
pytest
```

### Ejecutar tests con salida detallada

```bash
pytest -v
```

### Ejecutar tests específicos

```bash
pytest test_task_manager_init.py::TestTaskManagerInit::test_init_no_tasks_file_exists -v
```

### Cobertura de tests

```bash
pytest --cov=task_manager test_task_manager_init.py
```

### Suite de Tests Incluida

La suite `test_task_manager_init.py` incluye 6 tests que verifican:

1. ✅ Inicialización sin archivo de tareas existente
2. ✅ Inicialización con archivo JSON vacío
3. ✅ Carga de una única tarea desde archivo
4. ✅ Carga de múltiples tareas desde archivo
5. ✅ Preservación del estado (completada/pendiente) de las tareas
6. ✅ Correcta instanciación de objetos Task

## 🏗️ Arquitectura

### Clases Principales

#### `Task`
Representa una tarea individual con propiedades:
- `id`: Identificador único
- `description`: Descripción de la tarea
- `completed`: Estado de completitud (boolean)

#### `TaskManager`
Gestiona la colección de tareas:
- `add_task()`: Añade una nueva tarea
- `list_tasks()`: Muestra todas las tareas
- `complete_task()`: Marca una tarea como completada
- `delete_task()`: Elimina una tarea
- `load_tasks()`: Carga tareas desde JSON
- `save_tasks()`: Guarda tareas en JSON

### `ai_service`
Módulo que proporciona integración con OpenAI:
- `create_simple_tasks()`: Desglosa tareas complejas en subtareas

## 🤖 Integración con IA

La aplicación utiliza la API de OpenAI para procesar tareas complejas:

- **Modelo**: GPT-5 (o el modelo configurado)
- **Función**: Desglosar tareas en 3-5 subtareas simples y accionables
- **Prompt engineering**: Utiliza prompts optimizados para obtener respuestas estructuradas

## 📊 Flujo de Datos

```
main.py
  ├── TaskManager (gestión de tareas)
  │   └── task_manager.py
  │       ├── Task (modelo de datos)
  │       ├── load_tasks() → tasks.json
  │       └── save_tasks() → tasks.json
  └── ai_service (procesamiento IA)
      └── OpenAI API
```

## 🔐 Seguridad

- **Variables de entorno**: La clave API se carga desde `.env` (nunca se versiona)
- **Archivo .gitignore**: Asegura que `.env` no se suba al repositorio
- **Validación**: La aplicación verifica la existencia de la clave API antes de hacer llamadas

## 📝 Dependencias

Las dependencias se definen en `requirements.txt`:

```
openai>=1.0.0
python-dotenv>=1.0.0
pytest>=7.0.0
pytest-cov>=4.0.0
```

## 🐛 Solución de Problemas

### Error: "OPENAI_API_KEY no está configurada"
- **Solución**: Crea un archivo `.env` con tu clave API

### Error: "Módulo 'openai' no encontrado"
- **Solución**: Ejecuta `pip install -r requirements.txt`

### Las tareas no se guardan
- **Solución**: Verifica que tienes permisos de escritura en el directorio del proyecto

### Tests fallan
- **Solución**: Asegúrate de que pytest está instalado: `pip install pytest`

## 📚 Aprendizajes y Conceptos

Este proyecto demuestra:

- **POO**: Clases, herencia, encapsulación
- **Persistencia**: Lectura/escritura de JSON
- **APIs externas**: Integración con OpenAI
- **Testing**: Pruebas unitarias con pytest
- **Gestión de errores**: Try-except, manejo de excepciones
- **Variables de entorno**: Uso de .env
- **CLI**: Interfaz de línea de comandos

## 🤝 Contribución

Este es un proyecto educativo. Para sugerencias o mejoras:

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📄 Licencia

Este proyecto está bajo la licencia MIT - ver archivo LICENSE para más detalles.

## 👤 Autor

Desarrollado como proyecto práctico del Máster en Desarrollo de IA de BigSchool.

## 📞 Soporte

Para preguntas o problemas, puedes:
- Abrir un Issue en el repositorio
- Consultar la documentación de [OpenAI](https://platform.openai.com/docs)
- Revisar la documentación de [pytest](https://docs.pytest.org/)

## 🔄 Historial de Cambios

### v1.0.0 (Versión Inicial)
- Implementación básica de gestor de tareas
- Integración con OpenAI
- Suite de tests completa
- Documentación README

---

**Última actualización**: 22 de julio de 2026
