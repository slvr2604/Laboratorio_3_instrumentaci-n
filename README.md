# Tercera entrega de laboratorio instrumentación biomédica y biosensores BMED C. Grupo conformado por: 
Alissia Montealegre Quintero. 
Raul Alexander Peñuela Jimenez.
Silvia Lorena Vargas Rueda.


# Cálculo ambulatorio del índice pletismográfico quirúrgico (SPI)  

## Resumen

En esta práctica de laboratorio se planteó el desarrollo de un sistema para la adquisición de la señal fotopletismográfica (PPG) y el cálculo ambulatorio del índice pletismográfico quirúrgico (SPI), utilizado como indicador del balance entre nocicepción y analgesia. Para lograrlo, se propuso construir un circuito de adquisición basado en un sensor óptico de reflectancia, realizar la captura de la señal mediante Arduino y posteriormente procesarla utilizando MATLAB. La práctica también contemplaba la aplicación de la maniobra Cold Pressor Test (CPT) para observar las variaciones fisiológicas asociadas a una respuesta nociceptiva.

Durante el desarrollo experimental se realizó el montaje del circuito de adquisición en protoboard, sin embargo, el circuito no presentó el funcionamiento esperado y no fue posible obtener una señal PPG adecuada para continuar con la adquisición y procesamiento de los datos. Debido a esto, no se logró realizar la captura experimental, el cálculo del SPI ni la aplicación completa del protocolo planteado. Por esta razón, el presente informe documenta el procedimiento propuesto, las dificultades encontradas y las consideraciones necesarias para el desarrollo de la práctica.


---

# I. Introducción

Durante los procedimientos quirúrgicos, el organismo puede presentar respuestas fisiológicas asociadas a estímulos negativos y al estrés producido durante la intervención. La evaluación de estas respuestas es especialmente importante en pacientes sometidos a anestesia general, ya que permite estudiar el balance entre la nocicepción y la analgesia administrada. Entre las herramientas desarrolladas para este propósito se encuentra el índice pletismográfico quirúrgico (SPI, *Surgical Pleth Index*), el cual utiliza información obtenida a partir de la onda de pulso o señal fotopletismográfica (PPG) para estimar cambios relacionados con la respuesta nociceptiva [1].

El SPI presenta valores entre 0 y 100, donde los valores más altos indican una mayor respuesta nociceptiva. De acuerdo con la guía de laboratorio, durante una anestesia general se considera como referencia un rango entre 20 y 50 para una analgesia adecuada.

En esta práctica se planteó el diseño y construcción de un sistema para capturar las variaciones del volumen sanguíneo periférico mediante un sensor óptico de reflectancia. La señal obtenida debía ser adquirida mediante una placa Arduino y posteriormente procesada en MATLAB para identificar las características de la onda de pulso y calcular el SPI en cada latido. Además, se contemplaba la aplicación del *Cold Pressor Test* (CPT) con el propósito de generar una respuesta fisiológica similar a la producida por el dolor agudo y observar sus efectos sobre el índice.

Durante el desarrollo experimental, el circuito de adquisición no presentó el funcionamiento esperado. No fue posible obtener una señal PPG adecuada y estable que permitiera continuar con las etapas de adquisición, procesamiento y cálculo del SPI. Por esta razón, no se obtuvieron datos experimentales ni fue posible completar la entrega de laboratorio planteada inicialmente. Esta situación se documenta en el presente informe como parte de las dificultades encontradas durante la implementación del sistema.


## Objetivos.

### Objetivo general

Desarrollar y documentar un sistema de medición ambulatoria del índice pletismográfico quirúrgico (SPI) a partir de la adquisición y procesamiento de una señal fotopletismográfica (PPG), reconociendo las etapas necesarias para su implementación y las limitaciones encontradas durante el montaje experimental.

### Objetivos específicos

* Reconocer las características fundamentales de la onda de pulso utilizadas para la obtención del SPI.
* Construir un sistema de adquisición capaz de detectar las variaciones del volumen sanguíneo periférico mediante un sensor óptico.
* Implementar la adquisición de la señal mediante una placa Arduino y su posterior procesamiento en MATLAB.
* Analizar el procedimiento necesario para calcular el SPI a partir de las características de la señal de pulso.
* Identificar las posibles dificultades y limitaciones presentadas durante el montaje y funcionamiento del circuito de adquisición.
* Comprender la relación entre las variaciones fisiológicas producidas durante el Cold Pressor Test y la respuesta nociceptiva.

---

# II. Marco Teórico

## A. Fotopletismografía (PPG)

La fotopletismografía (PPG) es una técnica óptica que se utiliza para detectar variaciones en el volumen sanguíneo de los tejidos. Su funcionamiento se basa en la interacción de la luz con el tejido biológico, esto ocurre cuando una fuente de luz ilumina la zona de interés y un fotodetector registra los cambios en la cantidad de luz recibida. Debido a que el volumen de sangre presente en los vasos sanguíneos cambia con cada ciclo cardíaco, la señal obtenida presenta variaciones relacionadas con el pulso [2].

