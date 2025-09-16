---
cover: ../.gitbook/assets/quality-assurance-code-bug.jpg
coverY: 110.50526315789473
---

# Logging

El "logging" es el proceso de registrar mensajes, eventos o información relevante durante la ejecución de un programa de software. Estos registros se guardan en archivos de registro (logs) o se envían a otros destinos, como consolas, bases de datos o servicios de registro en la nube. El propósito del logging es proporcionar una traza de lo que ha sucedido en una aplicación durante su ejecución, lo que facilita la monitorización, el diagnóstico de problemas, la depuración y el análisis de rendimiento.

Los principales beneficios del logging son:

1. **Diagnóstico de problemas:** Los logs registran eventos, advertencias y errores que ocurren durante la ejecución del programa. Estos registros pueden ser útiles para identificar y solucionar problemas que surgen en la aplicación.
2. **Auditoría y cumplimiento:** Los logs pueden utilizarse para realizar un seguimiento de las acciones realizadas por los usuarios o por el sistema, lo que facilita el cumplimiento de regulaciones y políticas de seguridad.
3. **Rendimiento y optimización:** El análisis de logs puede proporcionar información sobre el rendimiento de la aplicación, como tiempos de respuesta, uso de recursos y patrones de uso, lo que puede ayudar a identificar áreas de mejora y optimización.
4. **Seguridad:** Los logs pueden registrar eventos relacionados con la seguridad, como intentos de acceso no autorizado, ataques de seguridad o comportamientos sospechosos, lo que puede ayudar a detectar y mitigar amenazas a la seguridad.
5. **Seguimiento de eventos:** Los logs pueden utilizarse para realizar un seguimiento de eventos específicos en la aplicación, como la creación de cuentas de usuario, la realización de transacciones o la generación de informes, lo que facilita el seguimiento del flujo de trabajo y la auditoría.

### Niveles de logging

Los niveles de logging son una forma de categorizar los mensajes de registro según su importancia o gravedad. Los niveles de logging son utilizados por los sistemas de logging para filtrar y controlar qué mensajes deben ser registrados y cuáles deben ser ignorados. Los niveles de logging más comunes son los siguientes (en orden de menor a mayor gravedad):

1. **TRACE:** El nivel de logging más bajo. Se utiliza para mensajes de depuración muy detallados, como trazas de ejecución de código, valores de variables, etc. Estos mensajes son útiles para comprender en detalle el flujo de ejecución del programa, pero pueden generar una gran cantidad de información y ruido en los logs.
2. **DEBUG:** Se utiliza para mensajes de depuración que son útiles durante el desarrollo y la depuración del código, pero que normalmente no se necesitan en producción. Estos mensajes proporcionan información detallada sobre el estado interno del programa y pueden ayudar a identificar y solucionar problemas durante el desarrollo.
3. **INFO:** Se utiliza para mensajes informativos que son útiles para rastrear la ejecución del programa y proporcionar información sobre su estado. Estos mensajes suelen ser útiles para los administradores del sistema o para supervisar el funcionamiento general del programa.
4. **WARN:** Se utiliza para mensajes de advertencia que indican situaciones anormales o potencialmente problemáticas que no impiden la ejecución normal del programa, pero que podrían requerir atención. Estos mensajes suelen indicar condiciones que podrían conducir a errores o problemas en el futuro.
5. **ERROR:** Se utiliza para mensajes de error que indican que ha ocurrido un problema que impide que el programa continúe ejecutándose correctamente. Estos mensajes suelen indicar errores críticos que requieren intervención o corrección inmediata.
6. **FATAL:** Algunos sistemas de logging incluyen un nivel adicional de "FATAL" para mensajes que indican errores muy graves que causan la terminación inmediata del programa. Estos mensajes suelen indicar problemas que impiden que el programa continúe ejecutándose y que pueden requerir intervención manual o reparación del sistema.

Es importante utilizar los niveles de logging de manera apropiada y consistente en tu código para proporcionar la cantidad adecuada de información en los logs y facilitar la depuración y el análisis de problemas. En entornos de producción, es común configurar el sistema de logging para registrar mensajes de niveles INFO, WARN, ERROR y FATAL, mientras que en entornos de desarrollo se pueden utilizar niveles de logging más bajos como DEBUG y TRACE para obtener información detallada sobre el funcionamiento del programa.

## Logging en Java

Para realizar el logging en Java, usaremos la librerio slf4j-log4j12, para ello debemos añadir la siguiente dependencia a nuestro pom.xml

```xml
<!-- https://mvnrepository.com/artifact/org.slf4j/slf4j-log4j12 -->
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-log4j12</artifactId>
    <version>2.0.13</version>
</dependency>
```

Una vez se ha descargado la librería, debemos configurarla añadiendo el archivo log4j.xml al directorio src/main/resources

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">

<log4j:configuration debug="true">
    <appender name="fileAppender" class="org.apache.log4j.RollingFileAppender">
        <param name="File" value="out.log"/>
        <layout class="org.apache.log4j.PatternLayout">
            <param name="ConversionPattern" value="%d{yyyy-MM-dd HH:mm:ss} %-5p %c:%L - %m%n" />
        </layout>
    </appender>

    <appender name="consoleAppender" class="org.apache.log4j.ConsoleAppender">
        <param name="Target" value="System.out"/>
        <layout class="org.apache.log4j.PatternLayout">
            <param name="ConversionPattern" value="%d{yyyy-MM-dd HH:mm:ss} %-5p %c:%L - %m%n" />
        </layout>
    </appender>
    <root>
        <priority value="info" />
        <appender-ref ref="consoleAppender" />
        <appender-ref ref="fileAppender" />
    </root>
</log4j:configuration>
```

Esta configuración enviará todos los log a la consola `System.out` y a un fichero llamado `out.log`

Ahora, ya podemos empezar a utilizar la librería en nuestras clases. Veamos un ejemplo

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class MiClase {
    // Las clases que vayan a hacer logging tendran una sentencia como esta.
    // ATENCION: es importante cambiar el nombre de la clase
    private static final Logger log = LoggerFactory.getLogger(MiClase.class);

    public void miMetodo() {
        // Crea el mensaje "Este es un mensaje de depuración" con nivel debug en los log
        log.debug("Este es un mensaje de depuración");
        // Crea el mensaje "Este es un mensaje informativo" con nivel warning en los log
        log.info("Este es un mensaje informativo");
        // Crea el mensaje "Este es un mensaje de advertencia" con nivel warning en los log
        log.warn("Este es un mensaje de advertencia");
    }
}
```
