Wiki de Pets-Obsidian
¡Bienvenido a la documentación oficial de Pets-Obsidian! Esta guía te ayudará a instalar, configurar y usar todas las funcionalidades que ofrece este plugin de mascotas.

1. Introducción
Pets-Obsidian es un plugin avanzado de mascotas que permite a los jugadores comprar, coleccionar y personalizar mascotas cosméticas que los siguen por el mundo. Cada mascota puede tener efectos pasivos, efectos de combate, partículas personalizadas y mucho más.

Características Principales:

Mascotas como Cabezas Flotantes: Las mascotas son cabezas personalizadas que siguen al jugador.

Sistema de Tienda: Los jugadores pueden comprar mascotas usando una economía basada en Vault.

Menús Interactivos (GUI): Interfaces gráficas para gestionar y seleccionar mascotas.

Personalización: Cambia el nombre, las partículas y el estilo de seguimiento de tus mascotas.

Efectos Pasivos y de Combate: Las mascotas pueden otorgar efectos de poción al dueño o aplicar efectos negativos a los enemigos al golpear.

Integración con Plugins: Compatible con Vault, PlaceholderAPI y WorldGuard.

2. Instalación
Descarga el archivo Pets-Obsidian.jar.

Coloca el archivo .jar en la carpeta plugins de tu servidor.

Dependencias: Asegúrate de tener los siguientes plugins instalados:

Vault

Un plugin de economía compatible con Vault (ej. EssentialsX, CMI).

(Opcional) Para funcionalidades adicionales, instala:

PlaceholderAPI

WorldGuard

Reinicia o recarga tu servidor. La primera vez que se inicie, se generará la carpeta Pets-Obsidian con los archivos de configuración.

3. Comandos y Permisos
El comando principal es /pet (o sus alias /pets, /mascota).

Comando

Descripción

Permiso

/pet

Abre el menú principal de mascotas.

(Ninguno)

/pet shop

Abre la tienda para comprar mascotas.

(Ninguno)

/pet spawn <id>

Invoca una de tus mascotas.

(Requiere poseer la mascota)

/pet remove

Guarda tu mascota activa.

(Ninguno)

/pet info <id>

Muestra información sobre una mascota.

(Ninguno)

/pet reload

Recarga la configuración del plugin.

pet.admin.reload

/pet give <jugador> <id>

Da un invocador de mascota a un jugador.

pet.admin.give

/pet delete <jugador> <id>

Elimina una mascota de la colección de un jugador.

pet.admin.delete

4. Configuración
4.1. config.yml
Este es el archivo de configuración principal. Aquí puedes modificar los mensajes del plugin y algunas configuraciones generales.

prefix: "&d&lPets &8» &r"
shop:
  enabled: true
pet-settings:
  follow-distance: 1.5 # Distancia a la que la mascota sigue al jugador
  follow-height-offset: 1.2 # Altura de la mascota respecto a los pies del jugador
messages:
  no-permission: "&cNo tienes permiso para ejecutar este comando."
  # ... y otros mensajes personalizables

4.2. Crear una Mascota Nueva
Para crear una nueva mascota, simplemente crea un nuevo archivo .yml dentro de la carpeta plugins/Pets-Obsidian/pets/. Por ejemplo, mi_mascota.yml.

Aquí tienes una plantilla con todas las opciones disponibles:

# ID único de la mascota. Debe coincidir con el nombre del archivo.
id: "mi_mascota"

# (true/false) Si la mascota aparecerá en la tienda.
shop: true

# Nombre que se mostrará en los menús y sobre la cabeza de la mascota.
# Soporta códigos de color (&) y hexadecimales (&#RRGGBB).
display-name: "&#FF0000Mascota de Fuego"

# (true/false) Si el nombre se mostrará sobre la cabeza de la mascota en el juego.
show-display-name: true

# Descripción que aparece en los menús.
lore:
  - "&7Una mascota ardiente que te otorga"
  - "&7el poder del fuego."

# Tipo de cabeza. Puede ser "base64" o "player".
head-type: "base64"

