# Pipeline-jenkins-java

Repositorio para el laboratorio de CI con Jenkins

## Descripción del laboratorio

En este laboratorio el alumno aprenderá los fundamentos de los pipelines de Jenkins y configurará un pipeline sencillo
para una aplicación Java con Spring Boot y Maven. Se conectará Github con Jenkins mediante *hooks* de forma que cada vez
que se realice un commit en el repositorio se ejecute de forma automática el pipeline de Jenkins.

[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC_BY--NC--SA_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

## Configuración del servidor de CI

En la cloudshell de Azure, subimos el fichero jenkins-init-java21.sh en la shell de Azure clickando en “Manage files” -> Upload

```SHELL
# creamos una carpeta nueva 
mkdir jenkins-get-started

# movemos el fichero a la carpeta
mv jenkins-init-java21.sh jenkins-get-started

# cambiamos de carpeta
cd jenkins-get-started

# creamos un nuevo grupo de recursos en azure
az group create --name jenkinsems2026-rg --location spaincentral

# creamos una máquina virtual
az vm create \
  --resource-group jenkinsems2026-rg \
  --name jenkinsems-vm-2026 \
  --image Ubuntu2204 \
  --admin-username jenkinsuser \
  --admin-password PASSWORD-12-32CARACTERES-MAY-MIN-NUMERO-CARACTERESESPECIALES \
  --generate-ssh-keys \
  --public-ip-sku Standard \
  --custom-data jenkins-init-java21.sh \
  --size Standard_B2s_v2

#abrimos el puerto 8080
az vm open-port --resource-group jenkinsems2026-rg --name jenkinsems-vm-2026 --port 8080 --priority 1010

# conexion por ssh, si nos pide confirmación de fingerprint decir que sí, e introducir la contraseña
ssh jenkinsuser@<ip>

# mostrar el contenido del fichero por pantalla
sudo cat /var/lib/jenkins/secrets/initialAdminPassword


```
