# Todo empieza con un evento — kit inicial

Este kit corresponde a la misión 02 del Game Pack AWS Event-Driven. Incluye la
infraestructura Terraform base para estudiarla y preparar su validación.
Las funciones Python son ejercicios pendientes de la misión 03;
no procesan órdenes todavía. No contiene las pruebas ni las soluciones oficiales.

## Sube el kit desde tu navegador

1. Descomprime el ZIP. Sube su **contenido**, no el archivo ZIP ni la carpeta
   contenedora que pueda crear tu descompresor.
2. En GitHub, crea un repositorio en tu cuenta, por ejemplo `gameday-tu-nombre`.
   Puede ser público o privado; autoriza la GitHub App únicamente en este repositorio.
   No incluyas información personal ni secretos. Inicialízalo con un
   README para que aparezca el menú de archivos.
3. Abre **Add file → Upload files** y arrastra las carpetas `.github` y
   `game-packs`, junto con los archivos de la raíz de este kit. Activa mostrar
   archivos ocultos en tu explorador (en Linux, Ctrl+H) para ver `.github` y
   `.gitignore`. Guarda los cambios con **Commit changes** en `main`.
   Si GitHub propone una rama nueva, integra el cambio antes de enviar tu entrega.
4. Comprueba que la raíz de GitHub contiene `.github/` y `game-packs/`.
   Evita rutas como `kit/game-packs/` o `aws-event-driven/game-packs/`.
   Si ya tenías un repositorio vinculado, conserva ese repositorio y revisa los
   archivos antes de reemplazarlos. Subir el kit no elimina tu antigua carpeta
   `terraform/`: la ruta utilizada por el reto es la que aparece abajo.
5. Vuelve a Arena y vincula la URL HTTPS de ese repositorio en la misión 02.
6. En Arena, pulsa **Autorizar GitHub**, instala la App en el repositorio y termina la autorización con su cuenta propietaria.
7. Copia el identificador del evento que aparece en Arena. En GitHub entra a
   **Settings → Secrets and variables → Actions → Variables → New repository variable**.
   Crea `ARENA_EVENT_ID` con ese identificador (no es el código de inscripción).
8. Abre **Actions → Evaluar laboratorio en Arena → Run workflow** en la rama
   predeterminada. Los siguientes cambios en los archivos del laboratorio disparan
   la revisión automáticamente mientras el evento y la misión estén activos.
   Puedes seguir sus etapas tanto en Actions como en Arena.
9. Si ya tenías un kit anterior, reemplaza solamente `.github/workflows/terraform-lab.yml`
   con el archivo actualizado; conserva tus soluciones.

No necesitas instalar Git, Terraform ni AWS CLI en tu computador para estos pasos.
La estructura del repositorio debe quedar así:

```text
.github/workflows/terraform-lab.yml
.gitignore
README.md
LICENSE
ARENA-KIT.json
game-packs/aws-event-driven/
  terraform/
    main.tf
    variables.tf
    versions.tf
    outputs.tf
    terraform.tfvars.example
    .build/.gitkeep
  functions/
    orders/handler.py
    payments/handler.py
    inventory/handler.py
```

## Qué debes revisar en la misión 02

- Identifica el recorrido HTTP → Orders → EventBridge → SQS → Payments/Inventory.
- Ubica las tablas de DynamoDB, los permisos IAM y las colas de mensajes fallidos.
- Revisa las variables de Terraform y el prefijo único que asignará el instructor.
- Conserva `use_floci=true`. No agregues claves AWS ni ejecutes `terraform apply`
  en tu computador; el laboratorio se ejecutará en el entorno autorizado.
- Las tres funciones levantan `NotImplementedError` a propósito. Su implementación
  corresponde a la misión 03; los fallos y duplicados se trabajan en la misión 04.

## Estado actual de la evaluación

GitHub Actions solicita la evaluación del commit mediante una identidad OIDC de
corta duración. No necesitas guardar tokens ni claves en GitHub. El workflow no
ejecuta tu Terraform: el evaluador de Arena lo valida y genera el plan en una VM
desechable sin red, con Floci y proveedores preinstalados. No ejecuta `apply` ni
prueba todavía el comportamiento de las funciones.

Las etapas de verificación, inicialización, validación, plan y limpieza aparecen
en Arena y en los logs de Actions. El resultado oficial puede conceder los 14
puntos de validación una sola vez; el punto por vincular el repositorio es separado.
Un workflow modificado que muestre éxito no concede puntos por sí mismo.

Para reintentar un commit fallido o bloqueado, utiliza **Run workflow** y activa
`retry`; el portal solo muestra el resultado y sus etapas. Hay un máximo de cinco intentos
por entrega y una evaluación en curso por equipo. Una misión ya aprobada se omite.
Si el instructor usa otro dominio, configura además la variable `ARENA_URL` con
su URL HTTPS; su audiencia OIDC debe coincidir. La ruta de Actions debe estar
habilitada por el instructor en Cloudflare Access.

`ARENA-KIT.json` identifica la versión del kit y los hashes de los archivos
originales; puedes modificar el código para resolver los ejercicios.

Ayuda de GitHub: [subir archivos y carpetas desde el navegador](https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository).
