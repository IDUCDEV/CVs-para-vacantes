---
name: linkedin-hidden-jobs
description: Busca el "hidden job market" de LinkedIn (posts donde la gente publica vacantes de Flutter/Dart, no avisos oficiales). Filtra remoto/LATAM/español, últimos 3 días. Genera markdown en vacantes-ocultas/.
---

# Skill: linkedin-hidden-jobs

Busca oportunidades laborales publicadas en **posts de LinkedIn** (no en la sección de empleos). Cuando el usuario invoque esta skill, ejecuta TODO el workflow:

1. Buscar en web (`websearch`) las queries definidas
2. Parsear y filtrar resultados
3. Identificar ofertas reales + remoto/LATAM/español
4. Generar archivo markdown
5. Mostrar resultado al usuario
6. Indicar que puede aplicar con `cv-apply`

---

## Queries de búsqueda (ejecutar TODAS)

Usa `websearch` tool con `livecrawl="preferred"` para resultados frescos. Ejecuta cada query con 2-3s de separación:

```
site:linkedin.com/posts flutter hiring remote
site:linkedin.com/posts flutter vacante remoto
site:linkedin.com/posts flutter developer contratando
site:linkedin.com/posts dart developer hiring
site:linkedin.com/posts "flutter" "remote" latam
site:linkedin.com/posts flutter empleo
```

## Filtros (aplicar en orden)

### 1. Validar URL
Solo URLs que empiecen con `linkedin.com/posts/...` o `www.linkedin.com/posts/...`

### 2. Identificar oferta REAL (no artículo)
El snippet debe contener AL MENOS UNA de estas frases:
- `hiring`, `"we're hiring"`, `"we are hiring"`, `"looking for"`, `"job opening"`, `"join our team"`, `"open position"`, `"now hiring"`
- `vacante`, `contratando`, `"estamos buscando"`, `"se busca"`, `oportunidad`, `necesitamos`, `empleo`

### 3. Filtrar remoto/LATAM
El snippet debe contener AL MENOS UNA de:
- `remote`, `remoto`, `remota`, `work from home`, `trabajo desde casa`
- `latam`, `"latin america"`, `latinoamérica`, `worldwide`, `"anywhere"`

### 4. Detectar español
El snippet debe contener palabras en español (artículos, preposiciones, conectores como `el`, `la`, `de`, `en`, `para`, `que`, `con`, `por`, `una`, `los`, `las`, `del`, `se`, `al`, `su`, `más`, `como`, `entre`, `todo`, `desarrollador`, `experiencia`, `equipo`, `busca`, `trabajo`, `remoto`, `años`, `tiempo`, `empresa`, `salario`, `ofrecemos`, `requisitos`, `funciones`, `interesados`, `postular`, `disponibilidad`, `móvil`, `aplicaciones`, `ti`, `ingeniero`)

### 5. Deducir duplicados
Si la misma URL aparece en múltiples queries, mantener solo una ocurrencia.

### 6. Límite temporal
Solo resultados de los últimos 3 días. El `websearch` tool no siempre devuelve fechas exactas. Si no hay fecha visible, incluir el resultado pero confiar en `livecrawl="preferred"` para frescura. Si ves fechas explícitas en el resultado, excluir si son > 3 días.

---

## Output: formato del markdown

```markdown
# Vacantes Ocultas LinkedIn - {fecha}

> 🎯 Búsqueda en posts de LinkedIn · {hora} UTC
> 📍 Remoto LATAM · Últimos 3 días

---

## Resultados ({n})

### 1. {título del post}
**Empresa/Reclutador:** {inferido del snippet}
**Ubicación:** {inferido del snippet}
**📝** {snippet (máx 200 chars)}
**🔗** [{url}]({url})
`[Aplicar con cv-apply]`

### 2. ...
```

---

## Archivo de salida

```
/home/iducdev/Escritorio/curriculums/vacantes-ocultas/{YYYY-MM-DD}-hidden.md
```

Si se invoca varias veces el mismo día, sobrescribe el archivo.

---

## Pipeline post-búsqueda

Cuando el usuario vea la lista y quiera aplicar a una:

1. Usuario pasa el link o descripción
2. Cargar skill `cv-apply`
3. Ejecutar workflow de `cv-apply`
