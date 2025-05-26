# Despliegue Automatizado de SmaiV2 con Ansible

Este repositorio contiene un playbook Ansible que configura **localmente** todo lo necesario para ejecutar el proyecto [SmaiV2](https://github.com/McMiguel2004/smaiV2-main.git) en Ubuntu/Debian.

## ¿Qué hace este playbook?

1. **Instala herramientas básicas**  
   - `git` y `snapd`  
2. **Instala Docker**  
   - A través de `snap` (última versión estable)  
3. **Instala Node.js 16 LTS**  
   - Agrega el repositorio oficial NodeSource  
   - Instala `nodejs` (incluye `npm`)  
4. **Instala Python 3**  
   - Paquetes `python3`, `python3-pip`, `python3-setuptools` y `python3-wheel`  
5. **Instala y configura PostgreSQL**  
   - Instala el servicio PostgreSQL  
   - Modifica `pg_hba.conf` para usar autenticación MD5  
   - Crea la base de datos `smai` y el rol `usuario`  
   - Define tipos `ENUM` (`difficulty_enum`, `mode_enum`) y tablas iniciales  
   - Asigna permisos completos al rol  
6. **Descarga y prepara SmaiV2**  
   - Clona (o actualiza) el repositorio en `~/SmaiV2`  
   - Ejecuta `npm install` en `frontend` si falta  
   - Ejecuta `pip3 install -r requirements.txt` en `backend`  
7. **Configura sudoers**  
   - Permite a `www-data` y a tu usuario ejecutar Docker y WireGuard sin contraseña  

---

## Estructura de archivos

- smai-ansible/
- ├── inventory # Inventario local (localhost)
- ├── playbook.yml # Playbook principal
- └── README.md # Documentación



---

## Requisitos Previos

- Ubuntu 22.04 (o similar Debian-based)  
- Conexión a Internet  
- Permisos sudo  

---

## Instrucciones de Uso

1. **Instalar Ansible**  
   ```bash
   sudo apt update
   sudo apt install -y ansible


git clone https://github.com/McMiguel2004/smai-ansible.git
cd smai-ansible

2. **Ejecutar el playbook1.**  
   ```bash
ansible-playbook -i inventory playbook.yml --ask-become-pass
