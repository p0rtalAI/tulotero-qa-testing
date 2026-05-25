# TuLotero QA Testing Report

Análisis de calidad realizado sobre la plataforma web y app móvil de TuLotero (tulotero.es).

## Sobre este repositorio

Reporte de bugs encontrados durante un análisis exploratorio de la plataforma, documentados con pasos de reproducción, resultado esperado vs obtenido e impacto.

---

## Bugs encontrados

### BUG-001 · Layout roto con zoom del navegador
- **Severidad:** Media
- **Plataforma:** Web escritorio
- **Pasos:** Abrir tulotero.es → Aumentar zoom al 150% o más
- **Esperado:** La web se adapta correctamente
- **Obtenido:** Los elementos se descolocan y el layout se rompe

---

### BUG-002 · Menú desplegable no se cierra al hacer clic fuera
- **Severidad:** Baja-Media
- **Plataforma:** Web escritorio
- **Pasos:** Abrir tulotero.es → Clic en "Sorteos" → Clic fuera del menú
- **Esperado:** El menú se cierra
- **Obtenido:** El menú permanece abierto

---

### BUG-003 · Validación de email insuficiente en formulario de comentarios
- **Severidad:** Media
- **Plataforma:** Web escritorio y móvil
- **Pasos:** Ir al Blog → Sección comentarios → Introducir email con formato mínimo válido pero dominio inexistente → Publicar
- **Esperado:** El sistema rechaza emails no verificables
- **Obtenido:** El comentario se publica sin validación adicional
- **Impacto:** Permite registros con emails falsos en una plataforma de pagos regulada

---

### BUG-004 · Imagen de banner no responsive en móvil
- **Severidad:** Media
- **Plataforma:** Web móvil
- **Pasos:** Abrir tulotero.es en móvil o vista móvil del navegador → Observar banner central
- **Esperado:** La imagen se adapta y el texto es legible
- **Obtenido:** La imagen no se ajusta y el texto superpuesto no se puede leer
- **Impacto:** Afecta especialmente a su audiencia principal dado que TuLotero es principalmente una app móvil

---

### BUG-005 · Mensaje de error cortado en popup de app móvil
- **Severidad:** Media
- **Plataforma:** App móvil Android
- **Pasos:** Ir a Datos de usuario → Introducir apellido de más de 100 caracteres → Guardar
- **Esperado:** El mensaje de error es legible y completo
- **Obtenido:** El popup corta el texto sin permitir scroll
- **Nota:** En la versión web el mensaje sí se muestra completo. El problema es específico del componente popup en la app móvil

---

### BUG-006 · Límite de caracteres en campo Apellidos cuestionable y truncado sin aviso
- **Severidad:** Media-Alta
- **Plataforma:** App móvil Android
- **Pasos:** Introducir apellido que supere 100 caracteres → Guardar → Observar el campo tras el error
- **Esperado:** El sistema mantiene el valor original para que el usuario pueda corregirlo
- **Obtenido:** El apellido queda truncado automáticamente y se muestra así en el perfil sin informar al usuario
- **Recomendación:** Reducir el límite a 30-40 caracteres, más acorde a la realidad, y validar en frontend antes de llegar al popup
- **Impacto:** El usuario puede guardar datos de identidad incorrectos sin saberlo en una plataforma con verificación KYC

---

## Entorno de pruebas
- Navegador: Chrome escritorio
- Dispositivo móvil: Android
- Fecha del análisis: Mayo 2025
