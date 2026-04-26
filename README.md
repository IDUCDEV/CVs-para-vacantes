# Currículum Isaac Urdaneta

Sistema de gestión de currículum vitae personalizable para aplicaciones a diferentes vacantes,
con optimización para pasar filtros ATS (Applicant Tracking Systems).

## Estructura

```
.
├── isaac-urdaneta-base.md    # Plantilla base con información completa
├── cv-ats-prompt.md         # Prompt detallado para generar CVs ATS
├── CV_Isaac_Urdaneta_ES.md   # Versión en español (lista para usar)
├── CV_Isaac_Urdaneta_EN.md  # English version (ready to use)
├── Isaac Urdaneta CV - Español.pdf
└── Isaac Urdaneta CV - English.pdf
```

## Modo de Uso

### Paso 1: Proporcionar Vacante

Comparte la descripción completa de la vacante/puesto al que quieres aplicar.

### Paso 2: Generar CV Adaptado

Yo uso el prompt `cv-ats-prompt.md` para:
1. Analizar los requisitos de la vacante
2. Extraer keywords técnicos y funcionales
3. Mapear tu experiencia con los requisitos
4. Reescribir el CV optimizado para ATS
5. Generar archivo `.md` y `.pdf`

### Paso 3: Recibir Resultado

Obtienes:
- `isaac-urdaneta-{Rol/especialidad}-{empresa}.md` - CV en markdown
- `isaac-urdaneta-{Rol/especialidad}-{empresa}.pdf` - PDF listo para enviar

---

## Generación Manual (sin asistencia)

### 1. Análisis de Vacante

Extrae manualmente los requisitos:

| Categoría | Ejemplo |
|-----------|---------|
| Técnicos | Flutter, Dart, Clean Architecture, BLoC, APIs REST |
| Funcionales | Desarrollo móvil, publicación en Stores |
| Blandos | Trabajo en equipo, autonomía |
| Modalidad | Remoto / Híbrido / Presencial |

### 2. Optimización ATS

**Keywords obligatorios** (busca y menciona todos):
- Tecnologías requeridas en la vacante
- Años de experiencia
- Modalidad de trabajo

**Formato ATS-Safe**:
```
✓ Headers simples: ## Título
✓ Listas con guiones - o bullets •
✓ Texto plano sin tablas
✗ Sin imágenes
✗ Sin columnas
✗ Sin footnotes
```

### 3. Plantilla de Resumen

```markdown
## Perfil Profesional

[TÍTULO] con [AÑOS] años de experiencia en [TECNOLOGÍAS PRINCIPALES].
Especializado en [ARQUITECTURA/PATRONES]. Experiencia en [REQUISITOS CLAVE].
Capacidad para [RESPONSABILIDADES]. Modalidad: [REMOTO/HÍBRIDO].
```

### 4. Generar PDF

```bash
# Usar pandoc instalado
pandoc input.md -o output.pdf \
  -V mainfont="Helvetica" \
  -V fontsize=11 \
  -V geometry=margin=1in \
  --standalone
```

---

## Tips de Personalización

| Tipo de Vacante | Qué Destacar |
|-----------------|--------------|
| Flutter Senior | Clean Architecture, BLoC, Supabase, Publicación Stores |
| Frontend React | TypeScript, SSR, optimización, Lighthouse |
| Full Stack | Backend + Móvil + DevOps |
| Startup | Versatilidad, velocidad de entrega |

---

## Enmascarar Información

Si necesitas ocultar datos (ej. email, LinkedIn), busca y reemplaza en `isaac-urdaneta-base.md`:
- `urdanetacuarteisaacdavid@gmail.com` → `[EMAIL]`
- `linkedin.com/in/isaac-urdaneta` → `[LINKEDIN]`

---

## Optimización ATS - Checklist

Antes de enviar, verifica:

- [ ] Keywords de la vacante incluidos en el CV
- [ ] Años de experiencia reflejados
- [ ] Modalidad de trabajo especificada
- [ ] Sin información inconsistente
- [ ] Formato ATS-safe (sin tablas/imágenes)
- [ ] Densidad de keywords: 3-5%

---

## Contacto

Para preguntas sobre este CV: urdanetacuarteisaacdavid@gmail.com