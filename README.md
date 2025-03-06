
# Importar Recursos de Azure en Terraform

Este script de PowerShell (`import_terraform.ps1`) se utiliza para importar recursos de Azure en Terraform. A continuación se explica paso a paso cómo funciona el script y cómo utilizarlo.

> [!IMPORTANT]  
> **Requisitos**  
> - PowerShell instalado en tu sistema.  
> - Terraform instalado y configurado.  
> - Acceso a los recursos de Azure que deseas importar.  

## Descripción del Script

El script define una lista de recursos de Azure que se importarán en Terraform y luego ejecuta el comando `terraform import` para cada recurso.

### Lista de Recursos

La lista de recursos se define en la variable `$recursos` como un array de cadenas. Cada cadena contiene:
- Tipo de recurso: azurerm_virtual_machine
- Nombre del recurso: example
- ID del recurso: /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mygroup1/providers/Microsoft.Compute/virtualMachines/machine1

> [!CAUTION]
> Todo se separa por espacios, el propio script ya coloca el . en el lugar indicado.


```powershell
# Define la lista de recursos a importar
$recursos = @(
    "azurerm_virtual_machine example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mygroup1/providers/Microsoft.Compute/virtualMachines/machine1",
)
```
> [!TIP]
> Seguir añadiendo los recursos necesarios.

# Iterar y Ejecutar terraform import
El script itera sobre la lista de recursos y ejecuta el comando terraform import para cada uno. Primero, extrae el tipo de recurso, el nombre del recurso y el ID del recurso utilizando el método -split.

```powershell
# Iterar sobre la lista de recursos y ejecutar terraform import
foreach ($recurso in $recursos) {
    # Extraer el tipo de recurso, el nombre de recurso y el ID
    $tipo_recurso, $nombre_recurso, $id_recurso = $recurso -split ' '

 
    # Ejecutar terraform import para cada recurso
    Write-Output "Importando $tipo_recurso con ID $id_recurso..."
    terraform import "$tipo_recurso.$nombre_recurso" "$id_recurso"
}
```
# Uso
1. Clona este repositorio en tu máquina local.
2. Abre una terminal de PowerShell.
3. Login en Azure

    ```sh
    az login
    ```

4. Inicializa el backend de Terraform

    ```sh
    terraform init
    ```

   
5. Navega al directorio donde se encuentra el script import_terraform.ps1.
7. Ejecuta el script con el siguiente comando:
   
     ```powershell
   .\import_terraform.ps1
    ```
# El script importará los recursos definidos en la lista a tu configuración de Terraform.

> [!TIP]
> - Asegúrate de tener los permisos necesarios para acceder a los recursos de Azure.
> - Verifica que los IDs de los recursos sean correctos y estén actualizados.

> [!NOTE]  
> **Contribuciones**  
> - Si deseas contribuir a este proyecto, por favor abre un issue.  
> - También puedes enviar un pull request con mejoras.  
> - ¡Toda ayuda es bienvenida! 🚀

> [!WARNING]
Este proyecto está licenciado bajo la Licencia MIT. Consulta el archivo LICENSE para más detalles.
