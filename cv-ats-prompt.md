# PROMPT PARA GENERAR CVs OPTIMIZADOS ATS

## INPUT RECIBIDO

- **CV Base:** `isaac-urdaneta-base.md`
- **Vacante:** [Descripción completa del puesto/vacante]

---

## INSTRUCCIONES DE GENERACIÓN

### 1. ANÁLISIS DE LA VACANTE

Extrae y categoriza:

**Requisitos Técnicos:**
- Frameworks y lenguajes mencionados
- Herramientas y tecnologías requeridas
- Experiencia mínima (años)
- Certificaciones necesarias

**Requisitos Funcionales:**
- Responsabilidades clave (verbos de acción)
- Modalidad de trabajo (remoto/híbrido/presencial)
- Ubicación
- Idiomas

**Palabras Clave ATS:**
Lista todas las palabras técnicas y funcionales que aparezcan en la vacante.

---

### 2. MAPEO CV BASE vs VACANTE

Para cada requisito de la vacante:
- ✓ Coincide directamente → mantener
- ⚠ Coincide parcialmente → adaptar descripción
- ✗ No mentioned → agregar si es relevante o incluir como "conocimiento"
- ✗ No aplica → omitir

---

### 3. REESCRITURA OPTIMIZADA

**Resumen Profesional:**
- Reescribir para enfatizar requisitos de la vacante
- Incluir keywords principales en primeras 2 líneas
- Mencionar años de experiencia específicos
- Incluir modalidad de trabajo

**Habilidades Técnicas:**
- Reordenar: primero las requeridas en la vacante
- Agregar las que falten pero dominadas
- Usar formato: "Tecnología - Uso/Aplicación"

**Experiencia Profesional:**
- Para cada puesto: reescribir bullet points
- Resaltar achievements alineados con vacante
- Incluir métricas si son relevantes al puesto
- Usar verbos de acción  (desarrollé, implementé, lideré, optimicé, etc.)

**Proyectos:**
- Seleccionar los más relevantes a la vacante
- Reescribir para enfatizar habilidades requeridas

---

### 4. OPTIMIZACIÓN ATS

**Keywords:**
- Incluir TODAS las palabras clave de la vacante
- Density: 3-5% del contenido total
- Evitar sinónimos que ATS no reconozca

**Formato ATS-Safe:**
- ❌ No headers complejos
- ❌ No tablas
- ❌ No columnas
- ❌ No imágenes
- ✓ Headers simples: ## or ===
- ✓ Listas con guiones o bullets simples
- ✓ Texto plano, sin footnotes

**Estructura Recomendada:**

```
# [NOMBRE] - [TÍTULO/PUESTO]

## Datos de Contacto
[Info de contacto en una línea]

## Perfil Profesional
[Párrafo de 3-5 líneas optimizado con keywords]

## Habilidades Técnicas
[Lista categorizada]

## Experiencia Profesional
[Sin fechas detalladas en headers]

## Proyectos Destacados
[Si aplica]

## Educación
[Solo lo esencial]

## Referencias
[Nota simple]
```

---

### 5. GENERACIÓN DEL OUTPUT

**Archivo de salida:** `{nombre-base}-{Rol/especialidad}-{empresa}.md`

En markdown limpio, optimizado para parseo ATS.

*Idioma:** Español profesional (o según idioma de vacante)

---

## EJEMPLO DE APLICACIÓN

**Input Vacante Stefanini:**
- Desarrollador Flutter Senior
- Remoto
- Clean Architecture, BLoC, APIs REST
- Publicación en Stores

**Output Generado:**
- Título: "Desarrollador Flutter Senior"
- Resumen: Incluir keywords Flutter, Clean Architecture, BLoC, APIs REST, publicación Stores
- Skills: Reordenar Clean Architecture, BLoC antes que otras tecnologías
- Experiencia: Enfatizar publicación en Stores, arquitectura escalable

---

## USO DEL PROMPT

1. Leer CV base de `isaac-urdaneta-base.md`
2. Leer descripción de vacante proporcionada
3. Ejecutar instrucciones 1-5
4. Guardar output como nuevo archivo markdown
5. Convertir a PDF usando Pandoc:

```bash
pandoc input.md -o output.pdf \
  -V mainfont="sans-serif" \
  -V fontsize=11 \
  -V geometry=margin=1in \
  --standalone
```

---

## CRITERIOS DE CALIDAD

- [ ] Coincidencia de keywords ≥ 80%
- [ ] Años de experiencia reflejados correctamente
- [ ] Modalidad de trabajo especificada
- [ ] Sin información inconsistente con CV base
- [ ] Formato ATS-safe verificado
- [ ] Archivo genera PDF correctamente
