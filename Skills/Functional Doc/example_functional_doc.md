# TeeShop — Tienda Online de Camisetas

## URLs

- **DEV:** https://dev-teeshop-ui.app.ejemplo.com
- **PRE:** https://pre-teeshop-ui.app.ejemplo.com
- **PROD:** https://shop-europe.cloud.ejemplo.com/4/teeshop

---

## ¿Qué es TeeShop?

**TeeShop** es la aplicación responsable de gestionar y dirigir el proceso de venta de camisetas (catálogo, carrito, pago) a través de las diferentes etapas de una tienda online de forma automática y eficiente.

### Qué hace

- 🛒 Calcula recomendaciones automáticas para que el cliente encuentre la camiseta adecuada
- 🤖 Se adapta en tiempo real a cambios en el catálogo (stock agotado, promociones, etc.)
- 📊 Coordina con los sistemas externos (pasarela de pago, almacén, mensajería) para completar los pedidos
- 📍 Mantiene la precisión del inventario sin errores

### Quién lo usa

- Clientes finales (a través de la web/app)
- Agentes de atención al cliente
- Técnicos de mantenimiento de la plataforma
- Administradores de catálogo de TeeShop
- Store Managers (Gestores de Tienda)

### Qué problema resuelve

Antes de TeeShop, gestionar la venta de camisetas a través de canales dispersos era lento y propenso a errores. TeeShop automatiza completamente este proceso, asegurando que:

- Los pedidos lleguen siempre al cliente correcto
- El flujo de compra sea continuo y eficiente
- Se adapte automáticamente a problemas (productos sin stock, cambios de precio)
- Se reduzcan significativamente los tiempos de gestión de pedidos

### Dónde se usa

- En el ecommerce de la marca (web y app móvil)
- Específicamente en áreas de:
  - Navegación y búsqueda de catálogo
  - Gestión del carrito de la compra
  - Pago y confirmación de pedido
  - Seguimiento de envíos

### Información de Referencia

- **Propósito principal:** Automatizar y optimizar el proceso de venta de camisetas online
- **Owner/PM responsable:** Equipo Turing (Tech Lead: Ada Martín)
- **Repositorio:** `ejemplo/web-teeshop`
- **Área de Arquitectura:** Arquitectura de Ecommerce

---

## Funcionalidades y Casos de Uso Principales

### 1. Recomendación Dinámica de Productos

**Propósito**
Calcular automáticamente la recomendación más relevante para que cada cliente encuentre la camiseta que busca, adaptándose a sus preferencias reales.

**Quién lo usa**

- Sistema TeeShop (automáticamente)
- Clientes (indirectamente, ven los resultados)

**Cuándo se utiliza**

- Cada vez que un cliente navega por el catálogo
- Continuamente durante toda la sesión de compra (24/7)

**Cómo funciona**

1. El sistema TeeShop recibe una visita con un contexto (ej: categoría camisetas básicas)
2. Consulta el catálogo y el estado actual de todo el stock
3. Calcula automáticamente la recomendación óptima evitando productos agotados
4. Envía las sugerencias a la página de catálogo para mostrarlas al cliente
5. **Resultado:** El cliente ve recomendaciones ajustadas a su interés

**Beneficio / Valor para el negocio**

- ⏱️ **Reduce tiempos:** Las recomendaciones son automáticas, sin búsquedas innecesarias
- 🎯 **Aumenta precisión:** Los clientes encuentran el producto correcto
- 💰 **Reduce costos:** Menos abandono de carrito, flujo más eficiente
- 📈 **Aumenta conversión:** Más pedidos completados por hora

---

### 2. Adaptación en Tiempo Real a Cambios

**Propósito**
Detectar problemas en el catálogo (stock agotado, congestión de pagos) y recalcular automáticamente la disponibilidad para evitar interrupciones.

**Quién lo usa**

- Sistema TeeShop (automáticamente)
- Clientes (reciben avisos)

**Cuándo se utiliza**

- Cuando un producto se agota o se bloquea
- Cuando hay congestión en ciertas pasarelas de pago
- Cuando cambian los precios de los productos

**Cómo funciona**

1. Una camiseta se queda sin stock
2. TeeShop detecta instantáneamente que ese producto no está disponible
3. Recalcula automáticamente alternativas similares para el cliente
4. Evita que el cliente añada al carrito un producto agotado
5. **Resultado:** El flujo de compra continúa sin interrupciones

