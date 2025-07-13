# Proyecto IA: Gestión de Historias de Usuario y Tareas con Azure OpenAI

Este proyecto es una aplicación web desarrollada en Flask que permite gestionar historias de usuario y tareas de manera inteligente, utilizando la API de Azure OpenAI para la generación automática de historias y tareas a partir de prompts en lenguaje natural. Incluye integración con bases de datos SQL, despliegue con Docker y un pipeline CI/CD en Azure DevOps.
---
## Características

- **Generación automática de historias de usuario** a partir de prompts usando Azure OpenAI.
- **Generación automática de tareas técnicas** para cada historia de usuario.
- **Gestión CRUD** de historias de usuario y tareas.
- **Interfaz web moderna** con Bootstrap.
- **Persistencia en base de datos SQL** (MySQL por defecto).
- **Despliegue fácil con Docker y docker-compose**.
- **Pipeline CI/CD** con Azure DevOps.
- **Testing automatizado** con pytest.

## Tecnologías utilizadas

- Python 3.11
- Flask
- SQLAlchemy
- Pydantic
- Jinja2
- Azure OpenAI (API)
- MySQL
- Docker & docker-compose
- Bootstrap 5
---

## Estructura del proyecto

```
.
├── app/
│   ├── db.py
│   ├── models/
│   ├── routes/
│   ├── schemas/
│   ├── services/
│   └── templates/
├── test/
├── run.py
├── create_tables.py
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
└── azure-pipelines.yml
```
---

## Instalación local

1. **Clona el repositorio:**
   ```bash
   git clone https://miguelmorales144@dev.azure.com/miguelmorales144/Entregable5/_git/Entregable5
   ```
2. **Crea un entorno virtual e instala dependencias:**
   ```bash
   python -m venv venv
   venv\Scripts\activate  # En Windows
   # o
   source venv/bin/activate  # En Mac/Linux

   pip install -r requirements.txt
   ```
3. **Configura las variables de entorno:**

   Crea un archivo `.env` en la raíz del proyecto con el siguiente contenido (ajusta los valores según tu entorno):

   ```
   AZURE_OPENAI_API_KEY=tu_clave
   AZURE_OPENAI_ENDPOINT=tu_endpoint
   OPENAI_API_VERSION=2023-05-15
   AZURE_OPENAI_DEPLOYMENT=nombre_del_modelo
   DATABASE_URL=mysql+pymysql://usuario:contraseña@host:puerto/nombre_basedatos
   APP_SECRET_KEY=secretkey
   ```

4. **Crea las tablas de la base de datos:**
   ```bash
   python create_tables.py
   ```

5. **Ejecuta la aplicación:**
   ```bash
   python run.py
   ```
   Accede a [http://localhost:5000/user-stories](http://localhost:5000/user-stories)

---

## Uso

- Ingresa un prompt en la interfaz para generar una historia de usuario.
- Visualiza, elimina o genera tareas técnicas para cada historia.
- Visualiza las tareas asociadas a cada historia de usuario.
---

## Testing

Para ejecutar los tests automatizados en el terminal:
```sh
pytest
```
---
## CI/CD

El proyecto utiliza **Azure Pipelines** para la integración y entrega continua, definido en el archivo `azure-pipelines.yml` en la raíz del repositorio.

### ¿Qué hace el pipeline?

- Se activa automáticamente en cada push a la rama `main`.
- Se ejecutan los test
- Construye la imagen Docker de la aplicación usando el archivo `Dockerfile`.
- Publica la imagen en Azure Container Registry (ACR).
- Despliega la imagen en Azure Container Apps, actualizando la aplicación con la nueva versión.
- Durante el despliegue, configura todas las variables de entorno necesarias (claves, credenciales, endpoints, etc.) de forma segura usando los secretos definidos en Azure Pipelines.

### Estructura del pipeline
1. **Run Tests:**  
   - Se ejecutan los test.

2. **BuildAndPush:**  
   - Construye la imagen Docker.
   - La sube al Azure Container Registry configurado.

3. **DeployToContainerApp:**  
   - Despliega la imagen recién construida en Azure Container Apps.
   - Pasa las variables de entorno necesarias para el funcionamiento de la aplicación.

### Variables y secretos

Las variables sensibles (como claves de API, credenciales de base de datos, etc.) se gestionan de forma segura mediante las **variables y secretos** de Azure Pipelines y no se incluyen en el código fuente.

**Autor:** Miguel Morales Pareja


