# Guía de Skills para Búsqueda de Empleo

## Skills disponibles

| # | Skill | Propósito | Tipo | Invocación |
|---|-------|-----------|------|------------|
| 1 | **job-search** | Busca vacantes Flutter/Dart en 7 fuentes (LinkedIn, GetOnBoard, Himalayas, RemoteJobs, Career Nest, Jobicy, Computrabajo) | Script Python | `python3 $OPENCODE_SKILLS/job-search/job_search.py` |
| 2 | **linkedin-hidden-jobs** | Busca el "hidden job market" de LinkedIn: posts donde la gente publica vacantes, no avisos oficiales | AI guiada (websearch) | Cargar la skill → el AI ejecuta las queries |
| 3 | **cv-apply** | Genera CV optimizado ATS + carta de presentación + PDF a partir de una descripción de vacante | AI guiada | Cargar la skill → pegar descripción |
| 4 | **linkedin-outreach** | Genera mensaje personalizado para contactar reclutadores en LinkedIn | AI guiada | Cargar la skill → pegar URL de perfil |

---

## 1. job-search — Buscador de vacantes

**Archivos:** `job-search/SKILL.md`, `job-search/job_search.py`

```bash
python3 /home/iducdev/.opencode/skills/job-search/job_search.py
```

### Qué hace
- Fetch automático a 7 fuentes con paginación
- Filtra por Flutter/Dart, remoto, LATAM (≤24h LinkedIn)
- Deduplica por empresa + título normalizado
- Normaliza salarios a USD/mes
- Genera markdown con secciones por fuente

### Output
```
vacantes/{YYYY-MM-DD}.md
```

### Fuentes consultadas
| Fuente | API/Formato | Paginación | Autenticación |
|--------|-------------|------------|---------------|
| LinkedIn | Guest HTML | 3 páginas (start=0,10,20) | No |
| GetOnBoard | JSON pública | 1 página | No |
| Himalayas | JSON pública | 3 páginas (offset=0,20,40) | No |
| RemoteJobs.org | JSON pública | 1 página | No |
| Career Nest | JSON pública | Fallback silencioso (inestable) | No |
| Jobicy | JSON pública | Tags flutter + mobile | No |
| Computrabajo | JSON-LD + páginas individuales (VE, MX, CO, AR, CL, PE, EC) | 1 página por país | No |

### Filtros
- **Tecnología:** Flutter o Dart en título (o primeros 300 chars de descripción)
- **Ubicación:** LATAM o worldwide con `locationRestrictions` vacío
- **Modalidad:** Remoto (VE: todas las modalidades)
- **Deduplicación:** `normalize_company()` + `normalize_title()`

---

## 2. linkedin-hidden-jobs — Mercado laboral oculto

**Archivos:** `linkedin-hidden-jobs/SKILL.md`

No tiene script propio. Usa el `websearch` tool del agente.

### Queries que ejecuta el AI

```
site:linkedin.com/posts flutter hiring remote
site:linkedin.com/posts flutter vacante remoto
site:linkedin.com/posts flutter developer contratando
site:linkedin.com/posts dart developer hiring
site:linkedin.com/posts "flutter" "remote" latam
site:linkedin.com/posts flutter empleo
```

### Filtros (aplica el AI automáticamente)
1. **URL válida:** solo `linkedin.com/posts/...`
2. **Oferta real:** snippet contiene `hiring`, `vacante`, `contratando`, etc.
3. **Remoto/LATAM:** `remote`, `remoto`, `latam`, `worldwide`
4. **Español:** detección por palabras clave en snippet
5. **Dedup:** misma URL una sola vez
6. **Temporal:** últimos 3 días

### Output
```
vacantes-ocultas/{YYYY-MM-DD}-hidden.md
```

---

## 3. cv-apply — CV optimizado ATS

**Archivos:** `cv-apply/SKILL.md`

### Workflow

1. **Análisis de la vacante** — extrae requisitos técnicos, funcionales y keywords ATS
2. **Decisión** — mapea contra CV base con pesos (Flutter core 40%, backend 15%, experiencia 15%, ubicación 15%, inglés 10%, otros 5%)
3. **Match ≥ 60% y Flutter core** → genera CV optimizado
4. **CV optimizado** — reescribe resumen, habilidades, experiencia y proyectos alineados a la vacante
5. **Carta de presentación** — texto plano, mismo idioma de la vacante
6. **PDF** — `pandoc` con `Liberation Sans`, márgenes 1in

### Archivos base
- `isaac-urdaneta-base.md` — CV base (nunca se modifica)
- `cv-ats-prompt.md` — reglas ATS

### Output
```
{isaac-urdaneta-base}-{rol}-{empresa}.md
{isaac-urdaneta-base}-{rol}-{empresa}.pdf
```

### Dependencias
- `pandoc` instalado en el sistema
- Fuente `Liberation Sans` disponible

---

## 4. linkedin-outreach — Mensajes para LinkedIn

**Archivos:** `linkedin-outreach/SKILL.md`

### Workflow

1. Lee CV base (`isaac-urdaneta-base.md`)
2. Busca info pública del perfil con `websearch`
3. Pregunta tono: **Directo y natural** (recomendado), **Profesional formal**, o **Casual/amistoso**
4. Genera mensaje personalizado con nombre, empresa y stack
5. Guarda en archivo y muestra para copiar

### Output
```
mensajes-outreach/{nombre-normalizado}-{YYYY-MM-DD}.md
```

---

## Respaldo y restauración

### Backup automático
Las skills están respaldadas en:
```
skills-backup/
├── cv-apply/SKILL.md
├── job-search/SKILL.md
├── job-search/job_search.py
├── linkedin-hidden-jobs/SKILL.md
└── linkedin-outreach/SKILL.md
```

### Cómo restaurar (ej: después de formatear)

```bash
# 1. Clonar el proyecto
git clone <repo> ~/curriculums

# 2. Copiar skills de vuelta al directorio de opencode
cp -r ~/curriculums/skills-backup/* ~/.opencode/skills/

# 3. Verificar
ls ~/.opencode/skills/
# Debería mostrar: cv-apply/  job-search/  linkedin-hidden-jobs/  linkedin-outreach/
```

### Dependencias externas a reinstalar
| Dependencia | Para | Instalación |
|-------------|------|-------------|
| `pandoc` | cv-apply (PDF) | `sudo apt install pandoc` |
| `Liberation Sans` | cv-apply (PDF) | `sudo apt install fonts-liberation` |
| Python 3 | job-search | `python3` (viene con Ubuntu) |

---

## Pipeline completo (flujo recomendado)

```
1. job-search              → Buscar vacantes (diario)
2. linkedin-hidden-jobs    → Buscar posts ocultos (diario)
3. linkedin-outreach       → Contactar reclutadores (cuando haya un perfil relevante)
4. cv-apply                → Aplicar a vacante específica (cuando se decida aplicar)
```
