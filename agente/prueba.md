# Tu alcance autorizado

Este fichero es la **lista blanca** del agente: solo tocará lo que esté aquí. Lo que no aparezca, queda fuera. Aunque el modelo "quiera" salirse, el scope-guard se lo impide.

## Cómo rellenarlo (3 pasos)

1. **Elige** un objetivo que te autorice a investigarlo: un programa público de bug bounty (HackerOne, Bugcrowd, Intigriti...) o tu laboratorio.
2. **Mira su alcance** en la página del programa. Verás dos listas:
   - *In scope* → lo autorizado → va tal cual aquí.
   - *Out of scope* → lo excluido → va con `!` delante.
3. **Tradúcelo** a este formato (una entrada por línea):

| Entrada | Significado |
|---|---|
| `empresa.com` | Dominio exacto |
| `*.empresa.com` | Cualquier subdominio (NO incluye `empresa.com`) |
| `10.10.0.0/24` | Un rango de IPs (para laboratorio) |
| `192.168.56.20` | Una IP exacta |
| `!blog.empresa.com` | **Exclusión**: lo que lleva `!` queda siempre fuera |
| `# ...` | Las líneas con `#` y las vacías se ignoran |

**Reglas, en orden:** exclusiones (`!`) ganan siempre → coincidencia exacta → comodines y rangos → y por defecto, **FUERA**.

Comprueba tu alcance antes de lanzar (ver README, paso 3.2).

---

## Escribe aquí tu alcance

*(Borra el ejemplo de abajo y pon el tuyo.)*

Ejemplo (prográmalo con TU objetivo real):

```
mercadolibre.com
# *.empresa.com
# !blog.empresa.com
```

**scope.txt** · programa: Mercado Libre (HackerOne) · consultado: 2026-11-03
Fuente: <https://hackerone.com/mercadolibre/policy_scopes>

Convención: una línea = un objetivo · `!` = fuera de alcance (tiene prioridad sobre cualquier comodín). Las líneas con `#` son comentarios/notas y el agente debe ignorarlas.

---

## Tier 1 (con recompensa)

### Dominios y wildcards

```
*.adminml.com
*.mercadolibre.com
*.mercadolibre.cl
*.mercadolibre.com.ar
*.mercadolibre.com.co
*.mercadolibre.com.mx
*.mercadolibre.com.pe
*.mercadolibre.com.uy
*.mercadolivre.com.br
*.mercadopago.com
*.mercadopago.cl
*.mercadopago.com.ar
*.mercadopago.com.br
*.mercadopago.com.co
*.mercadopago.com.mx
*.mercadopago.com.pe
*.mercadopago.com.uy
```

### APIs

```
api.mercadopago.com
api.mercadolibre.com
```

### Paths concretos

```
mercadopago.com.mx/crypto/*
mercadopago.cl/crypto/*
mercadopago.com.br/crypto/*
```

### Fuera de la red (no se escanean; solo referencia)

- **Apps:** Mercado Pago (Android/iOS), Mercado Libre (Android/iOS), Mercado Envíos Flex, Extra y Logistics.
- **Hardware:** Point Smart (MLA y MLB).
- **Asset "Leaked Credentials":** credenciales de fuentes públicas (severidad máx. high).

---

## Tier 2 (con recompensa)

```
*.mlstatic.com
logistica.redelcom.cl
www.mercadolibre.co.cr
www.mercadolibre.com.bo
www.mercadolibre.com.do
www.mercadolibre.com.ec
www.mercadolibre.com.gt
www.mercadolibre.com.hn
www.mercadolibre.com.ni
www.mercadolibre.com.pa
www.mercadolibre.com.py
www.mercadolibre.com.sv
www.mercadolivre.com
www.mercadopago.com.ec
mercadopago.com.ve
mpago.li
mpago.la
mercadobackoffice.com
biolibre.ar
biolibre.cl
biolibre.co
biolibre.mx
biolivre.com.br
meliplay.com.ar
meliplay.com.pe
meliplay.com.uy
portalinmobiliario.cl
portalinmobiliario.com
tucarro.com
tucarro.com.co
tumoto.com
furycloud.io
furydocs.io
sustentabilidadmercadolibre.com
```

Notas:

- `mercadoplay.*` → la política no detalla los TLD; confirmar en `policy_scopes` antes de añadir.
- App Android: `com.mercadolibre.android.mplay_tv`.

---

## Tier 3 (solo hallazgos no aplicativos; no es un objetivo de red)

Credenciales filtradas en repos públicos, documentos expuestos, buckets mal configurados. Deben estar vinculados a Mercado Libre. Solo confirmar existencia (1 llamada no destructiva por credencial).

---

## Se acepta reporte pero sin recompensa (desactivado por defecto)

```
# mercadoenvios.com.ve
# www.ipbooster.com
# *.tucarro.com.ve
# *.mercadolibre.com.ve
# mercadolibreexperience.com.*
# mercadolivreexperience.mercadolivre.com.br
# *.modoblack.mercadolivre.com.br
# fullbarhomologa.modoblackfullbar.com.br
```

---

## Fuera de alcance (no se toca)

```
!*.kangu.com.br
!*.gokangu.cl
!*.gokangu.co
!*.gokangu.mx
!*.gokangu.uy
!*.kangu.tech
!developersforum.*
!developers-forum.mercadolibre.com
!wow-int.mercadolibre.com
!*.cn
!compras-mercadolibre.com
```

Notas:

- **Redelcom:** todo fuera de alcance **excepto** `logistica.redelcom.cl` (aplicar `!*.redelcom.cl` con excepción para ese host).
- **Lookalike que NO es del programa** (apareció en el dork "index of"; no tocar): `compras-mercadolibre.com`.
- **Funcionalidades fuera de alcance:** Melidolar y Collaborators.

---

## Reglas operativas para el agente

- **Prohibido:** escaneos masivos, DoS, fuerza bruta (ni para medir rate limit), creación masiva de cuentas.
- **Prohibido:** ingeniería social/phishing, ataques físicos, acceder a datos de otros usuarios comprometiendo cuentas.
- **Sin reporte** de: certificate pinning/SSL nativo, ofuscación, root detection, DoS GraphQL, dependency confusion, KYC, in-app-browser con dominios arbitrarios, librerías desactualizadas sin explotabilidad, scripts de terceros.
- Solo usuarios de prueba y tarjetas de prueba. No subir resultados de herramientas automáticas.
- CVSS < 2.0 no se acepta; recompensa mínima $50. Requiere Signal ≥ 1.0 (si no, *trial reports*).
