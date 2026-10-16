![MOMENTUM · Hackatón de DRL · SAIL-UGR · Universidad de Granada](workspace/img/banner-hackaton.jpg)

# MOMENTUM · Hackatón de DRL

Material y entorno de trabajo para el **hackatón presencial** de MOMENTUM, centrado en **aprendizaje por refuerzo profundo** (DRL). Entrenarás agentes que conducen en el simulador [`highway-env`](https://highway-env.farama.org/) con [Gymnasium](https://gymnasium.farama.org/), [Stable-Baselines3](https://stable-baselines3.readthedocs.io/) y [Optuna](https://optuna.org/).

**Requisitos previos:** la fase 1 del curso (los webinarios de Python). Sus notebooks están en [`workspace/repaso/`](workspace/repaso/) por si quieres repasar (incluidos los de RL con Stable-Baselines3).

## Elige cómo trabajar

| Opción | Qué necesitas | Recomendada si… |
|---|---|---|
| [**A · Docker**](#opción-a--docker-recomendada) | Docker instalado | Quieres el entorno listo, idéntico al del aula |
| [**B · GitHub Codespaces**](#opción-b--github-codespaces) | Una cuenta de GitHub | No puedes o no quieres instalar nada |
| [**C · Tu propio Python**](#opción-c--tu-propio-python) | Python 3.10 o superior | Ya tienes Python y prefieres tu editor |

Las tres opciones usan exactamente los mismos notebooks.

## Opción A · Docker (recomendada)

Instala [Docker Desktop](https://docs.docker.com/get-docker/) (Windows, macOS) o Docker Engine (Linux) y comprueba que está en marcha. Después, en una terminal:

```bash
docker run -d --name momentum-drl-hackaton -p 8080:8080 -v momentum-drl-hackaton:/home/coder/workspace ghcr.io/ugr-sail/momentum-drl-hackaton:latest
```

La primera vez descarga la imagen, que incluye PyTorch y tarda algo más que la de la fase 1. **Descárgala antes de llegar al hackatón**: la red del aula la compartiréis todos. Cuando termine:

1. Abre <http://localhost:8080> en el navegador.
2. Introduce la contraseña `curso2026`.
3. Empieza por `ejemplos/01_entornos.ipynb`. Si te pide un kernel, elige **Python (curso)**.

Verás VS Code en el navegador con Python, Jupyter y todas las librerías ya instaladas. Tu trabajo (notebooks y agentes guardados) se guarda en el volumen `momentum-drl-hackaton` y se conserva aunque apagues el ordenador.

| Quiero… | Comando |
|---|---|
| Detener el entorno | `docker stop momentum-drl-hackaton` |
| Volver a arrancarlo | `docker start momentum-drl-hackaton` |
| Empezar de cero con el material original | `docker rm -f momentum-drl-hackaton && docker volume rm momentum-drl-hackaton` y repetir el `docker run` |
| Actualizar a la última versión | `docker pull ghcr.io/ugr-sail/momentum-drl-hackaton:latest` y empezar de cero (⚠️ borra tu trabajo: descarga antes los notebooks y agentes que quieras conservar con clic derecho → *Download*) |

<details>
<summary>Alternativa con Docker Compose y los notebooks en tu carpeta</summary>

Si prefieres que los notebooks y los agentes estén en una carpeta de tu equipo (por ejemplo, para entregarlos o hacer copias), descarga este repositorio (botón **Code → Download ZIP**, o `git clone`) y, dentro de la carpeta:

```bash
docker compose up -d
```

Abre <http://localhost:8080> (contraseña `curso2026`). Lo que hagas queda en la carpeta `workspace/`. Para detenerlo: `docker compose down`.

</details>

<details>
<summary>Problemas frecuentes</summary>

- **`port is already allocated`:** otro programa usa el puerto 8080 (¿tienes en marcha el contenedor de la fase 1? Detenlo con `docker stop momentum-drl`). También puedes cambiar `-p 8080:8080` por `-p 8081:8080` y abrir <http://localhost:8081>.
- **`The container name "/momentum-drl-hackaton" is already in use`:** ya lo creaste antes. Usa `docker start momentum-drl-hackaton`.
- **`Cannot connect to the Docker daemon`:** Docker no está en marcha. Abre Docker Desktop y espera a que arranque.
- **El entrenamiento va muy lento:** Docker Desktop limita la CPU y la memoria. Súbelas en *Settings → Resources*.

</details>

## Opción B · GitHub Codespaces

[![Abrir en GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/ugr-sail/momentum-drl-hackaton)

Pulsa el botón (o *Code → Codespaces → Create codespace* en esta página). Se abre VS Code en el navegador con todo instalado; la primera vez tarda unos minutos. Las cuentas personales de GitHub incluyen horas gratuitas al mes.

Para recuperar un notebook original, ejecuta `git restore workspace/` en la terminal.

## Opción C · Tu propio Python

Descarga este repositorio (**Code → Download ZIP**, o `git clone https://github.com/ugr-sail/momentum-drl-hackaton`) y, dentro de la carpeta:

```bash
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
python -m ipykernel install --user --name curso-python --display-name "Python (curso)"
jupyter lab workspace
```

También puedes abrir la carpeta con VS Code (extensiones *Python* y *Jupyter*) o, si tienes Docker y la extensión *Dev Containers*, elegir *Reopen in Container*.

## Contenido

**Material didáctico**, en [`workspace/ejemplos/`](workspace/ejemplos/):

| Notebook | Contenido |
|---|---|
| [`01_entornos`](workspace/ejemplos/01_entornos.ipynb) | Entornos de Gymnasium y el simulador `highway-env` |
| [`02_agentes`](workspace/ejemplos/02_agentes.ipynb) | Agentes con Stable-Baselines3: entrenar, evaluar y guardar; *callbacks* y ajuste de hiperparámetros con Optuna |
| [`03_wrappers`](workspace/ejemplos/03_wrappers.ipynb) | *Wrappers* para modificar y ampliar el comportamiento de los entornos |

**Notebooks del reto**, en [`workspace/`](workspace/):

| Notebook | Para qué sirve |
|---|---|
| [`train`](workspace/train.ipynb) | Entrenar tus agentes. Guarda el mejor en `workspace/agentes/` |
| [`test`](workspace/test.ipynb) | Evaluar un agente guardado con las mismas condiciones para todos los equipos |

**Repaso de la fase 1**, en [`workspace/repaso/`](workspace/repaso/): los notebooks de Python de los webinarios, con sus soluciones, y los de aprendizaje por refuerzo con Stable-Baselines3 en `workspace/repaso/rl/stable-baselines/`.

## Cómo trabajar con los notebooks

- Ejecuta una celda con **Mayús + Intro**. Ejecuta las celdas **en orden**, de arriba abajo.
- Si aparece un `NameError`, probablemente te saltaste una celda anterior: usa *Run All* (ejecutar todo) o reinicia el kernel y vuelve a empezar desde arriba.
- En `train` y `test`, respeta las variables marcadas como fijas: son las mismas para todos los equipos.

## Licencia y autoría

Contenido didáctico bajo [CC BY 4.0](LICENSE-CONTENT.md); código y configuración bajo [MIT](LICENSE).

Miguel Molina-Solana, Juan Gómez-Romero, Ahmed Brek-Prieto y Antonio Manjavacas-Lucas · [SAIL-UGR research group](https://github.com/ugr-sail) · Universidad de Granada

![Generación D · Financiado por la Unión Europea (NextGenerationEU) · Ministerio para la Transformación Digital y de la Función Pública · Plan de Recuperación, Transformación y Resiliencia · CSIC · MOMENTUM](workspace/img/financiacion.png)
