# Academic ERP — Agenda escolar digital en Odoo 17

Módulo de **Odoo 17** que funciona como una **agenda escolar digital**: el colegio publica avisos (tareas, exámenes, eventos y comunicados) para un curso y los envía a padres, estudiantes o profesores. Cada destinatario recibe el aviso en Odoo, y el colegio puede ver quién lo recibió y quién lo leyó. Los avisos también aparecen en un calendario.

> Proyecto académico — Ingeniería de Software I, segundo parcial, UAGRM (2024).
> Autores: Dariana, Fabio y Lussiana.

## Funcionalidades

- **Cursos** por nivel (primaria / secundaria) y paralelo (A / B), con su profesor y sus materias.
- **Estudiantes**, **padres** y **profesores**, cada uno vinculado a un usuario de Odoo.
- **Materias** asignadas a cursos y profesores.
- **Avisos** de cuatro tipos: tarea, evento, examen y comunicado.
  - Dirigidos a padres, estudiantes o profesores de un curso.
  - Archivos adjuntos: documentos, audio, video o enlaces.
  - Al crear un aviso, el sistema genera automáticamente un registro por cada destinatario y publica el mensaje en el chat del aviso.
- **Seguimiento de lectura** por destinatario: no recibido, recibido, no leído y leído.
- **Agenda**: vista de calendario con los avisos.
- **Mis avisos**: cada usuario ve solo los avisos que le corresponden.
- **Roles de seguridad**: estudiante, padre, profesor y administrador académico.

## Tecnologías

- Odoo 17 (Python + XML)
- Módulos de Odoo: `base`, `calendar`, `mail`, `website`
- PostgreSQL 14
- Docker Compose

## Estructura

```
docker-compose.yaml             # Odoo 17 + PostgreSQL 14
config_odoo/odoo.conf           # Configuración de Odoo (puerto 8070)
dev_addons/academic_erp/
├── __manifest__.py
├── models/
│   ├── course.py               # Cursos
│   ├── student.py              # Estudiantes
│   ├── parent.py               # Padres
│   ├── teacher.py              # Profesores
│   ├── subject.py              # Materias
│   ├── notice.py               # Avisos
│   ├── notice_attachment.py    # Adjuntos de los avisos
│   └── notice_recipient.py     # Estado de lectura por destinatario
├── security/                   # Grupos y permisos de acceso
└── views/                      # Formularios, listas, calendario y menús
```

## Requisitos

- Docker Desktop

## Cómo ejecutar

```bash
docker compose up -d
```

1. Abrir `http://localhost:8070` y crear una base de datos.
2. Activar el **modo desarrollador** (Ajustes → Activar el modo de desarrollador).
3. Ir a **Aplicaciones → Actualizar lista de aplicaciones**.
4. Buscar **Academic ERP** e instalarlo.
5. Crear usuarios y asignarles el grupo correspondiente: *Student*, *Parent*, *Teacher* o *Academic Admin*.

PostgreSQL queda expuesto en el puerto `5430` del host.

## Menú del módulo

| Menú | Contenido |
|---|---|
| Courses | Cursos |
| Students | Estudiantes |
| Parents | Padres |
| Teachers | Profesores |
| Subjects | Materias |
| Agenda | Calendario de avisos |
| Notices | Todos los avisos |
| My Notices | Avisos del usuario actual |
