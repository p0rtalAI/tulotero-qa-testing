# TuLotero QA Testing Report

Análisis de calidad realizado sobre la plataforma web y app móvil de TuLotero (tulotero.es).

## Sobre este repositorio

## Criterio de severidades
- **Alta:** Afecta funcionalidad crítica o datos del usuario
- **Media:** Afecta experiencia de usuario de forma notable
- **Baja:** Problema menor que no bloquea el uso

Reporte de bugs encontrados durante un análisis exploratorio de la plataforma, documentados con pasos de reproducción, resultado esperado vs obtenido e impacto.

---

## Bugs encontrados

### BUG-001 · Layout roto con zoom del navegador
- **Severidad:** Media
- **Plataforma:** Web escritorio
- **Pasos:** Abrir tulotero.es → Aumentar zoom al 150% o más
- **Esperado:** La web se adapta correctamente
- **Obtenido:** Los elementos se descolocan y el layout se rompe

<img width="955" height="500" alt="image" src="https://github.com/user-attachments/assets/6e099fbd-378f-4f7e-a3da-1e94d5803672" />
<img width="950" height="491" alt="image" src="https://github.com/user-attachments/assets/f035a9e8-5e7d-4101-9d6c-271bbfdf3b99" />


---

### BUG-002 · Menú desplegable no se cierra al hacer clic fuera
- **Severidad:** Baja-Media
- **Plataforma:** Web escritorio
- **Pasos:** Abrir tulotero.es → Clic en "Sorteos" → Clic fuera del menú
- **Esperado:** El menú se cierra
- **Obtenido:** El menú permanece abierto

 <img width="950" height="1132" alt="image" src="https://github.com/user-attachments/assets/1bfcd4eb-a096-4cdb-99bf-5f0d722346ba" />


---

### BUG-003 · Ausencia de validación de formato estricto en campo email de comentarios
- **Severidad:** Media
- **Plataforma:** Web escritorio y móvil
- **Pasos:** Ir al Blog → Sección comentarios → Introducir email con formato mínimo válido pero dominio inexistente → Publicar
- **Esperado:** El sistema valida que el email tenga un formato estricto y real antes de publicar
- **Obtenido:** El comentario se publica sin validación adicional
- **Impacto:** Permite registros con emails falsos en una plataforma de pagos regulada

<img width="872" height="469" alt="image" src="https://github.com/user-attachments/assets/35f49aac-1947-4923-9719-03bd8dd2b7c1" />


---

### BUG-004 · Imagen de banner no responsive en móvil
- **Severidad:** Media
- **Plataforma:** Web móvil
- **Pasos:** Abrir tulotero.es en móvil o vista móvil del navegador → Observar banner central
- **Esperado:** La imagen se adapta y el texto es legible
- **Obtenido:** La imagen no se ajusta y el texto superpuesto no se puede leer
- **Impacto:** Afecta especialmente a su audiencia principal dado que TuLotero es principalmente una app móvil

<img width="790" height="978" alt="image" src="https://github.com/user-attachments/assets/ab42877a-5c57-470f-8521-dafcb47f2186" />

---

### BUG-005 · Mensaje de error cortado en popup de app móvil
- **Severidad:** Media
- **Plataforma:** App móvil Android
- **Pasos:** Ir a Datos de usuario → Introducir apellido de más de 100 caracteres → Guardar
- **Esperado:** El mensaje de error es legible y completo
- **Obtenido:** El popup corta el texto sin permitir scroll
- **Nota:** En la versión web el mensaje sí se muestra completo. El problema es específico del componente popup en la app móvil

<img width="536" height="1048" alt="image" src="https://github.com/user-attachments/assets/c818fb88-ec94-4d12-b33f-c30ecac28086" />

<img width="955" height="80" alt="image" src="https://github.com/user-attachments/assets/80acef14-b8f9-459a-ac44-716ef43885a7" />

---

### BUG-006 · Límite de caracteres en campo Apellidos cuestionable y truncado sin aviso
- **Severidad:** Media-Alta
- **Plataforma:** App móvil Android
- **Pasos:** Introducir apellido que supere 100 caracteres → Guardar → Observar el campo tras el error
- **Esperado:** El sistema mantiene el valor original para que el usuario pueda corregirlo
- **Obtenido:** El apellido queda truncado automáticamente y se muestra así en el perfil sin informar al usuario
- **Recomendación:** Reducir el límite a 30-40 caracteres, más acorde a la realidad, y validar en frontend antes de llegar al popup
- **Impacto:** El usuario puede guardar datos de identidad incorrectos sin saberlo en una plataforma con verificación KYC

<img width="714" height="325" alt="image" src="https://github.com/user-attachments/assets/921748ce-f3cf-4037-9c91-a8c610fcf8cc" />

---

## Entorno de pruebas

- Navegador: Microsoft Edge 148.0.3967.83 (64 bits)
- Dispositivo móvil: POCO X4 GT (Android)
- Fecha del análisis: Mayo 2025
- Automatización: Python 3.11 · Playwright 1.60 · pytest 9.0.3

## Automatización

Suite de 6 tests con Playwright + Python que cubren smoke testing 
y regresiones de los bugs documentados.

Herramientas: Python 3.11 · Playwright 1.60 · pytest

Ver evidencias en `/automation/evidencias/`