**Beneficio / Valor para el negocio**

- 🔧 **Reduce paradas:** El sistema se adapta automáticamente, no requiere intervención manual
- ⚡ **Respuesta rápida:** Las decisiones se toman en milisegundos
- 🛡️ **Previene errores:** Distribuye la demanda automáticamente
- 💼 **Operación sin interrupciones:** Mínimo impacto en ventas

**Duración estimada**
~Instantáneo (milisegundos)

---

### 3. Gestión de Estados de Pedidos

**Propósito**
Mantener un registro actualizado de dónde está cada pedido en todo momento y qué estado tiene.

**Quién lo usa**

- Sistema TeeShop
- Agentes de atención al cliente (para tracking)
- Sistema de analytics (para análisis)

**Cuándo se utiliza**

- Continuamente, para cada pedido de la tienda
- Cuando se necesita saber el estado de un pedido específico

**Cómo funciona**

1. Un cliente confirma un pedido
2. TeeShop registra su entrada y lo asigna a un estado inicial
3. A medida que avanza, TeeShop actualiza su estado en tiempo real
4. Cuando se entrega, TeeShop registra la salida y la entrega final
5. **Resultado:** Historial completo del recorrido del pedido

**Beneficio / Valor para el negocio**

- 📍 **Trazabilidad completa:** Saber dónde está cada pedido en cada momento
- 📊 **Datos para análisis:** Información para optimizar la operación
- 🔍 **Resolución de problemas:** Identificar dónde y cuándo ocurrieron incidencias
- ✅ **Auditoría:** Registro completo para cumplimiento

---

### 4. Comunicación con Sistemas Externos

**Propósito**
Enviar peticiones precisas a sistemas externos (pasarela de pago, almacén, mensajería) para que ejecuten cada paso del pedido según el proceso calculado.

**Quién lo usa**

- Sistema TeeShop
- Servicios/APIs externos

**Cuándo se utiliza**

- Continuamente durante la operación
- Cada vez que un pedido necesita avanzar de fase

**Cómo funciona**

1. TeeShop calcula que un pedido debe pasar de "pagado" a "preparado"
2. Determina qué sistema debe gestionarlo (ej: API de almacén)
3. Envía una petición a ese sistema con detalles precisos
4. El sistema ejecuta la petición
5. TeeShop recibe confirmación de que se ejecutó correctamente
6. **Resultado:** Avance preciso del pedido

**Beneficio / Valor para el negocio**

- 🎯 **Precisión:** Los sistemas saben exactamente qué hacer
- ⚡ **Eficiencia:** Sin tiempo perdido en decisiones
- 🔄 **Integración:** Los sistemas y la plataforma funcionan como uno
- 🛡️ **Confiabilidad:** Confirmación de que cada acción se completó

---

## 🔗 Documentación Técnica en GitHub o Wiki

> ⚠️ **Para developers, architects y personal técnico:**
> Toda la documentación técnica está centralizada en los repositorios del producto:

- **Front:** https://github.com/ejemplo/spa-teeshop/blob/develop/docs/readme.md
- **Back:** https://github.com/ejemplo/app-teeshop/blob/main/README.md#-documentation

---

## Conceptos Clave para el Usuario

### Pedido

**¿Qué es?:** Un conjunto de productos (camisetas) que un cliente compra en una misma transacción. Puede contener distintas tallas y modelos, y cada uno tiene un código único para identificarlo.

- **Por qué importa:** Es el elemento que TeeShop gestiona. Cada pedido tiene destinos y propiedades (talla, importe) que afectan cómo TeeShop lo maneja.
- **Ejemplo real:** Un pedido con 5 camisetas básicas que realiza un cliente de Madrid y necesita llegar a su domicilio.

### Tienda (Storefront)

**¿Qué es?:** Un canal específico del ecommerce dedicado a una tarea particular (ej: catálogo, carrito, checkout). Está compuesto por páginas y conexiones.

- **Por qué importa:** TeeShop funciona dentro de storefronts. Cada storefront tiene su propio mapa de páginas y flujos.
- **Ejemplo real:** La sección "Checkout" de la tienda online, donde se confirman los pedidos.

### Flujo

**¿Qué es?:** El recorrido que calcula TeeShop para que un pedido vaya de su estado actual a su estado final, pasando por pasos específicos.

