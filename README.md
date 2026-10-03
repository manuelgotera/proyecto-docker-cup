# Proyecto Docker Cup: Configuración de Entornos Dev y QA

Este repositorio contiene la arquitectura de microservicios requerida para la actividad. La solución despliega dos entornos independientes (Dev y QA), implementando aislamiento de red por capas y políticas de réplicas para el escalado de instancias.

---

## Arquitectura y Componentes

La infraestructura está dividida en dos entornos principales con la siguiente asignación de nombres, imágenes y puertos:

### Entorno Dev
- Frontend (web-dev): Basado en Nginx, expuesto en el puerto 4001:80.
- Backend (api-dev): Basado en Node.js, expuesto en el puerto 4002:3000.
- Base de Datos (bd-dev): Instancia de PostgreSQL, expuesta en el puerto 4003:5432.

### Entorno QA
- Frontend (web-qa): Basado en Nginx, expuesto en el puerto 5001:80.
- Backend (api-qa): Basado en Node.js, expuesto en el puerto 5002:3000.
- Base de Datos (bd-qa): Instancia de PostgreSQL, expuesta en el puerto 5003:5432.

---

## Segmentación de Redes

Para cumplir con las políticas de comunicación entre contenedores, se configuraron redes aisladas en cada entorno:

- Red Frontend (red-frontend-dev / red-frontend-qa): Permite únicamente el tráfico entre el contenedor de Frontend y la API Backend.
- Red Backend (red-backend-dev / red-backend-qa): Permite únicamente la comunicación entre la API Backend y la Base de Datos.

De esta manera, el Frontend no tiene acceso directo a la Base de Datos en ningún entorno.

---

## Escalado de Instancias

Siguiendo las especificaciones de escalado para las capas de Frontend y Backend, se definieron réplicas diferenciadas entre entornos mediante la directiva deploy:

- Dev: 2 instancias para el Frontend (web-dev) y 4 instancias para la API (api-dev).
- QA: 4 instancias para el Frontend (web-qa) y 4 instancias para la API (api-qa).

---

```bash
git clone [https://github.com/manuelgotera/proyecto-docker-cup.git](https://github.com/manuelgotera/proyecto-docker-cup.git)
cd proyecto-docker-cup