La señal PPG puede utilizarse para identificar características como los pulsos cardíacos, el intervalo entre ellos y la amplitud de la onda. Estas características son de utilidad para el monitoreo de variables fisiológicas y constituyen la base de diferentes sistemas de instrumentación biomédica.
### Figura 1. Circuito para la captura de las variaciones del volumen sanguíneo periférico
<img width="763" height="407" alt="image" src="https://github.com/user-attachments/assets/0f1c1cdc-4373-4e46-92a2-37a85b13483a" />

*Fuente: Adaptado de la Guía de Preparación de Práctica de Laboratorio, Instrumentación Biomédica y Biosensores, Universidad Militar Nueva Granada.*

## B. Nocicepción y respuesta autonómica
La nocicepción es el proceso por el cual el cuerpo detecta los estímulos potencialmente dañinos utilizando el sistema nervioso.Aunque existe una relación muy estrecha entre la nocicepción y el dolor los dos términos no son intercambiables;la nocicepción implica el procesamiento de los estímulos dolorosos por parte del sistema nervioso mientras que el dolor es una sensación que depende de la fisiología y la psicología.[2]Este punto se vuelve importante cuando se administra una anestesia general ya que incluso bajo una anestesia general un paciente puede presentar reacciones autónomas a la nocicepción [3].

La implementación de un estímulo nocivo conduce a cambios en el funcionamiento del sistema nervioso autónomo principalmente debido al aumento de la actividad simpática. Esta reacción puede causar alteraciones en los parámetros cardiovasculares incluyendo la frecuencia cardíaca, el intervalo entre ciclos cardíacos, la presión arterial y el tono vascular periférico. Dado que estos cambios pueden ser medidos por medio de señales fisiológicas,se han diseñado varios sistemas de monitoreo para evaluar objetivamente la respuesta nociceptiva durante la cirugía. Según la literatura especializada estos sistemas de monitoreo no miden directamente la experiencia subjetiva del dolor sino que miden reacciones fisiológicas relacionadas con la actividad autónoma como una aproximación de la experiencia nociceptiva [3].

En este sentido la actividad simpática adquiere un significado especial en la circulación periférica. En respuesta a ciertos estímulos estresantes o nocivos el proceso de vasoconstricción periférica disminuye el volumen de sangre en los tejidos y causa la alteración de la amplitud de la onda pulsátil medida por la fotoplejismografía. Así la alteración en la señal PPG puede proporcionar indirectamente información acerca de los cambios en el tono vascular y la reacción autónoma del paciente [4],[5].

## C. Amplitud de la onda pletismográfica y tono vascular
La amplitud de la señal de la plejismografía se vuelve un aspecto particularmente fascinante dentro del contexto de las aplicaciones asociadas con la reacción autónoma.Un cambio en el tono vascular periférico conduce a un cambio en el volumen de sangre en la cama vascular lo cual a su vez crea cambios en la amplitud de la señal óptica obtenida. La vasoconstricción periférica resultante de la activación simpática bajo algunos estímulos específicos conduce a una disminución de la amplitud de la señal del pulso [4],[5].

Este principio fisiológico explica el hecho de que la amplitud de la señal de la plejismografía sea uno de los parámetros del índice SPI.Incluye datos tanto de la amplitud de la onda de la PPG como del intervalo de tiempo entre pulsos [4],[5].

Sin embargo, es importante destacar que la amplitud de la PPG(Gradiente de Presión Pulso) no está exclusivamente relacionada con la respuesta nociceptiva. La presión,la temperatura,la perfusión, el volumen intravascular,la postura del cuerpo y otros factores hemodinámicos del sensor pueden afectar su valor.Por lo tanto un aumento o una disminución de la amplitud no puede considerarse la manifestación de la presencia del dolor de forma independiente [9].

## D. Índice pletismográfico quirúrgico
El SPI es un parámetro creado para evaluar el equilibrio entre el estímulo del dolor y la antinocicepción bajo la anestesia general.Este concepto se basa en la reacción del sistema nervioso autónomo a los estímulos nociceptivos y se basa en la información obtenida usando la fotoplejisografía periférica. El parámetro se describe mediante un número del 0 al 100, con números más altos que indican una reacción fisiológica más significativa al estímulo nociceptivo[4],[5].

El SPI se calcula de acuerdo a dos características fundamentales de la señal: la amplitud de la onda del pleth gráfico (PPGA) y la diferencia de tiempo entre latidos o Intervalo del latido cardíaco (HBI). Estos parámetros se normalizan y luego se integran en una sola expresión. La fórmula matemática utilizada es la siguiente:

$$
SPI=100-\left(0.67\,PPGA_{norm}+0.33\,HBI_{norm}\right)
$$

donde PPGAnorm corresponde a la amplitud pletismográfica normalizada y HBInorm representa el intervalo entre latidos normalizado [4], [10].





