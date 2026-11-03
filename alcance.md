**Enlace al programa:** [https://www.mercadolibre.com](https://www.mercadolibre.com/)
https://hackerone.com/mercadolibre/policy_scopes

**Fecha de consulta:** 03/11/2026

### 1. Qué está dentro y fuera del alcance

**Dentro, con recompensa Tier 1:**

- **Apps:** Mercado Pago (Android e iOS), Mercado Libre (Android e iOS), Mercado Envíos Flex, Mercado Envíos Extra y Mercado Envíos Logistics.
- **APIs:** `api.mercadopago.com` y `api.mercadolibre.com`.
- **Hardware:** Point Smart (MLA y MLB).
- **Wildcards:** `*.adminml.com`, `*.mercadolibre.com` y `*.mercadolibre.{cl, com.ar, com.co, com.mx, com.pe, com.uy}`. También `*.mercadolivre.com.br` y `*.mercadopago.{com, cl, com.ar, com.br, com.co, com.mx, com.pe, com.uy}`.
- **Otros:** los paths `/crypto/*` de mercadopago.com.mx, .cl y .com.br, y el asset “Leaked Credentials” (credenciales de fuentes públicas, severidad máxima high).

**Dentro, con recompensa Tier 2:**

- `*.mlstatic.com` y `logistica.redelcom.cl`.
- `www.mercadolibre.{co.cr, com.bo, com.do, com.ec, com.gt, com.hn, com.ni, com.pa, com.py, com.sv}`, `www.mercadolivre.com` y `www.mercadopago.com.ec`.
- `mercadopago.com.ve`, `mpago.li`, `mpago.la` y `mercadobackoffice.com`.
- `biolibre.{ar, cl, co, mx}`, `biolivre.com.br`, `meliplay.com.{ar, pe, uy}`, los `mercadoplay.*`, `portalinmobiliario.{cl, com}`, `tucarro.com`, `tucarro.com.co` y `tumoto.com`.
- `furycloud.io` y `furydocs.io` (marcados “Exposed in ZT”), `sustentabilidadmercadolibre.com` y la app Android `com.mercadolibre.android.mplay_tv`.

**Tier 3 (asset “Tier 3”):** hallazgos no aplicativos, como credenciales filtradas en repos públicos, documentos expuestos o buckets mal configurados.

- Deben estar demostrablemente vinculados a Mercado Libre.
- No se puede ir más allá de confirmar que existen. Vale una única llamada no destructiva para validar una credencial.
- Se paga una recompensa por fuente, de $75 a $1.000.
- No se aceptan reportes de usuarios integradores (desarrolladores externos).

**Se acepta el reporte pero sin recompensa:**

- `mercadoenvios.com.ve`, `www.ipbooster.com`, `*.tucarro.com.ve` y `*.mercadolibre.com.ve`.
- `mercadolibreexperience.com.*`, `mercadolivreexperience.mercadolivre.com.br`, `*.modoblack.mercadolivre.com.br` y `fullbarhomologa.modoblackfullbar.com.br`.
- Fallos en el SDK de integraciones de MercadoPago y en sus secure inputs: dan solo puntos de reputación.

**Fuera de alcance:**

- **Assets:** todo Kangu (`*.kangu.com.br`, `*.gokangu.{cl, co, mx, uy}`, `*.kangu.tech`), `developersforum.*`, `wow-int.mercadolibre.com` y cualquier otro asset de Redelcom (salvo `logistica.redelcom.cl`). También cualquier dominio `.cn`.
- **Funcionalidades:** Melidolar y Collaborators.
- **Tipos de fallo:**
    - KYC (acciones no monetarias sin pasar la validación de identidad).
    - DoS por GraphQL.
    - Los “Core Ineligible Findings” de HackerOne.
    - Dependency confusion.
    - Librerías de terceros desactualizadas sin prueba de explotabilidad.
    - Scripts de terceros en sus webs.
    - Móvil: certificate pinning, SSL/TLS en apps nativas, ofuscación, detección de root, componentes exportados sin impacto real, y cargar dominios arbitrarios vía `meli://in-app-browser/?url=` o `mercadopago://in-app-browser/?url=`.
    - Fallos de la web de terceros que no sean explotables en su infraestructura.
- **Mínimos:** CVSS menor de 2.0 no se acepta, y la recompensa mínima es de $50.

### 2. Reglas que afectan al proyecto

**Herramientas automáticas.** Están permitidas con límites: no se permiten escaneos automáticos masivos y se pide testing creativo. Tampoco se deben subir resultados de herramientas automáticas.

**Límite de peticiones.** No hay una cifra concreta de peticiones por segundo o por minuto. Lo que sí está prohibido:

- Degradar el servicio de forma significativa, lo que puede llevar a un ban.
- Ataques DoS.
- Fuerza bruta, incluso solo para medir el rate limiting.
- Creación masiva de cuentas.

**Contacto con empleados.** No hay una norma general contra hablar con ellos, pero está prohibida la ingeniería social de empleados, contratistas, proveedores o prestadores de servicio (incluido el phishing). También los ataques físicos y el intento de acceder a datos de otro usuario comprometiendo la cuenta de un cliente o empleado. Las dudas se resuelven por HackerOne o por su Discord.

**Identificación y acceso.**

- Hace falta un Signal de 1.0 o superior en el último año. Con menos, se usan reportes de prueba (trial reports).
- Puedes reclamar usuarios de prueba o crear los tuyos, pero un uso indebido o fuera de alcance puede acarrear un ban. En esos reportes, el CVSS siempre contará Privileges Required como HIGH.
- Hay tarjetas de prueba para simular pagos, sin usar tarjetas reales.
- No puede participar personal interno, ni proveedores o afiliados. Los ex empleados deben esperar un año desde su baja.
- El texto no pide ninguna cabecera especial ni documento de identidad.

**Otras reglas que conviene tener presentes:**

- **Divulgación:** no publiques nada sin acuerdo o autorización. Hay safe harbor (Gold Standard) si respetas las normas.
- **Dependencias y CVE:** los 0-day y CVE se pueden reportar 30 días después de su publicación, con PoC demostrable por internet.
- **Subdomain takeover:** exige poder insertar contenido, con evidencia DNS y página de verificación. No se pueden robar cookies, interactuar con usuarios ni hacer phishing.
- **XSS:** sin bypass de CSP se puntúa más bajo o nada.
- **Respeto:** un lenguaje irrespetuoso hacia los triagers cierra el reporte como N/A.
- **Cambios:** Mercado Libre puede modificar el programa y reevaluar los tiers cuando quiera.


