# Uv y Zensical

Guía para instalar `uv`, configurar **Zensical**, levantar el servidor de desarrollo y aprovechar la recarga en tiempo real.

---

## ¿Qué son uv y Zensical?

### `uv`

`uv` es un gestor de paquetes y proyectos para Python desarrollado por **Astral**, una empresa que desarrolla herramientas para el ecosistema de Python. Está escrito en Rust, lo que le permite resolver e instalar dependencias considerablemente más rápido que herramientas tradicionales como `pip`, `pip-tools`, `virtualenv`, `pyenv` o `Poetry`. De hecho, su objetivo es sustituir a todas ellas con una sola herramienta unificada.

### Zensical

**Zensical** es un generador de sitios estáticos pensado específicamente para documentación técnica, desarrollado por el mismo equipo de **MkDocs**. Toma archivos Markdown organizados en carpetas y los convierte en un sitio web navegable, con tema visual, barra de búsqueda y estructura de navegación configurables desde un único archivo central (`zensical.toml`).

Es la herramienta sobre la que trabaja toda esta guía:

---

## Paso 1: Instalar `uv`

`uv` es un gestor de paquetes y entornos de Python, abre tu terminal y ejecuta:

```
curl -sSf https://astral.sh/uv/install.sh | sh
```

> **Nota:** Tras completar la instalación, cierra y vuelve a abrir tu terminal para asegurarte de que el comando `uv` está disponible.

**Comprobar la ruta del ejecutable:**
   
```
which uv
```
*(Debería apuntar habitualmente a `~/.cargo/bin/uv` o `~/.local/bin/uv`)*

---

## Paso 2: Crear la carpeta del proyecto e inicializarlo

Crea un directorio para tu proyecto y entra en él:

```
mkdir mi-proyecto-docs
cd mi-proyecto-docs
```

A continuación, inicializa el proyecto con `uv`:

```
uv init
```

---

## Paso 3: Añadir la dependencia de Zensical

Instala **Zensical** dentro de tu proyecto mediante `uv`:

```
uv add zensical
```

`uv` gestionará automáticamente la descarga e instalación del paquete en el entorno virtual del proyecto.

> **Nota:** Para asegurarte de que Zensical solo se instale como herramienta de desarrollo (y no en el entorno de producción), utiliza la bandera `--dev`:

```
uv add --dev zensical
```

*Esto registrará `zensical` bajo el bloque `[tool.uv.dev-dependencies]` o `[dependency-groups]` en tu archivo `pyproject.toml`.*

---

## Paso 4: Levantar el servidor local

Para compilar la documentación y poner en marcha el servidor web de desarrollo, ejecuta:

```
uv run zensical serve
```

Verás una salida en la terminal indicando la dirección URL local, normalmente:

http://127.0.0.1:8000

Abre esa URL en tu navegador preferido para ver el sitio web generado.

---

## Paso 5: Edición y actualización en tiempo real (Live Reload)

El servidor de desarrollo de Zensical cuenta con un motor de recarga en tiempo real:

1. **Abre y edita:** Modifica cualquier archivo `.md` en tu editor de código.
2. **Guarda los cambios:** Al guardar el archivo, el servidor detectará la modificación de inmediato.
3. **Sincronización instantánea:** La página web abierta en el navegador reflejará los cambios automáticamente sin necesidad de recargar manualmente la página.
