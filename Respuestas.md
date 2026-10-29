# Reporte de Análisis: Patrón Bridge en Java

## Preguntas de Análisis

1. **Explosión de Clases:** 
   - *¿Cuántas clases necesitaríamos si tuviéramos 3 tipos de controles y 4 tipos de dispositivos sin el patrón Bridge?* 
     Sin el patrón Bridge, al haber una herencia directa y acoplada entre cada control y cada dispositivo, necesitaríamos el producto de ambas jerarquías: $3 \times 4 = 12$ clases (por ejemplo: `ControlBasicoRadio`, `ControlAvanzadoTV`, etc.).
   - *¿Y con el patrón Bridge?* 
     Con el patrón Bridge, las jerarquías están desacopladas mediante composición, por lo que solo necesitamos el número de elementos de cada lado sumados (más las clases base e interfaces): $3 \text{ (controles)} + 4 \text{ (dispositivos)} = 7$ clases en total, evitando por completo la explosión combinatorial.

2. **Acoplamiento:**
   - *¿Qué pasaría si la clase ControlRemotoBasico heredara directamente de Radio o TV en lugar de usar composición?* 
     Volveríamos al problema del acoplamiento estático. Si un control heredara directamente de un dispositivo específico, no podríamos cambiar de dispositivo en tiempo de ejecución ni reutilizar la lógica de los controles para nuevos electrodomésticos sin duplicar código masivamente.

3. **Extensibilidad:**
   - *Si quiero agregar un nuevo dispositivo (ej: Projector), ¿qué cambios necesito hacer? ¿Necesito modificar las clases de controles existentes?* 
     No se necesita modificar ninguna clase de control existente. Gracias al principio abierto/cerrado, solo creamos la clase `Projector` implementando la interfaz `Dispositivo`, y los controles existentes podrán interactuar con él inmediatamente gracias al puente.

4. **Principios SOLID:**
   - *¿Qué principios SOLID se aplican en este patrón?*
     - **Principio de Abierto/Cerrado (OCP):** Las jerarquías se pueden extender con nuevos dispositivos o controles sin alterar el código existente.
     - **Principio de Inversión de Dependencias (DIP):** Las abstracciones (`ControlRemoto`) dependen de abstracciones o interfaces (`Dispositivo`), no de implementaciones concretas.

5. **Flexibilidad:**
   - *¿Cómo nos beneficiamos al poder cambiar el dispositivo de un control en tiempo de ejecución?* 
     Permite una gran flexibilidad dinámica en la aplicación, donde un mismo objeto de control remoto puede apuntar, referenciar y operar diferentes aparatos electrónicos sobre la marcha.