- **Por qué importa:** Es lo que TeeShop calcula automáticamente. Un buen flujo = operación eficiente.
- **Ejemplo real:** Cliente entra en catálogo → carrito → pago → confirmación → envío.

### Paso / Punto

**¿Qué es?:** Una página o punto específico del ecommerce (ej: catálogo, carrito, pasarela de pago, confirmación). TeeShop identifica cada uno con un código.

- **Por qué importa:** Los flujos se componen de pasos. Necesitas entender dónde están los pasos para saber cómo avanzan los pedidos.
- **Ejemplo real:** `CHK3SB301` es un paso específico en el mapa del Checkout.

### API (Application Programming Interface)

**¿Qué es?:** Un punto de integración que conecta con un sistema externo (pago, almacén, mensajería). Ejecuta las peticiones que TeeShop envía.

- **Por qué importa:** Es lo que realmente procesa los pedidos. TeeShop habla con APIs para hacer que los sistemas externos actúen.
- **Ejemplo real:** La API de la pasarela de pago recibe una petición de TeeShop y cobra el pedido.

---

## Cómo Acceder

### Acceso Principal

- **Tipo:** Aplicación web (acceso de clientes y administradores)
- **Ubicación:** Desplegada en la nube (Cloud computing)
- **Disponibilidad:** 24/7
- **Requisitos:** Navegador moderno y conexión a internet

**Grafana:** Para visionado de métricas de seguimiento en nuestro portal de observabilidad de Grafana, accede a los dashboards aquí señalados:

- TeeShop Monitoring
- TeeShop per checkout step

### TeeShop Admin UI (Para Administradores)

Si necesitas administrar o monitorear TeeShop:

- **URL:** https://shop-europe.cloud.ejemplo.com/4/teeshop
- **Método de acceso:** Single Sign-On (SSO) con credenciales corporativas
- **Disponibilidad:** 24/7
- **Requisitos:** Navegador moderno (Chrome/Firefox), acceso a red corporativa, rol de administrador

### Primeros Pasos para Nuevo Usuario (Agente/Técnico)

1. Accede a la TeeShop Admin UI con tus credenciales
2. Navega a tu tienda específica en el menú principal
3. Visualiza el mapa de la tienda (layout) con todas las páginas
4. Observa los pedidos en tiempo real (estado, destino, importe)
5. Si necesitas intervenir, contacta al equipo de TeeShop Admin

---

## TeeShop Admin UI — Guía Visual

La interfaz de TeeShop Admin es donde administradores y técnicos pueden gestionar, monitorear y operar el sistema TeeShop. Aquí está lo que verás en cada sección:

### 1. Selección de Tiendas

**Pantalla inicial**

- Lista de todas las tiendas disponibles (ej: España, Portugal)
- Dentro de cada tienda, varias áreas o storefronts (Catálogo, Checkout, etc.)
- Seleccionas un storefront y entras a su panel de control

**Ejemplo:**

```
Tienda España
├── Storefront 1: Catálogo
└── Storefront 2: Checkout
```

### 2. Panel de Layout (El Mapa Visual)

Esta es la pantalla principal. Ves una representación visual de cómo está organizado el flujo del storefront.

**¿Qué ves?**

- **Nodos (puntos):** Cada página, entrada, salida, formulario o punto de espera
- **Conexiones (líneas):** Los flujos posibles entre páginas
- **Colores:** Verde (OK), Rojo (problema), Amarillo (seleccionado)

**Información de cada nodo:**

- Nombre/código (ej: `CHK3SB301`)
- Tipo (formulario, pago, catálogo, etc.)
- API asignada
- Estado actual
- Conexiones entrantes y salientes

**Ejemplo visual:**

```
[Catálogo] → [Carrito] → [Login] → [Pago] → [Confirmación] → [Envío]
```

### 3. Gestión de Versiones de Layout

**Versión Histórica**

- El layout es un documento versionado (como en Git)
- Ejemplo: v1, v2, v3, v4
- No puedes editar versiones antiguas (protección)
- Siempre hay una versión **ACTIVA** que es la que el sistema está usando ahora

**Modo Draft (Borrador)**

- Trabajas en un borrador antes de publicar
- Solo administradores pueden editar
- Una vez listo, lo publicas para crear una nueva versión oficial
- Luego lo activas para que entre en producción

**Flujo:**

