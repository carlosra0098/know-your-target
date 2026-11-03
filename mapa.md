### 1. Resumen

- **MercadoLibre Inc.**, con sede en Buenos Aires (Argentina), es la plataforma de comercio electrónico y pagos líder de Latinoamérica (Mercado Libre, Mercado Pago, Mercado Envíos); según Hunter.io, Internet Publishing, >10.001 empleados, empresa privada.
- Infraestructura **100% en AWS**: DNS en Route 53, balanceo con AWS ELB/CloudFront, certificados emitidos por Amazon Trust Services (TLS 1.3, sin POODLE ni Heartbleed).
- El dominio apex (`3.33.182.45`) resuelve a **AWS Global Accelerator**, confirmando una arquitectura multirregión detrás de un único punto de entrada.
- El correo corporativo usa **Google Workspace** (MX hacia `aspmx.l.google.com`) y el envío masivo pasa por **SendGrid** (`o*.sg.a.mercadolibre.com`, rango 149.72.x.x); DMARC está en `p=reject` con reporting a Netcraft, Proofpoint y vali.email.
- El Google dork reveló un **listado de directorio abierto** en `compras-mercadolibre.com` (dominio independiente, LiteSpeed), con un binario en `/cgi-bin/` al que el acceso devuelve 403.

### 2. Dominios y subdominios

IPs tomadas del JSON de DNSDumpster (imagen 7) y del informe Netcraft (imagen 1); el resto de los ~250 nombres de `subfinder` no tiene IP en el cuaderno, solo el nombre.

|Subdominio|IP|En alcance|Uso aparente|
|---|---|---|---|
|`mercadolibre.com` (apex)|3.33.182.45 (AWS Global Accelerator)|Sí (Tier 1, wildcard)|Entrada principal, multirregión|
|`www.mercadolibre.com`, `m.mercadolibre.com`, `home`|n/d (mismo rango CloudFront)|Sí|Web/móvil|
|`api.mercadolibre.com`|99.84.x.x — CloudFront|Sí (asset propio Tier 1)|API pública|
|`internal-api.mercadolibre.com`, `internal-api-stage`|n/d|Sí|API interna / staging|
|`auth.mercadolibre.com`|3.168.122.89 — CloudFront|Sí|Autenticación|
|`auth-identity`, `accountrecovery`, `login-mobile`, `registration`, `seguridad`, `verificacion`|n/d|Sí|Identidad y recuperación de cuenta|
|`developers.mercadolibre.com`|18.164.112.21 — CloudFront|Sí|Portal de desarrolladores|
|`applications.mercadolibre.com`|18.164.112.21 — CloudFront|Sí|Apps/integraciones|
|`appstore.mercadolibre.com`, `dev-test.mercadolibre.com`|18.164.116.5 — CloudFront|Sí|Distribución de apps / pruebas|
|`artifacts.mercadolibre.com`|98.80.0.0/13 — AMAZON-AES|Sí|Repositorio de artefactos internos|
|`careers-meli.mercadolibre.com`|13.33.252.40 — CloudFront|Sí|Empleo|
|`cbt.mercadolibre.com`, `data.mercadolibre.com`|3.168.122.27 — CloudFront|Sí|Cross-border trade / datos|
|`centrodepartners`, `consultoras`, `dejavu.mercadolibre.com`|3.168.122.36 / .89 — CloudFront|Sí|Portales de partners/consultoras, app interna|
|`alliance.mercadolibre.com`|52.48.0.14 — Amazon (Irlanda)|Sí|Alianzas (posible servicio regional UE)|
|`andes.mercadolibre.com`, `andes-landings`|52.51.23.169 — Amazon eu-west-1 (Irlanda)|Sí|Plataforma interna “Andes” (landings)|
|`error.mercadolibre.com`|143.204.98.4 — CloudFront|Sí|Página de error genérica|
|`envios.mercadolibre.com`|18.164.116.15 — CloudFront|Sí|Mercado Envíos|
|`ns1-4`, `dns2-4`, `dnsps*`, `dnsgc.mercadolibre.com`|205.251.19x.x — AWS Route 53|Sí|Servidores DNS autoritativos|
|`o1…o19.*.sg.a.mercadolibre.com`|149.72.x.x — SendGrid|Sí|Envío de correo masivo/transaccional|
|`prodeng*`, `prodeng-overvpn`, `prodeng-playground(-internal)`|n/d|Sí|Infraestructura de ingeniería, posible acceso solo VPN|
|`sandbox`, `sandbox-cbt`, `lhstage`, `test*`, `chattest`, `nginx.*-dev`|n/d|Sí|Entornos de pruebas|
|`bc-jpm-*` (beta/prod, ssl/sslv2/transfer/update)|n/d|Sí|Posible integración bancaria (JPMorgan), sin confirmar|
|`prod-proxy-urutec`, `hom-proxy-urutec`, `homl-proxy-urutec`|n/d|Sí|Proxy de integrador uruguayo|
|`compras-mercadolibre.com`|n/d (LiteSpeed, hosting distinto)|**No** (fuera del wildcard `*.mercadolibre.com`)|Dominio parecido con listado de directorio abierto; sin vínculo demostrado con la empresa|

