# Transcripción — Demo de Producto: Gymshark Training & Community App

**Fecha:** 25 de junio de 2026
**Hora:** 10:00 – 11:05
**Lugar:** Sala virtual (Google Meet)
**Tipo de reunión:** Demo Review / Sprint Review

## Asistentes

- **Marcus Reid** — Frontend Developer (presenta la demo)
- **Lena Howard** — Product Manager
- **Sofía Quintana** — UX/UI Designer
- **David Okafor** — Backend Developer
- **Priya Nair** — QA Engineer
- **Tom Becker** — Tech Lead

---

## Transcripción

**[10:00] Lena (PM):** Buenos días a todos. Hoy Marcus nos va a enseñar la demo de la nueva versión de la app de entrenamiento y comunidad de Gymshark. Marcus, cuando quieras, comparte pantalla y nos cuentas qué has preparado.

**[10:01] Marcus (Frontend):** Perfecto, gracias Lena. Comparto pantalla… ¿se ve bien? Genial. Pues hoy os traigo el flujo completo de la nueva sección **"Train"** integrada con la parte de **comunidad**. Os recuerdo el contexto: Gymshark no solo vende ropa deportiva, sino que ha apostado por productos digitales —planes de entrenamiento, retos y contenido exclusivo— para fidelizar a los clientes. Esta app es justamente ese producto digital.

**[10:02] Marcus:** Empiezo por el **onboarding**. Cuando el usuario abre la app por primera vez, le mostramos un flujo de cuatro pantallas donde recogemos sus objetivos (ganar músculo, perder grasa, mejorar resistencia), su nivel de experiencia y los días que puede entrenar a la semana. Con esa información, el sistema genera una recomendación inicial de plan.

**[10:03] Sofía (UX):** Marcus, ¿el onboarding se puede saltar?

**[10:03] Marcus:** Sí, buena pregunta. Hay un botón "Skip for now" en la esquina superior derecha. Si lo pulsa, le asignamos un plan genérico por defecto y guardamos un flag para volver a sugerirle completar el perfil más adelante. A nivel técnico, ese estado lo persistimos en el backend a través del endpoint `POST /api/v1/users/onboarding` y también lo cacheamos en local con AsyncStorage para no bloquear al usuario si hay problemas de red.

**[10:04] Marcus:** Vamos a la **pantalla principal de Train**. Aquí el usuario ve su plan activo, el entrenamiento del día y su progreso semanal. Funcionalmente, lo importante es que esta vista se adapta según el momento del día y según si el usuario ya ha completado o no la sesión de hoy.

**[10:05] Marcus:** A nivel técnico, esta pantalla está construida con **React Native** y **TypeScript**. El estado de la pantalla lo gestionamos con **Redux Toolkit**, y las llamadas a la API las hacemos con **RTK Query**, que nos da el caching y la invalidación automática. El plan del día lo pedimos al endpoint `GET /api/v1/training/today` y se cachea durante 5 minutos para evitar llamadas innecesarias.

**[10:06] Tom (Tech Lead):** ¿Has resuelto ya el tema del refetch cuando el usuario completa una sesión?

**[10:06] Marcus:** Sí, Tom. Cuando se marca una sesión como completada, disparo una mutation `completeSession` que invalida el tag `TodayWorkout`, así RTK Query refresca automáticamente la vista sin que tenga que hacer un pull-to-refresh manual. Lo veréis en un momento cuando complete el entrenamiento.

**[10:07] Marcus:** Entro en el **detalle de un entrenamiento**. Aquí se ve la lista de ejercicios, las series, repeticiones y los tiempos de descanso. Cada ejercicio tiene un vídeo demostrativo. Funcionalmente, el usuario puede registrar el peso que ha levantado en cada serie y la app guarda ese histórico para mostrar la progresión.

**[10:08] Marcus:** Los vídeos los servimos desde un CDN, en concreto **Cloudflare Stream**, y usamos lazy loading: solo cargamos el vídeo cuando el ejercicio entra en el viewport, usando un componente con `IntersectionObserver` adaptado a React Native con `onViewableItemsChanged` de la FlatList. Esto nos ha bajado bastante el consumo de datos y mejora el tiempo de carga inicial.

**[10:09] Priya (QA):** ¿Qué pasa si el usuario pierde conexión a mitad de un entrenamiento?