```
Draft (edición) → Publicar (v5) → Activar (pasa a producción)
```

### 4. Edición de Layout (Modo Administrador)

Si tienes permisos, puedes editar y agregar elementos:

**Elementos que puedes agregar:**

- 📍 Página de Entrada (detecta clientes que llegan)
- 📍 Página de Espera (clientes en cola)
- 📍 Nodo Estándar (página o punto)
- 📍 Comando (acción especial)
- 📍 Punto de Salida (conexión con otro storefront)
- 📍 Carpetas (agrupación de nodos para mejor visualización)

**Cómo editar:**

1. Arrastra un elemento del panel izquierdo al layout
2. Haz clic en el nodo para ver/editar sus propiedades
3. Configura: nombre, código, API, destinos, etc.
4. Conecta nodos manualmente (arrastra línea) o en bloque
5. Organiza visualmente (alinea, expande, colapsa)
6. Guarda y publica cuando esté listo

**Propiedades de cada nodo:**

- **Step ID:** Identificador único
- **Alias:** Nombre legible
- **Descripción:** Para qué sirve
- **API Asignada:** Qué sistema lo procesa
- **Tipo:** Entrada, formulario, etc.
- **Destinos:** A dónde va si se completa, rechaza, o no se completa
- **Medidas:** Importe, peso, unidades (si aplica)

**Edición en bloque:**

- Selecciona múltiples nodos (Ctrl+Click)
- Edita sus propiedades juntos
- Cambia tipo, API, conexiones en masa
- Alinea visualmente (izquierda, derecha, arriba, abajo)

### 5. Vista Técnica (Lectura - Sin Edición)

Si tienes rol de técnico (solo lectura):

**Verás:**

- El layout completo con todos los nodos
- Propiedades de cada nodo
- Conexiones entre ellos
- Estado visual en tiempo real

**Dos modos de visualización:**

**A) Modo Gráfico (Visual)**

- Ves el mapa visual del layout
- Haz clic en nodos para ver detalles
- Los nodos ocultos se muestran en sombra

**B) Modo Tabla**

- Todos los nodos en una tabla
- Columnas: Nombre, Tipo, API, Descripción, Medidas, etc.
- Útil para revisar configuraciones
- Pestaña "Edges" para ver conexiones

### 6. Filtros para Diagnóstico

**Filtro por API**

- Selecciona una API específica
- Todos los nodos que NO pertenecen a esa API se oscurecen
- **Uso:** Identificar qué nodos afecta si una API falla

**Ejemplo:**

```
Si la API 009 (pago) se cae:
Filtras por 009 → Ves todos los nodos que dependen de ella
→ Entiendes qué parte del checkout se verá afectada
```

**Filtro por Nodos**

- Selecciona nodos problemáticos
- Se destacan en el layout
- Ves sus conexiones inmediatas
- **Uso:** Debuggear problemas específicos reportados

**Ejemplo:**

```
Se reporta problema en nodos 022 y 023
→ Filtras por ellos
→ Ves que están conectados con ciertas pasarelas de pago
→ Sabes dónde buscar el problema
```

---

## Roles y Permisos

### ¿Qué puedo hacer según mi rol?

| Mi Rol | Puedo acceder | Puedo hacer |
|---|---|---|
| Cliente | Sí (indirecto) | Ver el catálogo de TeeShop, recibir recomendaciones, reportar problemas |
| Agente de Atención | Sí | Visualizar mapa, monitorear pedidos, ver alertas, reportar problemas |
| Técnico de Mantenimiento | Sí | Conectar/desconectar APIs, ejecutar diagnósticos, reportar fallos |
| Store Manager | Sí | Administrar layout, ver reportes, gestionar configuración |
| TeeShop Admin | Sí | Acceso completo (layout, configuración, diagnósticos, métodos directos) |
| Data Analytics | Sí | Consultar datos de TeeShop en la Data Platform |

---

## Soporte y Ayuda

### ¿Dónde pido ayuda?

Sigue esta guía para cualquier duda o petición al equipo:
https://arquitectura-ecommerce.docs.ejemplo.com/docs/6/working-agreements#flujo-de-trabajo-ante-nuevas-peticiones

---

## Roadmap y Cambios Futuros

Puedes consultar todas las iniciativas en nuestro board de Github Issues:
https://github.com/orgs/ejemplo/projects/509