El resto de los ~230 nombres de `subfinder` (categorías del marketplace, `jobs`, `universidad`, `investor`, `status`, etc.) quedan en la tabla de la respuesta anterior: todos bajo `*.mercadolibre.com`, en alcance Tier 1, sin IP propia en el cuaderno.

### 3. Infraestructura y servicios

**Hosting y DNS**

- Netblock owner: **Amazon Technologies Inc.**, AS16509, hosting en EE. UU.; DNS admin `awsdns-hostmaster@amazon.com`.
- Nameservers Route 53 (`ns-368.awsdns-46.com` y los cuatro del WHOIS), DNSSEC **activado**.
- Sitio visto por primera vez en marzo de 2000, idioma principal español, rank Netcraft 50.320.

**TLS/Certificados**

- Certificado wildcard `*.mercadolibre.com` (SAN incluye también el apex), válido del 8 sep 2026 al 24 mar 2027, emitido por **Amazon RSA 2048 M01** (cadena hasta Amazon Root CA 1).
- TLS 1.3, Perfect Forward Secrecy, servidor **`awselb/2.0`** (AWS Elastic Load Balancer). Sin POODLE, sin Heartbleed.

**Correo (SPF/DMARC)**

- SPF: `a:spfip.mercadolibre.com include:spfrange.mercadolibre.com ~all` (softfail, no hardfail).
- DMARC: **`p=reject`**, `pct=100`, reportes a `dmarcrua@mercadolibre.com` y a terceros (netcraft.com, vali.email, proofpoint.com) — indica monitorización activa de suplantación de dominio.
- MX hacia `aspmx.l.google.com` y `alt1/alt2.aspmx.l.google.com` → **Google Workspace** para el correo corporativo.
- Envío masivo/transaccional delegado a **SendGrid** (rango 149.72.x.x, ASN 11377).
- Verificaciones TXT del dominio para SuccessFactors, DocuSign, Miro, Monday, OneTrust, Zapier, Airtable, Pardot, Apple y otros — reflejan el stack SaaS corporativo (RR. HH., firma digital, gestión de proyectos, privacidad, marketing).

**Site Technology (Netcraft)**

- Red: AWS Route 53. Servidor: SSL activo. Encoding UTF-8. CSS externo. **Sin web trackers detectados.**

**Google dork — `compras-mercadolibre.com`**

- Listado de directorio abierto (`Index of /`) servido por **LiteSpeed Web Server**, con una carpeta `cgi-bin` modificada el 26/01/2025; el acceso al binario dentro de esa carpeta devuelve **403 Forbidden**. Es un dominio y hosting completamente distintos a `mercadolibre.com` (no AWS), así que no hay evidencia de que pertenezca a Mercado Libre.

**`security.txt`**

- `https://mercadolibre.com/.well-known/security.txt` devuelve **404** (“Parece que esta página no existe”): no publican política de divulgación en esa ruta (usan HackerOne como canal, según el propio programa).

**Shodan (`mercadolibre.com`)**

