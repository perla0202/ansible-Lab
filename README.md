# Laboratorio Ansible + Docker

## Objetivo de la práctica

Crear un laboratorio con dos servidores Linux (contenedores Ubuntu 24.04) usando
Docker y administrarlos con Ansible mediante un inventario y un playbook que:

- Muestra el nombre del host y el sistema operativo.
- Crea el directorio `/tmp/ansible-demo` y el archivo `info.txt`.
- Crea con un `loop` los directorios `logs`, `backup` y `config`.
- Muestra un mensaje únicamente cuando el sistema operativo es Ubuntu.

## Estructura

```text
ansible-lab/
├── docker-compose.yml
├── inventory.ini
├── playbook.yml
└── README.md
```

## Requisitos

- Docker y Docker Compose
- Ansible (`sudo apt install ansible` o `pip install ansible`)
- Colección `community.docker` (ya incluida en el paquete `ansible`; si no):

```bash
ansible-galaxy collection install community.docker
```

## Comandos para iniciar los contenedores

```bash
# Levantar los servidores
docker compose up -d

# Verificar que estén ejecutándose
docker ps

# Instalar Python en cada contenedor (requerido por Ansible)
docker exec server1 bash -c "apt update && apt install -y python3"
docker exec server2 bash -c "apt update && apt install -y python3"
```

## Comprobar la conexión

```bash
ansible docker -i inventory.ini -m ping
```

## Comando para ejecutar el playbook

```bash
ansible-playbook -i inventory.ini playbook.yml
```

## Captura de pantalla de la ejecución exitosa

![Ejecución exitosa del playbook](CapturaPrueba.png)

## Limpieza

```bash
docker compose down
```
