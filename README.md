# Currículum Isaac Urdaneta

Sistema de gestión de currículum vitae personalizable para aplicaciones a diferentes vacantes.

## Estructura

```
.
├── isaac-urdaneta-base.md    # Plantilla base con información completa
├── CV_Isaac_Urdaneta_ES.md   # Versión en español (lista para usar)
├── CV_Isaac_Urdaneta_EN.md   # English version (ready to use)
├── Isaac Urdaneta CV - Español.pdf
└── Isaac Urdaneta CV - English.pdf
```

## Cómo usar

### 1. Para una vacante específica

1. Copia `isaac-urdaneta-base.md`
2. Personaliza según los requisitos de la vacante:
   - Resalta habilidades relevantes
   - Reordena proyectos según impacto
   - Ajusta el resumen profesional
3. Guarda como `CV_VACANTE.md`

### 2. Generar PDF

```bash
# Instalar pandoc si no lo tienes
sudo apt install pandoc

# Convertir a PDF
pandoc CV_Isaac_Urdaneta_ES.md -o "Isaac_Urdaneta_CV.pdf"
```

### 3. Enmascarar información sensible

Si necesitas ocultar datos (ej.email, LinkedIn), busca y reemplaza en `isaac-urdaneta-base.md`:
- `urdanetacuarteisaacdavid@gmail.com` → `[EMAIL]`
- `linkedin.com/in/isaac-urdaneta` → `[LINKEDIN]`

## Tips de personalización

| Tipo de vacante | Qué destacar |
|-----------------|---------------|
| Flutter Senior | Clean Architecture, BLoC, Supabase |
| Frontend React | TypeScript, SSR, optimización |
| Full Stack | Backend + móvil + DevOps |
| Startup | Versatilidad, velocidad de entrega |

## Contacto

Para preguntas sobre este CV: urdanetacuarteisaacdavid@gmail.com
