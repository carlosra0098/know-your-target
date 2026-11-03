**Enlace al programa:** [https://www.mercadolibre.com](https://www.mercadolibre.com/)
https://hackerone.com/mercadolibre
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

---
# whois
``` bash
09:30:24
https://who.is/whois/mercadolibre.com
```
mercadolibre.com

WHOIS Information

IP Address: [3.33.182.45](https://who.is/whois-ip/ip-address/3.33.182.45)

## Contact Information

### Abuse Contact

Phone

+1.2086851750

### Registrant Contact

Organization

MercadoLibre Inc.

Address

AR

Email

Select Request Email Form at https://domains [dot] markmonitor [dot] com/whois/mercadolibre [dot] com

### Tech Contact

Email

Select Request Email Form at https://domains [dot] markmonitor [dot] com/whois/mercadolibre [dot] com

## Registrar Information

Registrar

MarkMonitor Inc.

WHOIS Server

whois.markmonitor.com

Referral URL

[http://www.markmonitor.com](http://www.markmonitor.com/)

## Important Dates

Created

May 8, 1999

Updated

August 30, 2025

Expires

October 1, 2027

WHOIS data last fetched October 14, 2026

## Nameservers

|Hostname|IP Address|
|---|---|
|[ns-1451.awsdns-53.org](https://who.is/nameserver/ns-1451.awsdns-53.org)|[205.251.197.171](https://who.is/whois-ip/ip-address/205.251.197.171)|
|[ns-1708.awsdns-21.co.uk](https://who.is/nameserver/ns-1708.awsdns-21.co.uk)|[205.251.198.172](https://who.is/whois-ip/ip-address/205.251.198.172)|
|[ns-368.awsdns-46.com](https://who.is/nameserver/ns-368.awsdns-46.com)|[205.251.193.112](https://who.is/whois-ip/ip-address/205.251.193.112)|
|[ns-984.awsdns-59.net](https://who.is/nameserver/ns-984.awsdns-59.net)|[205.251.195.216](https://who.is/whois-ip/ip-address/205.251.195.216)|

## Domain Status

- clientDeleteProhibited https://icann.org/epp#clientDeleteProhibited
- clientTransferProhibited https://icann.org/epp#clientTransferProhibited
- clientUpdateProhibited https://icann.org/epp#clientUpdateProhibited
- serverDeleteProhibited https://icann.org/epp#serverDeleteProhibited
- serverTransferProhibited https://icann.org/epp#serverTransferProhibited
- serverUpdateProhibited https://icann.org/epp#serverUpdateProhibited
- clientDeleteProhibited (https://www.icann.org/epp#clientDeleteProhibited)
- clientTransferProhibited (https://www.icann.org/epp#clientTransferProhibited)
- clientUpdateProhibited (https://www.icann.org/epp#clientUpdateProhibited)
- serverDeleteProhibited (https://www.icann.org/epp#serverDeleteProhibited)
- serverTransferProhibited (https://www.icann.org/epp#serverTransferProhibited)
- serverUpdateProhibited (https://www.icann.org/epp#serverUpdateProhibited)

## Similar Domains

- [mer.ca](https://who.is/whois/mer.ca)
- [merca10.com.br](https://who.is/whois/merca10.com.br)
- [merca20.com](https://who.is/whois/merca20.com)
- [merca24.com](https://who.is/whois/merca24.com)
- [merca2.com](https://who.is/whois/merca2.com)
- [merca2.org](https://who.is/whois/merca2.org)
- [merca3.com](https://who.is/whois/merca3.com)
- [merca3w.com](https://who.is/whois/merca3w.com)
- [merca9.com](https://who.is/whois/merca9.com)
- [mercaa323.com](https://who.is/whois/mercaa323.com)
- [mercaadolibrecl.org](https://who.is/whois/mercaadolibrecl.org)

----------------------------------------------------------
# DNSDumpster

``` bash
10:33:51 
curl.exe -H "X-API-Key: c33b6d8fcde07151f24b208c8f1a7aa6cc571074e84865b7ff73d992ec5bb8cf" https://api.dnsdumpster.com/domain/mercadolibre.com
# Se reciben varios servidores de nombres, correos, TXT.
```
![[Pasted image 20261103122817.png]](https://github.com/carlosra0098/know-your-target/blob/main/anexos/Pasted%20image%2020261103122817.png)

-------------------------
# Subdominios

``` bash
10:54:28
subfinder -silent -d mercadolibre.com
# Se reciben todos los subdominios que tiene el dominio.
```
nginx.s1-int-prd.mercadolibre.com
www.soap.mercadolibre.com
internal-api-stage.mercadolibre.com
portal-antares.mercadolibre.com
dc4-iron09.mercadolibre.com
andesx.mercadolibre.com
dnsps52.mercadolibre.com
iron06-c.mercadolibre.com
citiportal.mercadolibre.com
accountrecovery.mercadolibre.com
dc4-iron08-b.mercadolibre.com
dc4-iron09-d.mercadolibre.com
pppi-stg.mercadolibre.com
inmuebles-home.mercadolibre.com
dc4-iron05-b.mercadolibre.com
iron04-e.mercadolibre.com
iron07.mercadolibre.com
ns2.mercadolibre.com
www.content.mercadolibre.com
eshops.mercadolibre.com
videojuegos.mercadolibre.com
dc4-ironinbound03.mercadolibre.com
iron07-e.mercadolibre.com
nginx.m-int-dev.mercadolibre.com
training.mercadolibre.com
chattest.mercadolibre.com
alejandria-int.mercadolibre.com
dns2.mercadolibre.com
dnsps11.mercadolibre.com
dnsps28.mercadolibre.com
iron04-c.mercadolibre.com
joker6.mercadolibre.com
news.mercadolibre.com
dnsps31.mercadolibre.com
iron02-b.mercadolibre.com
iron06.mercadolibre.com
omp.ms.mercadolibre.com
prodeng-playground-internal.mercadolibre.com
survey.mercadolibre.com
bc-jpm-beta-sslv2.mercadolibre.com
www.jobs.mercadolibre.com
auth-identity.mercadolibre.com
dc4-iron05.mercadolibre.com
dc4-iron08-c.mercadolibre.com
sdl-agent.mercadolibre.com
treasury.mercadolibre.com
arte-antiguedades.mercadolibre.com
myml-applications.mercadolibre.com
pcivm26.mercadolibre.com
prodeng-internal.mercadolibre.com
prodeng-playground.mercadolibre.com
electronica.mercadolibre.com
publicidad.mercadolibre.com
registration.mercadolibre.com
pago.mercadolibre.com
artifacts.mercadolibre.com
ml-challenge.mercadolibre.com
guia.mercadolibre.com
iron07-c.mercadolibre.com
o12.ptr7196.sg.mercadolibre.com
bc-jpm-prod-update.mercadolibre.com
social.mercadolibre.com
iron04-b.mercadolibre.com
www.encuestas.mercadolibre.com
telefonia.mercadolibre.com
iron02.mercadolibre.com
joker2.mercadolibre.com
joker3.mercadolibre.com
static-cbt.mercadolibre.com
dev-test.mercadolibre.com
realtime-dev.global-selling.mercadolibre.com
ns4.mercadolibre.com
resell.mercadolibre.com
dnsgc.mercadolibre.com
omp.e.mercadolibre.com
iron03.mercadolibre.com
iron07-d.mercadolibre.com
universidad.mercadolibre.com
tienda.mercadolibre.com
prod-proxy-urutec.mercadolibre.com
legolas.mercadolibre.com
sandbox.mercadolibre.com
cbt.mercadolibre.com
dc4-iron08-d.mercadolibre.com
nginx.s1-pub-dev.mercadolibre.com
bc-jpm-prod-ssl.mercadolibre.com
test-marcos3.mercadolibre.com
coleccionables.mercadolibre.com
vender.mercadolibre.com
o6.ptr4588.sg.a.mercadolibre.com
lhstage.mercadolibre.com
a.mercadolibre.com
vehiculos.mercadolibre.com
andes.mercadolibre.com
andes-landings.mercadolibre.com
global-selling.mercadolibre.com
nginx.s1-int-dev.mercadolibre.com
content.mercadolibre.com
mercadoclics.mercadolibre.com
login-mobile.mercadolibre.com
ayuda.mercadolibre.com
buyingflow.mercadolibre.com
reputacion.mercadolibre.com
test.baloto.mercadolibre.com
massive2.mercadolibre.com
postfix02.mercadolibre.com
vendedores.mercadolibre.com
dare-transnetwork-adapter.mercadolibre.com
prodeng-overvpn.mercadolibre.com
www.api.mercadolibre.com
iron07-b.mercadolibre.com
pppi.mercadolibre.com
nginx.s1-pub-prd.mercadolibre.com
sustentabilidad.mercadolibre.com
reparacion-instalacion.mercadolibre.com
dc4-iron05-c.mercadolibre.com
ns3.mercadolibre.com
nginx.s2-int-prd.mercadolibre.com
bc-jpm-prod-transfer.mercadolibre.com
addresses.mercadolibre.com
events-ads.mercadolibre.com
envios.mercadolibre.com
bc-jpm-beta-update.mercadolibre.com.mercadolibre.com
dns3.mercadolibre.com
dnsps32.mercadolibre.com
nginx.s2-pub-prd.mercadolibre.com
learning.mercadolibre.com
api-cbt.mercadolibre.com
opinion.mercadolibre.com
dnsps5.mercadolibre.com
articulo.mercadolibre.com
reviews.mercadolibre.com
realtime-prod.global-selling.mercadolibre.com
play.mercadolibre.com
www.universidad.mercadolibre.com
feedback.mercadolibre.com
e.mercadolibre.com
iron04-f.mercadolibre.com
consultoras.mercadolibre.com
encuesta.mercadolibre.com
www.vendedores.mercadolibre.com
apps.mercadolibre.com
mp3.mercadolibre.com
nginx.m-int-prd.mercadolibre.com
device.mercadolibre.com
celulares.mercadolibre.com
inscripcion.mercadolibre.com
navidad.mercadolibre.com
seguridad.mercadolibre.com
dnsps13.mercadolibre.com
casas.mercadolibre.com
moto.mercadolibre.com
api.mercadolibre.com
dnsps1.mercadolibre.com
departamento-suite.mercadolibre.com
perfil.mercadolibre.com
profesional.mercadolibre.com
dc4-iron09-c.mercadolibre.com
jobs.mercadolibre.com
ucs.orion-prd.mercadolibre.com
advertising.mercadolibre.com
universidadvirtual.mercadolibre.com
data.mercadolibre.com
iron04.mercadolibre.com
ucs.orion-dev.mercadolibre.com
status.mercadolibre.com
auto.mercadolibre.com
ideas.mercadolibre.com
portal-cbt.mercadolibre.com
o7.ptr3323.sg.r.mercadolibre.com
sellers.mercadolibre.com
realtime-dev.sellers.mercadolibre.com
bc-jpm-beta-ssl.mercadolibre.com
investor.mercadolibre.com
manualdeestilo.mercadolibre.com
ux.mercadolibre.com
myaccount.mercadolibre.com
camioneta.mercadolibre.com
dnsps27.mercadolibre.com
dejavu.mercadolibre.com
prostores.mercadolibre.com
casa-villa.mercadolibre.com
alliance.mercadolibre.com
inmuebles.mercadolibre.com
test-marcos2.mercadolibre.com
www.citiportal.mercadolibre.com
terreno.mercadolibre.com
cerbero.mercadolibre.com
iron06-d.mercadolibre.com
dnsps6.mercadolibre.com
dnsps34.mercadolibre.com
omptrans.e.mercadolibre.com
encuestas.mercadolibre.com
departamentos.mercadolibre.com
dc4-iron05-d.mercadolibre.com
dnsps41.mercadolibre.com
internal-api.mercadolibre.com
ironport-inbound02.mercadolibre.com
voice-agents.tcp.s1-int-prd.mercadolibre.com
fotografia.mercadolibre.com
listado.mercadolibre.com
servicio.mercadolibre.com
o18.sg.a.mercadolibre.com
foro.mercadolibre.com
iron03-b.mercadolibre.com
iron06-e.mercadolibre.com
soap.mercadolibre.com
autos.mercadolibre.com
list.mercadolibre.com
ofertas.mercadolibre.com
dns4.mercadolibre.com
o5.ptr8540.sg.a.mercadolibre.com
o11.ptr1968.sg.mercadolibre.com
mldp.mercadolibre.com
syi.mercadolibre.com
careers-meli.mercadolibre.com
ms.mercadolibre.com
motos.mercadolibre.com
ironport-inbound.mercadolibre.com
global-selling-dev.mercadolibre.com
computacion.mercadolibre.com
mediations.mercadolibre.com
m.mercadolibre.com
auth.mercadolibre.com
iron02-c.mercadolibre.com
learninghub-studio-int.mercadolibre.com
dnsps23.mercadolibre.com
servicedesk.mercadolibre.com
servicios-home.mercadolibre.com
syimobile.mercadolibre.com
vehiculo.mercadolibre.com
dnsps14.mercadolibre.com
eqix-ema-dc.mercadolibre.com
error.mercadolibre.com
hp.mercadolibre.com
iron01.mercadolibre.com
massive.mercadolibre.com
vehiculos-home.mercadolibre.com
dnsps22.mercadolibre.com
dc4-iron05-e.mercadolibre.com
appstore.mercadolibre.com
compra.mercadolibre.com
centrodepartners.mercadolibre.com
iron06-b.mercadolibre.com
o1.sg.mercadolibre.com
home.mercadolibre.com
servicios.mercadolibre.com
verificacion.mercadolibre.com
developers-forum.mercadolibre.com
learninghub-int.mercadolibre.com
test.mercadolibre.com
dc4-iron09-e.mercadolibre.com
www.mercadolibre.com
www.servicedesk.mercadolibre.com
video.mercadolibre.com
bc-jpm-beta-transfer.mercadolibre.com
dc4-ironinbound04.mercadolibre.com
dnsps12.mercadolibre.com
dnsps2.mercadolibre.com
op-scim.mercadolibre.com
prodeng.mercadolibre.com
realtime-prod.sellers.mercadolibre.com
pmspxl.mercadolibre.com
www.investor.mercadolibre.com
dnsps24.mercadolibre.com
bc-jpm-beta-update.mercadolibre.com
hom-proxy-urutec.mercadolibre.com
refpayments.baloto.mercadolibre.com
www.data.mercadolibre.com
pmstrk.mercadolibre.com
questions.mercadolibre.com
o2.ptr6987.sg.a.mercadolibre.com
dnsps21.mercadolibre.com
o3.ptr3169.sg.a.mercadolibre.com
analytics.mercadolibre.com
nginx.m-pub-dev.mercadolibre.com
chat.mercadolibre.com
vip.mercadolibre.com
confirmacao.mercadolibre.com
dnsps42.mercadolibre.com
homl-proxy-urutec.mercadolibre.com
inmueble.mercadolibre.com
tendencias.mercadolibre.com
pcivm25.mercadolibre.com
applications.mercadolibre.com
dc4-iron08.mercadolibre.com
sandbox-cbt.mercadolibre.com
dc4-iron08-e.mercadolibre.com
developers.mercadolibre.com
dnsps51.mercadolibre.com
test-vendedores.mercadolibre.com
notifications.mercadolibre.com
o19.sg.a.mercadolibre.com
fooddeliverywebapp.mercadolibre.com
domssl.mercadolibre.com
dnsps33.mercadolibre.com
omptrans.ms.mercadolibre.com
fiesta-evento.mercadolibre.com
o4.ptr5260.sg.a.mercadolibre.com
ns1.mercadolibre.com

-------------------------
# Huella tecnológica

``` bash
12:05:40
https://sitereport.netcraft.com/?url=https://mercadolibre.com
# Hosting, CDN/WAF, tecnologías, histórico a través de netcraft.
```

![[Pasted image 20261103120353.png]]
![[Pasted image 20261103120418.png]]
![[Pasted image 20261103120434.png]]
![[Pasted image 20261103120455.png]]
![[Pasted image 20261103120529.png]]

-------------------------
# Ficheros expuestos

``` bash
12:12:46
curl -s https://mercadolibre.com/robots.txt
curl -s https://mercadolibre.com/.well-known/security.txt
# Rutas que el dueño no quiere indexar.
```
## robots.txt
User-agent: Amazonbot
User-agent: PerplexityBot
User-agent: Perplexity-User
User-agent: ClaudeBot
User-agent: Claude-User
User-agent: GPTBot
User-agent: ChatGPT-User
Disallow: /

User-agent: AdsBot-Google
Disallow: /tracks*

User-agent: AdsBot-Google-Mobile
Disallow: /tracks*

User-agent: *
Disallow: /jms/*/compra
Disallow: /jms/*/buyingflow
Disallow: /jms/*/lgz/
Disallow: /jms/*/gz/webdevice/config
Disallow: /adn/api*
Allow: /.well-known/
Allow: /jms/*/lgz/msl/login/
## security.txt
![[Pasted image 20261103124251.png]]

-------------------------
# Servicios expuestos


``` bash
https://www.shodan.io/search?query=mercadolibre.com
# Puertos y servicios visibles sin tocar nada.
```
![[Pasted image 20261103122116.png]]
![[Pasted image 20261103123227.png]]

----
# Google dorks

``` bash
12:45:20
intitle:"index of" mercadolibre.com --> https://compras-mercadolibre.com/
# Documentos, paneles, directorios indexados.
```

Al haber buscado en Google por _intitle:"index of" mercadolibre.com_, aparece una página con la URL https://compras-mercadolibre.com/ en la cual aparece un binario al que no se tiene acceso, ya que es restringido.
![[Pasted image 20261103124940.png]]
![[Pasted image 20261103125008.png]]

---
# Correos

``` bash
12:53:54
https://hunter.io/search/mercadolibre.com
# Correos y patrón de correo corporativo.
```
Al utilizar la página de Hunter.io y usar la URL de mercado libre, aparecen 331 resultados de distintos tipos de correos y patrones corporativos de la empresa desde ejecutivos hasta departamentos desconocidos.
![[Pasted image 20261103130114.png]]

---
