# PruebaProgramadorBackendCSharp

API REST desarrollada en .NET 8 para gestión de marcas de automóviles.

## Características

- **API REST** con endpoints CRUD para marcas de automóviles
- **Entity Framework Core** con PostgreSQL
- **Pruebas unitarias** con XUnit (>70% cobertura)
- **Docker Compose** para fácil despliegue


## Estructura del Proyecto

```
PruebaProgramadorBackendCSharp/
├── Controllers/           # Controladores de la API
├── Models/               # Entidades del dominio
├── DTOs/                 # Data Transfer Objects
├── Services/             # Lógica de negocio
├── Repositories/         # Acceso a datos
├── Data/                 # Contexto de Entity Framework
├── Migrations/           # Migraciones de base de datos
└── Tests/                # Pruebas unitarias e integración
```

## Endpoints de la API

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| GET | `/api/MarcasAutos` | Obtener todas las marcas |
| GET | `/api/MarcasAutos/{id}` | Obtener marca por ID |
| POST | `/api/MarcasAutos` | Crear nueva marca |
| PUT | `/api/MarcasAutos/{id}` | Actualizar marca existente |
| DELETE | `/api/MarcasAutos/{id}` | Eliminar marca |

## Ejecución con Docker Compose

### Prerequisitos
- Docker
- Docker Compose

### Instrucciones

1. **Clonar el repositorio:**
   ```bash
   git clone https://github.com/Gaitan19/Prueba-Conocimiento-Backend-Gaitan.git
   cd Prueba-Conocimiento-Backend-Gaitan
   ```

2. **Ejecutar con Docker Compose:**
   ```bash
   docker-compose up -d
   ```

3. **Verificar que los servicios estén ejecutándose:**
   ```bash
   docker-compose ps
   ```

4. **Acceder a la API:**
   - URL: `http://localhost:8080`
   - Swagger UI: `http://localhost:8080/swagger`

5. **Verificar la base de datos:**
   - Host: `localhost`
   - Puerto: `5432`
   - Base de datos: `prueba_db`
   - Usuario: `postgres`
   - Contraseña: `19062003kk`

### 🚀 Pasos para Probar Docker

1. **Ubicarse en el directorio raíz del proyecto**
   ```bash
   cd /ruta/al/proyecto/Prueba-Conocimiento-Backend-Gaitan
   ```

2. **Verificar archivos necesarios**
   ```bash
   ls -la
   ```
   Debes ver:
   - `docker-compose.yml`
   - `Dockerfile`
   - `init-scripts/`
   - `PruebaProgramadorBackendCSharp/`

3. **(Opcional) Limpiar contenedores anteriores**
   ```bash
   docker-compose down -v
   docker system prune -f
   ```

4. **Construir y ejecutar los servicios**
   ```bash
   docker-compose up -d --build
   ```
   Esto levantará:
   - `prueba_postgres_db` (PostgreSQL)
   - `prueba_api_rest` (API REST)

5. **Verificar estado de los contenedores**
   ```bash
   docker-compose ps
   ```
   Espera que ambos servicios estén en estado **Up (healthy)**.

6. **Ver logs**
   ```bash
   docker-compose logs api-rest
   docker-compose logs postgres-db
   ```

7. **Probar la API REST**
   - Navegador: [http://localhost:8080/api/MarcasAutos](http://localhost:8080/api/MarcasAutos)
   - o con curl:
     ```bash
     curl -X GET http://localhost:8080/api/MarcasAutos
     ```

8. **Probar Endpoints**
   ```bash
   # Crear nueva marca
   curl -X POST http://localhost:8080/api/MarcasAutos    -H "Content-Type: application/json"    -d '{"nombre":"Toyota","activo":true}'
   ```

9. **Swagger**
   - Navegador: [http://localhost:8080/swagger](http://localhost:8080/swagger)
    

10. **Verificar base de datos**
   ```bash
   docker exec -it prueba_postgres_db psql -U postgres -d prueba_db
   \dt
   SELECT * FROM "MarcasAutos";
   \q
   ```

11. **Health Checks**
    ```bash
    docker inspect prueba_api_rest | grep -A 10 '"Health"'
    docker inspect prueba_postgres_db | grep -A 10 '"Health"'
    ```

---

## Desarrollo Local

### Prerequisitos
- .NET 8 SDK
- PostgreSQL (local o Docker)

### Configuración

1. **Actualizar connection string en `appsettings.Development.json`:**
   ```json
   {
     "ConnectionStrings": {
       "DefaultConnection": "Host=localhost;Port=5432;Database=prueba_db;Username=postgres;Password=your_password"
     }
   }
   ```

2. **Aplicar migraciones:**
   ```bash
   cd PruebaProgramadorBackendCSharp
   dotnet ef database update
   ```

3. **Ejecutar la aplicación:**
   ```bash
   dotnet run
   ```

## Pruebas

### Ejecutar todas las pruebas:
```bash
cd PruebaProgramadorBackendCSharp.Tests
dotnet test
```

### Ejecutar pruebas con cobertura:
```bash
dotnet test /p:CollectCoverage=true /p:CoverletOutputFormat=lcov
```


