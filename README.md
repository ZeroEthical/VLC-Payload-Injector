# Enhanced Windows Hacking Script via Movie Files (Potentially Malicious)

**Advertencia:** Este script ha sido modificado para incluir funcionalidades potencialmente maliciosas y debe ser utilizado únicamente en entornos controlados y con el permiso explícito del propietario del sistema. El uso no autorizado de este script es ilegal y puede acarrear graves consecuencias. El autor de este README no se hace responsable del uso indebido de este código.

## Descripción

Este script es una versión mejorada de un script original creado por Sabber Hossen, diseñado para explotar una vulnerabilidad en el reproductor VLC para ejecutar código malicioso en sistemas Windows a través de archivos de películas (MKV) modificados. Esta versión ha sido significativamente modificada para incluir funcionalidades adicionales con el propósito de ilustrar técnicas avanzadas de ataque y evaluar la seguridad de los sistemas.

**Código Original:** El código base de este script es una adaptación del trabajo original de Sabber Hossen. Los derechos de autor del código original pertenecen a Sabber Hossen.

**Modificaciones:** Esta versión del script incluye las siguientes modificaciones y funcionalidades adicionales:

*   **Técnicas Anti-Análisis:** Se han implementado comprobaciones básicas para detectar entornos virtualizados y herramientas de depuración, con el fin de dificultar el análisis del script.
*   **Ofuscación del Payload:** Se ha añadido un proceso de ofuscación básico del payload para intentar evadir la detección por software antivirus.
*   **Persistencia Avanzada:** Se ha incorporado la creación de un servicio systemd en el sistema objetivo para asegurar la ejecución del payload malicioso incluso después de un reinicio.
*   **Movimiento Lateral:** Se incluye una función para escanear la red local utilizando `nmap` en busca de otros hosts vulnerables, facilitando el movimiento lateral dentro de la red.
*   **Exfiltración de Datos:** Se ha añadido la capacidad de buscar y exfiltrar archivos específicos (documentos, hojas de cálculo, etc.) a un servidor remoto controlado por el atacante.
*   **Ataque a Aplicación Específica (Placeholder):** Se incluye un comentario como marcador de posición donde se podrían añadir módulos para explotar vulnerabilidades específicas en aplicaciones instaladas en el sistema objetivo.
*   **Payload Meterpreter:** Se ha actualizado la generación del archivo MKV para que utilice un payload de Meterpreter en lugar de una simple shell inversa, proporcionando capacidades de post-explotación más avanzadas.

## ¿Cómo Funciona?

El script sigue los siguientes pasos:

1. **Verifica el acceso root:** El script requiere privilegios de superusuario para su correcta ejecución.
2. **Instala dependencias:** Se asegura de que las herramientas necesarias (Metasploit Framework, Apache2, shc, nmap, curl, wine) estén instaladas en el sistema del atacante.
3. **Aplica técnicas anti-análisis:**  Realiza comprobaciones básicas para detectar entornos de análisis.
4. **Solicita la IP y el puerto del atacante:** Pide al usuario que introduzca la dirección IP y el puerto donde escuchará las conexiones inversas.
5. **Ofusca el payload:**  Genera y ofusca el payload malicioso.
6. **Inicia el handler de Metasploit:** Abre una instancia de `msfconsole` configurada para recibir la conexión del payload ofuscado.
7. **Genera el archivo MKV malicioso:** Utiliza Metasploit para crear un archivo MKV específicamente diseñado para explotar la vulnerabilidad de VLC y ejecutar el payload.
8. **Mueve el archivo al servidor web:** Copia el archivo MKV generado al directorio raíz del servidor web Apache para que pueda ser descargado por la víctima.
9. **Establece la persistencia:** Crea un servicio systemd para asegurar que el payload se ejecute al inicio del sistema.
10. **Realiza el movimiento lateral:**  Escanea la red local en busca de otros hosts.
11. **Intenta la exfiltración de datos:** Busca y trata de enviar archivos importantes a un servidor remoto.
12. **Inicia el handler principal de Metasploit:** Abre una segunda instancia de `msfconsole` configurada para recibir la conexión del payload principal (Meterpreter).

## ¿Cómo Utilizarlo?

**Advertencia:** Utiliza este script bajo tu propia responsabilidad y solo en entornos autorizados.

1. **Clona el repositorio:** Descarga el script a tu máquina Linux.
2. **Asegúrate de tener las dependencias instaladas:**  Si no se instalaron automáticamente, puedes instalarlas con el comando: `sudo apt install metasploit-framework apache2 shc nmap curl wine`
3. **Ejecuta el script con privilegios de root:**  `sudo bash nombre_del_script.sh`
4. **Introduce la IP del atacante:**  Introduce la dirección IP de tu máquina Linux, que será donde escuches las conexiones inversas.
5. **Introduce el puerto del atacante:**  Introduce el puerto en el que quieres que Metasploit escuche.
6. **Espera a que la víctima ejecute el archivo MKV:** Una vez que la víctima abra el archivo MKV modificado con VLC, el payload debería ejecutarse y establecer una conexión con tu máquina a través de Metasploit.

## Prerrequisitos

*   Sistema operativo Linux (Kali Linux recomendado).
*   Acceso a root.
*   Metasploit Framework instalado.
*   Servidor web Apache2 instalado y en funcionamiento.
*   `shc` (para ofuscación).
*   `nmap` (para escaneo de red).
*   `curl` (para exfiltración de datos).
*   `wine` (opcional, para ejecutar payloads de Windows si es necesario).

## Limitaciones

*   La efectividad del script depende de la vulnerabilidad de la versión de VLC utilizada por la víctima.
*   Las técnicas anti-análisis implementadas son básicas y pueden ser fácilmente superadas por herramientas de análisis más avanzadas.
*   La ofuscación del payload también es básica y puede ser detectada por software antivirus sofisticado.
*   El éxito del movimiento lateral depende de las vulnerabilidades presentes en otros hosts de la red.
*   La exfiltración de datos depende de la configuración del firewall de la víctima y de la disponibilidad del servidor de exfiltración.

## Licencia

Este código se proporciona tal cual, sin garantías. Se permite la copia, modificación y distribución para fines educativos y de investigación de seguridad, siempre y cuando se mantenga el reconocimiento del código original de Sabber Hossen y se incluya esta advertencia.

## Descargo de Responsabilidad

El autor de este README no se hace responsable del uso que se le dé a este script. Su uso para actividades ilegales o no éticas está estrictamente prohibido. Utilice este código de forma responsable y únicamente en entornos autorizados.
