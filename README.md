# Agenda Inspecciones Vehiculares — Proyección para TV

Esta es una página HTML estática que muestra la agenda diaria de inspecciones en un televisor. La información se lee desde una hoja de Google Sheets (CSV export).

Archivos en este directorio:
- `index.html` — la página principal personalizada con logo y paleta de colores (negro/rojo/blanco).
- `logo.png` — coloca aquí el logo `Alberto Ochoa & Cia` (no está incluido; pon el archivo proporcionado con este nombre).

Cómo usar

1. Asegúrate de que la hoja de Google Sheets sea accesible públicamente para lectura, o que la opción "Anyone with the link can view" esté activada en Compartir.

2. (Recomendado) Publicar la hoja o usar la export URL CSV.
   - La página ya usa la URL de export CSV construida a partir de tu link:

     https://docs.google.com/spreadsheets/d/1z0JSYJaETDFlsW8cmxn3LO4GFx7HO6sWHdVoDK05qF4/export?format=csv&gid=1863384913

   - Si prefieres usar otra hoja, reemplaza la constante `CSV_URL` en `index.html` por la URL de export CSV correspondiente.

3. Coloca el logo en este mismo directorio con el nombre `logo.png`.

4. Servir la página en la red local (para que el TV pueda abrirla). Desde macOS puedes abrir un terminal y ejecutar desde este directorio:

```bash
# opción rápida con Python 3
python3 -m http.server 8000
```

Luego en el televisor abre el navegador y escribe la IP del ordenador que sirve la página, por ejemplo:

http://192.168.1.42:8000

(Si no conoces la IP local, en macOS puedes verla con `ipconfig getifaddr en0` o revisando Preferencias de Red).

5. La página se refresca automáticamente cada 30 segundos. Usa el selector "Mostrar sólo hoy" para ver únicamente las inspecciones cuya columna FECHA coincida con la fecha actual.

Notas y recomendaciones
- Asegúrate que la primera fila de la hoja contenga encabezados con las columnas (idealmente): `TIPO, FECHA, EMPRESA, VEHICULO, HORA INICIO, HORA FIN, COORDINADOR`.
- Si tu columna FECHA usa formato dd/mm/yyyy o yyyy-mm-dd, el script intentará parsearla correctamente.
- Si la hoja contiene comas dentro de celdas complejas, la simple división CSV usada podría fallar en casos raros; para datos complejos considera exportar como CSV con comillas, o usar un backend que parsee XLSX directamente.

Siguientes pasos (opcional)
- Implementar un backend en Node/Express que reciba un archivo Excel (.xlsx) y haga el parsing robusto (recomendado si el CSV export falla con celdas complejas).
- Añadir control remoto para mensajes/alertas o rotación automática de pantallas.

Si quieres, continuo y:
- Creo un backend Express que acepte subida de XLSX y exponga `/agenda.json`.
- O bien empaqueto esto en una pequeña app (Vite/React) con subida de archivos.

Dime qué prefieres y continúo.