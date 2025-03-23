 Restaurar en otro servidor o VPS**
1. **Prepara el nuevo servidor**:
   - Instala Ubuntu Server y configura los requisitos previos de Pterodactyl (dependencias, MySQL, PHP, etc.).
   - Clona el repositorio de GitHub en el nuevo servidor.

2. **Restaurar el Panel**:
   - Importa la base de datos:
     ```bash
     mysql -u root -p panel < panel_backup.sql
     ```
   - Extrae los archivos del panel:
     ```bash
     tar -xzvf pterodactyl_panel_backup.tar.gz -C /var/www/pterodactyl
     ```
   - Configura el archivo `.env` con las credenciales correctas para el nuevo servidor.

3. **Restaurar el Daemon**:
   - Extrae los archivos del daemon:
     ```bash
     tar -xzvf pterodactyl_daemon_backup.tar.gz -C /etc/pterodactyl
     ```
   - Copia el archivo de configuración del servicio:
     ```bash
     cp pterodactyl_service_backup.service /etc/systemd/system/pterodactyl.service
     ```
   - Recarga los servicios y reinicia el daemon:
     ```bash
     systemctl daemon-reload
     systemctl restart pterodactyl
     ```

4. **Verifica la instalación**:
   - Accede al panel desde el navegador y asegúrate de que todo funcione correctamente.
   - Prueba la conexión entre el panel y el daemon.

---

### **4. Automatización (Opcional)**
Si planeas hacer esto con frecuencia, puedes crear un script en Bash para automatizar el proceso de respaldo y restauración. También puedes usar herramientas como **Docker** para empaquetar todo el entorno de Pterodactyl y facilitar la migración.

---

### **Notas adicionales**
- Asegúrate de que las versiones de Pterodactyl, PHP, MySQL y otras dependencias sean compatibles entre los servidores.
- Si cambias la IP o el dominio del servidor, actualiza las configuraciones correspondientes en el panel y el daemon.

Con estos pasos, deberías poder migrar tu instalación de Pterodactyl sin problemas. ¡Buena suerte! 🚀
