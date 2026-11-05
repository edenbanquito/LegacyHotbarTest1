# Hotbar Only (Fabric 1.21.1)

El inventario del jugador queda reducido a la **hotbar**, como en los minijuegos de Legacy Console Edition (p. ej. Tumble). Siempre activo, sin configuración.

## Qué hace

- Los slots 9..35 del inventario (la mochila) se **ocultan y bloquean** en todas las pantallas que muestren el inventario del jugador (inventario, cofres, mesas de crafteo, yunques, etc.).
- Los objetos recogidos solo pueden ir a la hotbar; si está llena, no caben.
- Armadura y mano secundaria siguen funcionando normal.
- Al entrar/reaparecer, lo que hubiera en la mochila se pasa a huecos libres de la hotbar. Lo que no quepa **no se borra**, solo queda inaccesible.

## Compatibilidad con Legacy4J

Legacy4J dibuja los slots y navega (ratón/mando) respetando `Slot#isActive()`. Este mod engancha ahí
(`SlotMixin`) y además bloquea `mayPlace`/`mayPickup` en cliente y servidor. Usa mappings oficiales de
Mojang, los mismos que Legacy4J. Además hay una red de seguridad en `AbstractContainerScreen`
(`renderSlot`/`slotClicked`) para pantallas de otros mods.

## Compilar

Requisitos: JDK 21 y Gradle 8.10+ (o abre la carpeta en IntelliJ y deja que importe el proyecto).

```
gradle wrapper --gradle-version 8.12   # solo la primera vez
./gradlew build
```

El `.jar` queda en `build/libs/` (usa el que NO termina en `-sources`). Ponlo en `mods/` junto con
Fabric API y Legacy4J (versión para 1.21.1).

Si alguna versión de `gradle.properties` (loader / Fabric API) no existe, cámbiala por la última
disponible para 1.21.1.

## Cómo se ve

Sin hueco: la hotbar sube a donde estaba la primera fila de la mochila y el panel se hace más bajito
(inventario, cofres, hornos, dispensadores, tolvas, shulkers...). En las pantallas anchas de Legacy4J
(crafteo, telar, cortapiedras, aldeanos) el panel no se encoge porque ocupan todo su alto con otras cosas,
pero la mochila desaparece y la hotbar queda pegada donde empezaba.

## Notas

- Escrito contra el código de Legacy4J rama 1.21 (1.7.x). Si usas otra versión y alguna pantalla se ve mal,
  dime cuál y la ajusto.
- En pantallas de vanilla sin Legacy4J los slots se ocultan, pero la textura del fondo es fija y no se encoge.
- Instalar el mod solo en el cliente o solo en el servidor funciona, pero lo ideal es en ambos.
