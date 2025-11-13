# Lab 5 Integration and SOA - Project Report

## 1. EIP Diagram (Before)

![Before Diagram](diagrams/before.png)

Los problemas principales en el código inicial eran:
1. **Number Channel**: El canal NumberChannel no estaba creado, esto causaba que no hubiese un canal previo por el que pasar los números generados antes de ser enrutados a los flujos de números pares e impares, lo que producía errores con los negativos por ejemplo. Dicho problema se solucionó creando un canal directo llamado `numberChannel` y haciendo que el generador de números envíe los números a este canal primero.
2. **Filtro de Números Impares Mal Configurado**: El filtro en el flujo de números impares es una buena herramienta de programación defensiva, pero estaba mal configurado, además la solución solicitada no requería de este.

3. **Odd channel publish-subscribe**: El canal oddChannel no estaba definido per se, por lo que se ha definido como un canal publish-subscribe, permitiendo que múltiples suscriptores reciban mensajes de este canal (Handler Odd y Service Odd).  
---

## 2. What Was Wrong

Explain the bugs you found in the starter code:

- **Bug 1**: Los números negativos no eran manejados correctamente. Esto ocurría porque el canal `numberChannel` no estaba definido, lo que causaba que los números generados fueran enviados directamente a los flujos de números pares e impares sin un canal intermedio. La solución fue crear un canal directo llamado `numberChannel` y modificar el flujo de generación de números para que envíe los números a este canal primero.
- **Bug 2**: El sistema rechazaba algunos números impares debido a un filtro mal configurado en el flujo de números impares. Este filtro no era necesario para la funcionalidad requerida y causaba que algunos números válidos fueran descartados (más o menos la mitad, los que fuesen hacia el filtro). La solución fue eliminar el filtro del flujo de números impares, permitiendo que todos los números impares pasen directamente al transformador y al Service Activator.

---

## 3. What You Learned

He aprendido los principales elementos de los patrones de integración empresarial (EIP) y cómo implementarlos utilizando Spring Integration en Kotlin. Específicamente, he comprendido cómo funcionan los canales de mensajes, los flujos de integración, los transformadores y los activadores de servicio. Por último, he aprendido la importancia de la programación defensiva al manejar datos entrantes y cómo diseñar flujos de trabajo robustos que puedan manejar diferentes tipos de entradas sin fallar.

---

## 4. AI Disclosure

**Did you use AI tools?** (ChatGPT, Copilot, Claude, etc.)

- If YES: Which tools? What did they help with? What did you do yourself?
SI, cambios menores para que pase el clean Build con el Ktlin.
- If NO: Write "No AI tools were used."

**Important**: Explain your own understanding of the code and patterns, even if AI helped you write it.

---

## Additional Notes

Any other comments or observations about the assignment.
