# Colecciones Postman — Plataforma Yanki

Colecciones Postman v2.1 generadas automáticamente a partir de los scripts de pruebas integrales de la plataforma Yanki. Cada colección corresponde a un set de pruebas y está completamente documentada en español.

## 📋 Índice de Colecciones

| # | Archivo | Colección | Requests | Naturaleza |
|---|---------|-----------|----------|------------|
| 1 | [`SET-08-Infraestructura.postman_collection.json`](SET-08-Infraestructura.postman_collection.json) | SET-08 - Infraestructura | 6 | Health checks, Eureka, Config Server, Gateway rutas |
| 2 | [`SET-01-Authenticacion.postman_collection.json`](SET-01-Authenticacion.postman_collection.json) | SET-01 - Autenticación | 8 | Login, refresh token, credenciales inválidas, token inválido |
| 3 | [`SET-02-Customers.postman_collection.json`](SET-02-Customers.postman_collection.json) | SET-02 - Customers | 6 | CRUD clientes, duplicados, validación de campos |
| 4 | [`SET-03-Accounts.postman_collection.json`](SET-03-Accounts.postman_collection.json) | SET-03 - Accounts | 6 | CRUD cuentas, depósitos, retiros, saldo insuficiente |
| 5 | [`SET-05-Credits.postman_collection.json`](SET-05-Credits.postman_collection.json) | SET-05 - Credits | 3 | Listar créditos, solicitar crédito, crédito inexistente |
| 6 | [`SET-04-Cards.postman_collection.json`](SET-04-Cards.postman_collection.json) | SET-04 - Cards | 3 | Listar tarjetas, emitir tarjeta, tarjeta inexistente |
| 7 | [`SET-06-Transfers.postman_collection.json`](SET-06-Transfers.postman_collection.json) | SET-06 - Transfers | 2 | Listar transferencias, transferencia a cuenta inexistente |
| 8 | [`SET-07-Wallet.postman_collection.json`](SET-07-Wallet.postman_collection.json) | SET-07 - Wallet | 3 | Listar wallets, crear wallet, wallet inexistente |
| 9 | [`SET-09-ErroresGlobales.postman_collection.json`](SET-09-ErroresGlobales.postman_collection.json) | SET-09 - Errores Globales | 3 | Ruta inexistente (404), método no permitido (405), actuator |
| 10 | [`SET-10-Reports.postman_collection.json`](SET-10-Reports.postman_collection.json) | SET-10 - Reports | 6 | Reportes bancarios, agregados, cliente 360°, movimientos |
| 11 | [`SET-11-VIP-PYME.postman_collection.json`](SET-11-VIP-PYME.postman_collection.json) | SET-11 - VIP/PYME | 7 | Validaciones perfiles VIP/PYME, actualización cliente |
| 12 | [`SET-12-CreditsAdvanced.postman_collection.json`](SET-12-CreditsAdvanced.postman_collection.json) | SET-12 - Credits Advanced | 8 | Reestructuración, cancelación, pagos, cronograma |
| 13 | [`SET-13-CardsAdvanced.postman_collection.json`](SET-13-CardsAdvanced.postman_collection.json) | SET-13 - Cards Advanced | 3 | Límite, estado de cuenta, consumptions, movimientos |
| 14 | [`SET-14-TransfersAdvanced.postman_collection.json`](SET-14-TransfersAdvanced.postman_collection.json) | SET-14 - Transfers Advanced | 2 | Validaciones: origen/destino inexistente, idempotencia |
| 15 | [`SET-15-WalletE2E.postman_collection.json`](SET-15-WalletE2E.postman_collection.json) | SET-15 - Wallet E2E | 3 | Flujo integral wallet, top-up, P2P, retiro, tarjetas |
| 16 | [`SET-16-AuthAdvanced.postman_collection.json`](SET-16-AuthAdvanced.postman_collection.json) | SET-16 - Auth Advanced | 5 | Token malformado, issuer inválido, blacklist, roles |
| 17 | [`E2E-HappyPath.postman_collection.json`](E2E-HappyPath.postman_collection.json) | E2E - Happy Path Completo | 22 | Flujo E2E continuo: auth, customers, accounts, cards, transfers, wallet, reports |

**Total: 17 colecciones, 81 requests**

## 🚀 Cómo Usar

### 1. Importar las colecciones en Postman

1. Abre Postman
2. Click en **Import** (arriba a la izquierda)
3. Selecciona los archivos `.json` de este directorio
4. Las colecciones aparecerán en tu sidebar

### 2. Configurar las variables

Cada colección incluye variables de colección predefinidas:

| Variable | Valor por defecto | Descripción |
|----------|-------------------|-------------|
| `base_url` | `http://localhost:8080` | URL del API Gateway |
| `auth_token` | `` | JWT access token (se obtiene del login) |
| `refresh_token` | `` | JWT refresh token (se obtiene del login) |
| `customer_id` | `` | ID del cliente creado |
| `account_id` | `` | ID de la cuenta creada |
| `card_id` | `` | ID de la tarjeta creada |
| `credit_id` | `` | ID del crédito creado |
| `wallet_id` | `` | ID del wallet creado |

### 3. Orden de ejecución recomendado

Ejecuta las colecciones en este orden para garantizar que las variables se poblen correctamente:

```
1.  SET-08 - Infraestructura      (verificar que todo está corriendo)
2.  SET-01 - Autenticación         (obtener auth_token)
3.  SET-02 - Customers             (crear cliente → customer_id)
4.  SET-03 - Accounts              (crear cuenta → account_id)
5.  SET-05 - Credits               (crear crédito → credit_id)
6.  SET-04 - Cards                 (crear tarjeta → card_id)
7.  SET-06 - Transfers             (usar account_id)
8.  SET-07 - Wallet                (crear wallet → wallet_id)
9.  SET-09 - Errores Globales      (independiente)
10. SET-10 - Reports               (usar customer_id, card_id)
11. SET-11 - VIP/PYME              (usar customer_id)
12. SET-12 - Credits Advanced      (usar credit_id)
13. SET-13 - Cards Advanced        (usar card_id)
14. SET-14 - Transfers Advanced    (usar account_id)
15. SET-15 - Wallet E2E            (usar wallet_id)
16. SET-16 - Auth Advanced         (independiente)
17. E2E - Happy Path Completo      (flujo independiente completo)
```

### 4. Ejecutar la colección E2E

La colección `E2E-HappyPath` es un flujo independiente que:
1. Hace login automáticamente
2. Crea 3 clientes (STANDARD, VIP, PYME)
3. Abre 2 cuentas (SAVINGS, CURRENT)
4. Emite 2 tarjetas (débito, crédito)
5. Realiza transferencia intra-cliente
6. Crea wallet, asocia tarjeta y hace top-up
7. Genera reporte 360°
8. Verifica saldos finales
9. Cierra sesión

**Para ejecutarla:** Importa la colección y usa **Collection Runner** → Selecciona "E2E - Happy Path Completo" → Run.

## 📊 Resumen por Tipo de Prueba

| Tipo | Colecciones | Requests |
|------|-------------|----------|
| **Happy Path (HP)** | Todas | ~45 |
| **Negative Happy Path (NHP)** | Todas | ~36 |
| **Infraestructura** | SET-08, SET-09 | 9 |
| **Autenticación** | SET-01, SET-16 | 13 |
| **Negocio** | SET-02 a SET-07, SET-10, SET-11 | 34 |
| **Avanzado** | SET-12 a SET-15 | 16 |
| **E2E** | E2E-HappyPath | 22 |

## 🔧 Requisitos

- **Postman** v10+ (compatible con formato v2.1)
- **Plataforma Yanki** en ejecución (`docker-compose.full.yml`)
- **API Gateway** accesible en `http://localhost:8080`
- **MongoDB** con `yanki_auth` conteniendo credenciales de admin/operador

## 📝 Notas

- Los requests de tipo **Negative** esperan códigos de error (400, 401, 404, 405, 409, 422).
- Los tests Postman (`pm.test`) validan automáticamente los códigos de estado esperados.
- El request `PRUEBA-01-01: Login ADMIN` extrae automáticamente el token y lo guarda en `auth_token`.
- Los IDs de recursos (customer_id, account_id, etc.) se extraen automáticamente con `pm.collectionVariables.set()`.
- Para ejecutar las colecciones avanzadas (SET-12 a SET-15), primero ejecuta las colecciones base correspondientes para poblar las variables.

## 🔗 Referencias

- **Scripts de prueba:** [`pruebas_integrales/run-tests.ps1`](../../pruebas_integrales/run-tests.ps1), [`pruebas_integrales/run-happy-path-e2e.ps1`](../../pruebas_integrales/run-happy-path-e2e.ps1)
- **Documentación de sets:** [`pruebas_integrales/SET-XX-*.md`](../../pruebas_integrales/)
- **Informe de pruebas:** [`pruebas_integrales/INFORME-PRUEBAS-INTEGRALES.md`](../../pruebas_integrales/INFORME-PRUEBAS-INTEGRALES.md)
- **Casos de prueba QA:** [`../CASOS_PRUEBA`](../CASOS_PRUEBA/CASOS_PRUEBA_QA.md)
- **Matriz de trazabilidad:** [`../CASOS_PRUEBA`](../CASOS_PRUEBA/RTM.md)

---

*Generado automáticamente a partir de los scripts de pruebas integrales de la plataforma Yanki.*