**[10:09] Marcus:** Muy buena, Priya, porque es uno de los casos que más he trabajado. Tenemos un modo **offline-first** para la sesión activa. Cuando empiezas un entrenamiento, descargamos toda la sesión en local. Los registros de series y pesos se guardan en una cola local con **WatermelonDB**, y cuando se recupera la conexión, sincronizamos con el backend mediante un proceso de sync que envía los cambios pendientes al endpoint `POST /api/v1/training/sessions/sync`. Si hay conflicto, gana siempre el dato del cliente porque es el que refleja lo que el usuario hizo realmente en el gimnasio.

**[10:11] Marcus:** Voy a completar una serie para que lo veáis… registro 60 kilos, 10 repeticiones… marco la serie como hecha. Fijaos que el indicador de progreso se actualiza al instante; eso es optimistic update. Hago el update en local inmediatamente y, si la llamada al backend falla, hago rollback del estado.

**[10:12] David (Backend):** Confirmo que el endpoint de sync ya está desplegado en el entorno de staging y soporta el envío en batch.

**[10:12] Marcus:** Perfecto, gracias David. Ahora paso a la parte de **comunidad**, que es la otra gran pata del producto.

**[10:13] Marcus:** La sección **"Community"** es un feed social donde los usuarios comparten sus entrenamientos, sus logros y participan en retos. Funcionalmente, el usuario puede publicar un post con texto, imágenes y opcionalmente vincular un entrenamiento que ha completado. También puede dar like, comentar y seguir a otros usuarios.

**[10:14] Marcus:** El feed es un scroll infinito con paginación. Técnicamente uso una **FlatList** optimizada con `getItemLayout` para evitar recálculos de layout, y paginación basada en cursor contra el endpoint `GET /api/v1/community/feed?cursor=...`. Uso paginación por cursor en lugar de offset porque el feed cambia constantemente y el cursor nos evita duplicados o saltos cuando se insertan posts nuevos.

**[10:15] Sofía (UX):** ¿Las imágenes del feed están optimizadas? En la versión anterior iban algo lentas.

**[10:15] Marcus:** Sí, ese era un punto débil. Ahora servimos imágenes responsive desde el CDN: pedimos la resolución adecuada según el tamaño del dispositivo y la densidad de pantalla. Además usamos `FastImage` en lugar del componente Image nativo, que nos da mejor caching en disco y memoria. El placeholder es un blurhash que se renderiza mientras carga la imagen real, así la transición es suave.

**[10:16] Marcus:** Os enseño los **retos (Challenges)**. Esta es una funcionalidad clave de fidelización. Un reto es una meta colectiva o individual con una duración determinada —por ejemplo, "30 días de entrenamiento" o "Corre 50 km este mes"—. El usuario se une, va registrando su progreso y ve un ranking con otros participantes.

**[10:17] Marcus:** Funcionalmente, cuando completas actividades que cuentan para el reto, tu progreso se actualiza automáticamente. Al terminar el reto, si cumples el objetivo, desbloqueas recompensas: contenido exclusivo, descuentos en la tienda de Gymshark o badges digitales.

**[10:18] Marcus:** Técnicamente, el ranking en tiempo real es lo más interesante de esta parte. Mantenemos una conexión **WebSocket** para recibir las actualizaciones del leaderboard sin tener que hacer polling. Cuando otro participante avanza, el backend nos empuja el evento y actualizamos la posición en el ranking con una animación. Si el WebSocket se cae, tenemos un fallback a polling cada 30 segundos para no dejar la vista desactualizada.

**[10:19] Tom (Tech Lead):** ¿Cómo gestionas la reconexión del WebSocket?

**[10:19] Marcus:** Con un backoff exponencial. Empiezo intentando reconectar al segundo, luego a los dos, cuatro, ocho… hasta un máximo de 30 segundos entre intentos. Y cuando la app vuelve a primer plano desde background, fuerzo una reconexión inmediata y un refetch del estado del leaderboard para asegurar que los datos están frescos.

**[10:20] Marcus:** Os enseño el **contenido exclusivo**. Es la sección donde los miembros tienen acceso a vídeos de entrenadores, recetas, artículos y planes premium. El acceso depende del tipo de membresía del usuario.

**[10:21] Marcus:** A nivel técnico, el control de acceso lo gestionamos con un sistema de feature flags y entitlements que vienen del backend en el perfil del usuario. La UI se adapta: si un contenido es premium y el usuario no tiene la membresía, mostramos un paywall en lugar del contenido. Nunca confiamos solo en el frontend para esto; el backend valida siempre el acceso cuando se pide el contenido real, el frontend solo decide qué mostrar visualmente.

