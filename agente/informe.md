

# Informe de Reconocimiento Pasivo

## 📌 Notas de Alcance
- **`mercadolibre.com`**: ✅ Dentro del alcance autorizado. Investigación completa.
- **`shopify.com`** y **`blog.chaturbate.com`**: ❌ `BLOQUEADO` por todas las herramientas consultadas. Ambos dominios están fuera del alcance autorizado definido en el scope, por lo que no se profundiza en ellos conforme a los lineamientos de la auditoría.

---

## 🔍 `mercadolibre.com`

### 1. Registro WHOIS
| Dato | Valor |
|------|-------|
| **Dominio** | `MERCADOLIBRE.COM` |
| **Alta** | 1999-05-08 |
| **Caducidad** | 2027-10-01 |
| **Último cambio** | 2025-08-30 |
| **Registrador** | Entidad ID `292` |
| **Estado** | `client delete/transfer/update prohibited`, `server delete/transfer/update prohibited` |
| **Nameservers** | `NS-1451.AWSDNS-53.ORG`, `NS-1708.AWSDNS-21.CO.UK`, `NS-368.AWSDNS-46.COM`, `NS-984.AWSDNS-59.NET` |
*Fuente: `whois_dominio`*

### 2. Registros DNS
| Tipo | Valor |
|------|-------|
| **A** | `15.197.170.90`, `3.33.182.45` |
| **MX** | `1 aspmx.l.google.com.`<br>`5 alt1.aspmx.l.google.com.`<br>`5 alt2.aspmx.l.google.com.`<br>`10 aspmx2.googlemail.com.`<br>`10 aspmx3.googlemail.com.` |
| **NS** | `ns-1451.awsdns-53.org.`<br>`ns-368.awsdns-46.com.`<br>`ns-984.awsdns-59.net.`<br>`ns-1708.awsdns-21.co.uk.` |
| **TXT** | `v=spf1 a:spfip.mercadolibre.com include:spfrange.mercadolibre.com ~all`<br>`amazonses:KZfWZfLSFRWn93/urMWkRsrzcgXIawrm/zeEXt6DGIQ=`<br>`amazonses:lAb4bMWZe6i922dR7pKmYqv1URbJ9/ZL2P2uHwRAayY=`<br>`google-site-verification=...` (múltiples)<br>`docusign=...`<br>`openai-domain-verification=dv-pPqxWlnQjziHS1kRXCIxHiyL`<br>`zapier-domain-verification-challenge=393316cd-...`<br>`DirectFedAuthUrl=https://auth-meli.adminml.com/...` |
*Fuente: `dns_registros`*

### 3. Subdominios (en alcance)
- **crt.sh**: 115 subdominios identificados. Incluye: `api.mercadolibre.com`, `status.mercadolibre.com`, `developers.mercadolibre.com`, `sellers.mercadolibre.com`, `notifications.mercadolibre.com`, `internal-api.mercadolibre.com`, `cbt.mercadolibre.com`, `andes.mercadolibre.com`, `bc-jpm-prod-ssl.mercadolibre.com`, `pcivm25.mercadolibre.com`, entre otros.
- **subfinder**: 172 subdominios identificados. Incluye: `auth.mercadolibre.com`, `analytics.mercadolibre.com`, `careers-meli.mercadolibre.com`, `dev-test.mercadolibre.com`, `error.mercadolibre.com`, `envios.mercadolibre.com`, `foro.mercadolibre.com`, `joker2/3/6.mercadolibre.com`, `learninghub-int.mercadolibre.com`, `mldp.mercadolibre.com.ar`, `nginx.*.mercadolibre.com`, `prodeng.*.mercadolibre.com`, `treasury.mercadolibre.com`, `universidad.mercadolibre.com`, entre otros.
*Fuente: `subdominios_crtsh`, `subdominios_subfinder`*

### 4. Huella Tecnológica
- **Servidor Web**: `nginx`
- **IP de respuesta**: `3.33.182.45`
- **Rastreo/Analítica**: `Google-Analytics [UA-80810547-1]`, `Google-Tag-Manager`
- **Cabeceras de seguridad**: `Strict-Transport-Security[max-age=63072000; includeSubDomains; preload]`, `X-XSS-Protection[1; mode=block]`
- **Infraestructura Cloud**: Cabeceras `x-amz-*` presentes (AWS CloudFront/S3/ELB), indicando backend o CDN gestionado en AWS.
*Fuente: `tecnologias_whatweb`*

> ⚠️ `huella_netcraft` devolvió error por bloqueo/JS dinámico en el reporte público.  
> ⚠️ `correos_theharvester` falló en la consulta con las fuentes seleccionadas.

---

## 📋 Resumen Ejecutivo
- **Alta madurez del dominio**: Registrado desde 1999, con protecciones `client/server prohibit` activas contra transferencias o borrados no autorizados.
- **Infraestructura**: DNS gestionado en AWS Route53. Tráfico web servido por `nginx` sobre infraestructura AWS (IP `3.33.182.45` y cabeceras `x-amz-*`). Correo delegado íntegramente a Google Workspace.
- **Seguridad**: Implementación estricta de `HSTS` con preload y protección XSS. Política `SPF` restrictiva (`~all`) con inclusiones internas (`spfip.mercadolibre.com`, `spfrange.mercadolibre.com`). Verificaciones de dominio para múltiples proveedores SaaS (OpenAI, Docusign, Amazon SES, Zapier, Monday, Postman, ElevenLabs, etc.).
- **Superficie de ataque**: ~280+ subdominios únicos entre crt.sh y subfinder, con patrones claros de entornos (`dev`, `stg`, `int`, `prd`), infraestructura (`iron05`, `nginx.s1-*`, `dc4-iron*`), y servicios internos (`api`, `internal-api`, `auth`, `notifications`, `sellers`, `treasury`).
- **Dominios adicionales**: `shopify.com` y `blog.chaturbate.com` fueron rechazados por el filtro de alcance de la auditoría (`BLOQUEADO`).