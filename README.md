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

<img width="763" height="407" alt="image" src="https://github.com/user-attachments/assets/0f1c1cdc-4373-4e46-92a2-37a85b13483a" />