**[10:22] Priya (QA):** ¿El paywall lo habéis probado con los distintos tipos de membresía?

**[10:22] Marcus:** Sí, tenemos usuarios de prueba para cada tier: free, premium y premium plus. En QA podéis usar las cuentas que dejé documentadas en Confluence. He cubierto los tres casos en la demo de hoy con la cuenta premium.

**[10:23] Marcus:** Para cerrar la parte funcional, os comento la **integración con la tienda**. Desde la app, en ciertos puntos —por ejemplo al completar un reto— mostramos productos recomendados de Gymshark y un descuento. Al pulsar, abrimos el flujo de compra. Esto conecta el producto digital con el negocio principal de venta de ropa, que es justo la estrategia de fidelización.

**[10:24] Marcus:** Técnicamente, la recomendación de productos la pedimos a `GET /api/v1/shop/recommendations` pasando el contexto —por ejemplo, el reto completado— y el backend nos devuelve los productos relevantes. El deep link a la tienda lo gestionamos con React Navigation y un esquema de deep linking, de forma que si el usuario tiene la app de tienda principal instalada, puede saltar a ella, y si no, abrimos el flujo web embebido.

**[10:25] Marcus:** Un par de notas técnicas transversales antes de pasar a preguntas. La app está internacionalizada con **i18n**, soportamos ahora mismo inglés, español y alemán. La accesibilidad la hemos cuidado con labels de accesibilidad en todos los componentes interactivos y soporte para lectores de pantalla. Y en cuanto a calidad, tenemos tests unitarios con **Jest** y **React Native Testing Library**, y tests end-to-end con **Detox** para los flujos críticos: onboarding, completar entrenamiento y unirse a un reto.

**[10:27] Marcus:** El rendimiento lo monitorizamos con **Sentry** para errores y con **Firebase Performance** para métricas de carga. Desde la última optimización, el tiempo de arranque en frío bajó de 3,2 a 1,9 segundos en gama media. Y con esto cierro. ¿Preguntas?

**[10:28] Lena (PM):** Muy completo, Marcus. ¿El flujo de retos está listo para producción o falta algo?

**[10:28] Marcus:** Funcionalmente está completo. Me queda pulir la animación del leaderboard en dispositivos antiguos, donde va un poco a tirones, y David tiene que confirmar que el endpoint de recompensas está finalizado.

**[10:29] David (Backend):** El endpoint de recompensas lo cierro esta semana. Te aviso en cuanto esté en staging.

**[10:29] Tom (Tech Lead):** Por mi parte, buen trabajo con el offline-first y la sincronización. Revisemos juntos la estrategia de resolución de conflictos antes de pasar a producción, quiero asegurarme de que cubrimos el caso de multi-dispositivo.

**[10:30] Marcus:** Perfecto, lo agendamos. Anoto resolución de conflictos multi-dispositivo como pendiente.

**[10:31] Sofía (UX):** A mí me ha encantado cómo ha quedado el blurhash en el feed. Solo pediría revisar el contraste del paywall, creo que el botón secundario se ve poco.

**[10:31] Marcus:** Anotado, Sofía. Ajusto el contraste del botón del paywall.

**[10:32] Priya (QA):** Yo empiezo hoy mismo con la batería de pruebas de los retos y el offline. Te paso incidencias por Jira si encuentro algo.

**[10:32] Lena (PM):** Genial. Pues resumo acciones: Marcus pule la animación del leaderboard y el contraste del paywall; David cierra el endpoint de recompensas; Tom y Marcus revisan conflictos multi-dispositivo; Priya arranca QA. Gracias a todos, muy buena demo.

**[10:33] Marcus:** Gracias a vosotros. Subo la build a la plataforma de testing para que todos podáis probarla. ¡Nos vemos!

---

## Resumen de Acciones (Action Items)

| # | Acción | Responsable | Estado |
|---|--------|-------------|--------|
| 1 | Pulir animación del leaderboard en dispositivos antiguos | Marcus | Pendiente |
| 2 | Ajustar contraste del botón secundario del paywall | Marcus | Pendiente |
| 3 | Finalizar endpoint de recompensas de retos | David | En curso |
| 4 | Revisar estrategia de resolución de conflictos multi-dispositivo | Tom + Marcus | Pendiente |
| 5 | Ejecutar batería de pruebas de retos y modo offline | Priya | En curso |
| 6 | Subir build a la plataforma de testing | Marcus | Hecho |