# Textura de la cabeza.
# Si head-type es "base64", pon la textura de Minecraft-Heads.com aquí.
# Si head-type es "player", pon el nombre de un jugador aquí.
head-texture: "eyJ0ZXh0dXJlcyI6eyJTS0lOIjp7InVybCI6Imh0dHA6Ly90ZXh0dXJlcy5taW5lY3JhZnQubmV0L3RleHR1cmUvYjU4ODJlY2Y2Y2U1ZjY1MjY0YjU1ZTIxY2U0OTM3ODM0YjRkM2Q0ODRkNzllYjY3MThjM2M0ZGNjYjA1ZDAifX19"

# Precio en la tienda. Si es 0, la compra será gratuita.
price: 500.0

# Permiso necesario para comprar y usar la mascota.
# Si se deja en blanco o se omite, no se necesita ningún permiso.
permission: "pet.use.mi_mascota"

# Efectos de poción pasivos que se aplican al dueño de la mascota.
# Formato: "TIPO_DE_EFECTO:AMPLIFICADOR"
effects:
  - "SPEED:0" # Velocidad I
  - "FIRE_RESISTANCE:0" # Resistencia al Fuego I

# Efectos de poción que se aplican al enemigo cuando el dueño de la mascota lo golpea.
# Formato: "TIPO_DE_EFECTO:AMPLIFICADOR:DURACION_EN_SEGUNDOS"
on-hit-effects:
  - "WITHER:1:5" # Wither II por 5 segundos

# Cooldown en ticks (20 ticks = 1 segundo) para los efectos de on-hit-effects.
on-hit-cooldown: 200 # 10 segundos

# Configuración de las partículas de la mascota.
particles:
  enabled: true
  type: "FLAME" # Tipo de partícula de Minecraft.
  amount: 5 # Cantidad de partículas por ciclo.

5. Integraciones
5.1. Vault
Si tienes Vault y un plugin de economía, el sistema de precios de la tienda se activará automáticamente. Los jugadores necesitarán tener el dinero especificado en el .yml de la mascota para poder comprarla.

5.2. PlaceholderAPI
Si tienes PlaceholderAPI, puedes usar los siguientes placeholders:

%pet_active%: Devuelve "Sí" o "No" si el jugador tiene una mascota activa.

%pet_name%: Devuelve el nombre de la mascota activa.

%pet_id%: Devuelve el ID de la mascota activa.

5.3. WorldGuard
Si tienes WorldGuard, puedes usar la siguiente flag en tus regiones:

Flag: permitted-pets

Valores:

allow (por defecto): Las mascotas están permitidas en la región.

deny: Las mascotas no están permitidas. Los jugadores no podrán invocar mascotas en la región y las mascotas activas se ocultarán al entrar.

Ejemplo de uso:
/rg flag mi_region permitted-pets deny - Esto bloqueará el uso de mascotas en la región "mi_region".

6. Menús (GUI)
Menú Principal (/pet)
Se abre al ejecutar el comando /pet. Desde aquí puedes acceder a tus mascotas o a la tienda.

Tienda (/pet shop)
Aquí puedes ver todas las mascotas disponibles para comprar. El lore de cada ítem te indicará si ya la posees, si está disponible o si está bloqueada por falta de permisos.

Mis Mascotas
Muestra todas las mascotas que has comprado o que te han dado. Al hacer clic en una, se abre el menú de gestión.

Gestionar Mascota
Este es el menú más importante para personalizar tu mascota.

Cambiar Nombre: Te permite asignarle un apodo personalizado a tu mascota.

Cambiar Partículas: Te permite elegir un nuevo efecto de partícula para tu mascota.

Activar/Desactivar Nombre: Muestra u oculta el nombre sobre la cabeza de la mascota.

Estilo de Seguimiento: Cambia cómo te sigue la mascota (a la derecha, a la izquierda, detrás o sobre tu cabeza).

Activar/Desactivar Partículas: Activa o desactiva las partículas de la mascota.

Invocar/Guardar Mascota: Te permite sacar o guardar tu mascota.
