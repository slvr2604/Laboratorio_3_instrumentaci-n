# Tercera entrega de laboratorio instrumentación biomédica y biosensores BMED C. Grupo conformado por: 
Alissia Montealegre Quintero. 
Raul Alexander Peñuela Jimenez.
Silvia Lorena Vargas Rueda.


# Cálculo ambulatorio del índice pletismográfico quirúrgico (SPI)  

## Resumen

La respiración es un proceso fisiológico esencial que garantiza el intercambio de oxígeno y dióxido de carbono entre el organismo y el medio ambiente. El monitoreo de sus variables permite evaluar el estado funcional del sistema respiratorio y constituye una herramienta de gran utilidad en aplicaciones clínicas.

En esta práctica se diseñó un sistema de adquisición para registrar el patrón respiratorio de un individuo sano mediante un sensor resistivo sensible a la fuerza (**FSR402**), ubicado sobre la región toracoabdominal para detectar las variaciones de presión de contacto generadas durante la respiración.

La señal fue adquirida mediante una tarjeta **DAQ** y procesada en **MATLAB** para su visualización y análisis. Se realizaron registros en condiciones de reposo y durante el habla con el fin de comparar el comportamiento del patrón respiratorio y estimar la frecuencia respiratoria.

Además, se plantea el análisis de la señal en los dominios del tiempo y de la frecuencia para identificar las componentes dominantes y relacionar los resultados con la fisiología respiratoria.

---

# I. Introducción

La respiración es un proceso fisiológico fundamental para el mantenimiento de la vida, ya que permite el intercambio de oxígeno y dióxido de carbono entre el organismo y el medio externo, garantizando el aporte de oxígeno a los tejidos y la eliminación del dióxido de carbono producido por el metabolismo celular [1].

Debido a su importancia, la evaluación de la función respiratoria constituye una herramienta esencial para valorar el estado fisiológico de un individuo y detectar posibles alteraciones del sistema respiratorio [2].

Entre los principales parámetros respiratorios se encuentran:

- Frecuencia respiratoria.
- Volumen corriente.
- Volumen minuto.
- Patrón respiratorio.

Estos parámetros proporcionan información sobre el funcionamiento del sistema respiratorio y la respuesta del organismo frente a diferentes condiciones fisiológicas [2].

En particular, la frecuencia respiratoria es uno de los signos vitales de mayor utilidad clínica, ya que puede modificarse como consecuencia de cambios en la actividad física, el habla, el estrés o diversas patologías respiratorias [3].

Para el monitoreo de estos parámetros pueden medirse diferentes variables físicas relacionadas con el proceso respiratorio, como:

- Flujo de aire.
- Presión.
- Temperatura.
- Humedad.
- Movimientos de expansión y contracción torácica y abdominal.

La selección de la variable depende de la aplicación y del método de adquisición empleado [4].

Los sistemas de monitoreo no invasivos han cobrado especial importancia debido a que permiten registrar la actividad respiratoria sin generar molestias ni interferir con el proceso fisiológico normal [4].

En esta práctica se empleó un sensor **FSR402** ubicado sobre la región toracoabdominal para detectar las variaciones de fuerza de contacto producidas durante la expansión y contracción del cuerpo a lo largo del ciclo respiratorio.

### Objetivo

Desarrollar un sistema de adquisición capaz de registrar la señal respiratoria de un individuo sano mediante una tarjeta DAQ, procesarla en MATLAB y determinar la frecuencia respiratoria tanto en estado de reposo como durante el habla.

---