- **654 resultados totales**, pero es una búsqueda de texto libre, no un filtro por organización: aparecen IPs en OVH, DigitalOcean, Contabo y Google Cloud que probablemente solo mencionan “mercadolibre.com” en un banner o certificado, no son del propio Mercado Libre. Hay que tratar estos resultados con cautela y cruzarlos con el ASN de Amazon antes de investigar nada.
- Top organizaciones: **Amazon Technologies Inc. (162)**, Amazon Data Services Northern Virginia (84), DigitalOcean LLC (40), Contabo GmbH (37), Amazon.com Inc. (33).
- Top países: EE. UU. (438), Brasil (88), Alemania (35), Canadá (22), Argentina (13).
- Top puertos: 443 (443), 80 (176), 3000 (11), 8080 (8), 3001 (2) — los puertos 3000/3001/8080 (poco habituales en producción) son los más interesantes para revisar.
- Top productos: **nginx (406)**, Apache httpd (90), Microsoft IIS httpd (5), OpenResty (2). Top SO: Ubuntu (177), Windows (7).

### 4. Correos y personas

- Patrón confirmado por Hunter.io: **`{nombre}.{apellido}@mercadolibre.com`**, con “Accept all: YES” (el servidor acepta cualquier dirección con ese patrón, lo que dificulta validar cuáles son reales).
- 331 resultados, mayoría en IT/Engineering (89), seguido de departamento desconocido (125), Support (15), Sales (11), Arts & Design (11), Data & Research (7), Finance (7).
- Perfil ejecutivo visible: **Marcos Galperin, CEO** (`marcos.galperin@mercadolibre.com`), además de un Global Process Owner y un Board Member con correo oculto.
- Organización: Buenos Aires, Argentina; tamaño >10.001 empleados; empresa privada.
- Recuerda que el programa prohíbe explícitamente la ingeniería social y el phishing a empleados: estos datos sirven para dimensionar la superficie, no para contactarlos.

### 5. Puntos de interés para la fase activa

1. **`api.mercadolibre.com`, `auth.mercadolibre.com` y la capa de identidad (`auth-identity`, `accountrecovery`, `login-mobile`).** Siguen siendo el foco de mayor impacto: assets Tier 1 propios, manejan sesión y datos de usuario. El SPF en softfail (`~all`) y el patrón de correo “accept all” hacen más plausible el phishing externo contra usuarios (no contra empleados, que está prohibido), así que vale la pena revisar si hay mecanismos anti-spoofing adicionales pese al DMARC `p=reject`.
2. **Puertos atípicos en Shodan (3000, 3001, 8080) dentro del ASN de Amazon (AS16509).** Esos puertos no son los habituales de un front de producción y suelen corresponder a paneles de administración, apps de desarrollo expuestas por error o servicios internos mal segmentados. Hay que filtrar primero por organización Amazon/AS16509 para descartar ruido de otros hosts que solo mencionan “mercadolibre.com”.
3. **Entornos de preproducción y rutas bloqueadas en `robots.txt` (`/jms/*/compra`, `/jms/*/buyingflow`, `/jms/*/lgz/`, `prodeng-playground-internal`, `sandbox`, `dev-test`).** El propio `robots.txt` señala las rutas que la empresa no quiere indexadas, lo que suele coincidir con flujos sensibles (compra, login) con menos protección operativa. Conviene comprobar primero cuáles resuelven públicamente antes de tocar nada, respetando el límite de no hacer fuerza bruta ni degradar el servicio.

`compras-mercadolibre.com` queda fuera de esta lista porque no está en el wildcard de alcance y no hay evidencia de que pertenezca a Mercado Libre; solo sería reportable como Tier 3 si se logra demostrar ese vínculo.

---
# Anexos

![[Pasted image 20261103122817.png]]

---

![[Pasted image 20261103120353.png]]
![[Pasted image 20261103120418.png]]
![[Pasted image 20261103120434.png]]
![[Pasted image 20261103120455.png]]
![[Pasted image 20261103120529.png]]

---

![[Pasted image 20261103124251.png]]

---

![[Pasted image 20261103122116.png]]
![[Pasted image 20261103123227.png|332]]

---

![[Pasted image 20261103124940.png]]
![[Pasted image 20261103125008.png]]

---

![[Pasted image 20261103130114.png]]