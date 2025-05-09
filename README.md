# 🛑 Problema SEO: Etiquetas Canónicas Duplicadas en PDP (Product Detail Pages)

## 🧩 Descripción del Problema

Durante la auditoría técnica del sitio **[cyamoda.com](https://www.cyamoda.com)** se detectó que múltiples páginas de producto (PDP) incluyen **etiquetas canónicas duplicadas o inconsistentes** dentro del mismo documento HTML, lo cual afecta negativamente la indexación de URLs en buscadores.

---

## 📍 Ejemplo Identificado

**URL afectada:**  
`https://www.cyamoda.com/playera-tank-slim/3104446.html`

**Código encontrado en `<head>`:**

```html
<link rel="canonical" href="https://www.cyamoda.com/playera-tank-slim/3104446.html" />
<!-- Más adelante, duplicado o diferente canonical por JavaScript u otro template -->
<link rel="canonical" href="https://www.cyamoda.com/3104446.html" />

--------------

## ⚠️ Impacto SEO

- Google puede **ignorar ambas etiquetas canónicas** al detectar conflicto.
- Puede provocar **indexación de URLs incorrectas** o sin parámetros UTM eliminados.
- Aumenta el riesgo de **contenido duplicado interno**.
- Reduce la **autoridad concentrada** en la URL preferida.

---

## 🔍 Posibles Causas

| Causa                                       | Descripción                                                                                  |
|--------------------------------------------|----------------------------------------------------------------------------------------------|
| Plantillas con canonicals hardcodeados     | Algunas PDP usan duplicación de `<link rel="canonical">` por conflicto entre templates.      |
| Scripts externos que modifican el DOM      | Herramientas como Yotpo o Visual Website Optimizer pueden inyectar canonical alternas.       |
| Duplicidad por parámetros (`?pid=`, `?dwvar_`) | Google puede ver como duplicado si no se unifican correctamente.                            |

---

## ✅ Recomendaciones

1. **Unificar generación del canonical a nivel backend (Demandware / SFCC):**

    ```html
    <link rel="canonical" href="https://www.cyamoda.com/playera-tank-slim/3104446.html" />
    ```

    Asegurarse que **solo se renderice una vez por producto**.

2. **Bloquear canonicals en JavaScript:**

    - Verificar si librerías como **Yotpo**, **VWO** o **GTM** están inyectando duplicados.
    - Auditar el **DOM final** (con JS habilitado) en Lighthouse o DevTools.

3. **Canonicalizar la versión sin parámetros:**

    - Si existen múltiples variantes de URL (`?pid=`, `?dwvar_`), declarar como canónica la **URL amigable sin parámetros**.

4. **Test A/B antes de aplicar en todo el catálogo:**

    - Realizar prueba con **3 productos** antes de aplicar la solución completa.

---

## 🧪 Verificación Técnica

- Usar el comando en Google:  
  `site:cyamoda.com inurl:3104446`  
  Para validar si Google ha indexado duplicados.

- Herramientas recomendadas:
  - [Screaming Frog SEO Spider](https://www.screamingfrog.co.uk/seo-spider/)
  - [Sitebulb](https://sitebulb.com/)
  - [Ahrefs](https://ahrefs.com/) (para problemas de canonical duplicado)

---

## 📌 Estado Recomendado del HTML

```html
<head>
  ...
  <link rel="canonical" href="https://www.cyamoda.com/playera-tank-slim/3104446.html" />
  <!-- Ninguna otra etiqueta canonical debe aparecer -->
</head>


----------------

## 🧠 Conclusión

Resolver este problema es **prioridad alta**, ya que afecta directamente la correcta **consolidación de autoridad de página** y puede **diluir señales SEO**.  
Esta corrección debe realizarse **antes de nuevas campañas o lanzamientos de temporada** para asegurar una **indexación óptima** y una **experiencia consistente** para los motores de búsqueda.
