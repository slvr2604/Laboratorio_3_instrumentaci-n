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

La normalización es un proceso importante ya que es a través de la normalización que las variables originales se convierten en una escala tal que puedan ser combinadas. La derivación original del índice implica la transformación de la distribución individual del HBI y del PPGA usando datos históricos del paciente y distribuciones de referencia para poder expresar ambas variables usando una escala común del 0 al 100 [10].

El peso asignado a cada uno de los componentes lleva al hecho de que la amplitud plethysmográfica tiene más peso que el intervalo entre latidos del corazón.Esto se debe a la capacidad del PPGA de detectar los cambios en la vasoconstricción periférica debido a la actividad simpática. El HBI por otro lado da datos acerca de la actividad cardíaca [4],[10].

En estudios clínicos se ha empleado un intervalo aproximado de 20 a 50 como referencia para la monitorización de la analgesia durante anestesia general. No obstante, estos valores corresponden al contexto clínico del SPI comercial y no deben trasladarse automáticamente a una implementación experimental simplificada, especialmente cuando el algoritmo de normalización y las condiciones de adquisición difieren del sistema clínico original [5], [6].

## E. Procesamiento digital de señales PPG
La adquisición de parámetros fisiológicos de una señal PPG normalmente requiere una fase de preprocesamiento inicial. El objetivo es eliminar las partes de la señal que no se desean manteniendo intactas las características relacionadas con los latidos del corazón. Algunos de los problemas comunes en este sentido son el desplazamiento de la línea base, ruidos de alta frecuencia, artefactos de movimiento y la variación de la forma del pulso [9].

Se pueden utilizar filtros para confinar la señal dentro de un cierto rango de frecuencia basado en el rango de frecuencia fisiológica. Los filtros de paso banda por ejemplo pueden ayudar a atenuar las partes de muy baja frecuencia de la señal que causan el desplazamiento de la línea base y las partes de alta frecuencia que corresponden al ruido. Sin embargo se debe tener cuidado al seleccionar los frecuencias de corte en términos de la tasa de muestreo ya que un sobre filtrado puede distorsionar la forma de la señal y así interferir con la detección de los pulsos [9].

## F. Detección de máximos y mínimos en señales PPG
Encontrar los máximos y mínimos es una parte crucial del análisis de las señales PPG ya que ayuda a definir los límites de cada onda pulsátil y su dinámica temporal.La diferencia entre los máximos consecutivos permite determinar la distancia temporal entre latidos del corazón mientras que la relación entre los máximos y los mínimos permite estimar la amplitud de los pulsos.Se han propuesto diversos enfoques para realizar esta operación todos los cuales poseen tanto ventajas como desventajas en cuanto a la presencia de ruido,el desplazamiento de la línea base y la amplitud variable.[9]

### F.1. Detección mediante máximos y mínimos locales
Una de las técnicas más sencillas incluye la detección de los valores máximos o mínimos en un determinado intervalo de tiempo. Dentro de esta técnica el señal se analiza de acuerdo a ventanas de tiempo y el punto que tenga el valor máximo o mínimo dentro de cada área se elige. Este proceso puede ser complementado por limitaciones de amplitud y de tiempo que evitarían que cualquier amplitud pequeña sea detectada como pulsaciones [9].

La principal ventaja de esta técnica radica en su simplicidad que permite su uso en sistemas de adquisición en tiempo real fácilmente. Sin embargo depende mucho del tamaño de la ventana y de la selección del umbral. En caso de una selección de ventana inadecuada la técnica detectará varios máximos correspondientes a un mismo pulso o por el contrario no detectará pulsos consecutivos. Además la variabilidad línea a línea puede influir en la detección cuando se aplican umbrales absolutos [9].

### F.2. Detección mediante umbral adaptativo
Los métodos de umbrales adaptativos intentan mejorar algunos problemas presentados en el método de umbral fijo ajustando el umbral basándose en las propiedades de la señal detectadas en períodos anteriores.En el caso de la señal PPG estos algoritmos podrían ajustar el umbral dependiendo de la amplitud del pulso y establecer limitaciones temporales entre eventos consecutivos [7][9].

El algoritmo de umbral adaptativo utiliza un umbral que varía junto con la amplitud de la señal y establece un periodo refractario para evitar la detección de eventos en pulsos posteriores.En particular esta técnica es útil cuando se trabaja con señales cuya amplitud varía durante la adquisición porque el criterio no está completamente fijo [7].

Una ventaja de los métodos adaptativos es su tolerancia a los cambios lentos en la línea base y a la variación de la amplitud. Sin embargo el algoritmo requiere algunos parámetros referentes a la adaptación del umbral y al intervalo refractario, así que la configuración inadecuada de estos puede causar pulsos perdidos o detecciones falsas [7][9].

### F.3. Detección mediante cruces por cero y derivadas
Otra forma de abordar el problema es estudiar la pendiente de la propia señal. El máximo local se dará cuando la pendiente pase de ser positiva a negativa y viceversa, un mínimo se dará cuando la pendiente pase de ser negativa a positiva. Por lo tanto el problema de detectar amplitudes extremas se reduce al problema de detectar la transición entre signos en la pendiente.[9]

Los enfoques basados en cruces de cero pueden tener problemas si hay pequeñas oscilaciones en la señal ya que cada oscilación va a traer cambios de signo que son detectados como máximos o mínimos.En este caso siempre se requiere un preprocesamiento o un suavizado. También existen variantes en las cuales las transformadas de onda o de Hilbert preceden al procedimiento de detección.[9]

### F.4. Métodos basados en transformada wavelet
La transformada wavelet permite representar la señal simultáneamente en los dominios temporal y de escala, facilitando la identificación de características que aparecen a diferentes frecuencias. En señales PPG, esta propiedad puede aprovecharse para separar componentes asociadas con los pulsos de otras variaciones de la señal [9], [11].

Los métodos basados en wavelets pueden presentar una elevada robustez frente a componentes de ruido tanto de alta como de baja frecuencia; sin embargo, su mayor complejidad computacional puede dificultar su implementación en sistemas de tiempo real con recursos limitados [9], [11].

### F.5. Detección mediante primera derivada
Los métodos basados en derivadas son otra forma de encontrar los puntos característicos de la onda PPG. La primera derivada es una herramienta para enfatizar las transiciones rápidas de la señal mientras que la segunda derivada se utiliza para analizar la morfología del pulso y encontrar sus características secundarias [9]. La principal fortaleza de este método es la capacidad de acentuar las características morfológicas de la señal que son difíciles de notar en la original. Sin embargo la desventaja de este método es la amplificación de los componentes de ruido de alta frecuencia [9].

## F.6. Método del alpinista
Entre los enfoques diseñados especialmente para el procesamiento de las señales PPG se encuentra el "Método del Montañero" que se ha sugerido para el reconocimiento de picos en las señales PPG. El enfoque ha sido elaborado teniendo en cuenta particularmente la dificultad de reconocer los pulsos en caso de cambios en las amplitudes de la señal, el desplazamiento de la línea base y las señales de baja amplitud [8].

El enfoque se basa en escanear gradualmente la señal para definir las áreas de pendientes ascendentes y descendentes de la señal hasta que se reconozcan los puntos que podrían corresponder a los picos y valles de la señal. El enfoque no se basa solamente en un umbral absoluto sino que analiza la evolución de la propia señal para encontrar sus picos y valles. Este enfoque permite que el algoritmo tome en cuenta los cambios en las amplitudes de la señal, lo cual es especialmente importante para las señales PPG ya que su amplitud puede cambiar [8].

La técnica del escalador es particularmente importante para la práctica ya que no se trata solamente de la detección de picos sistólicos sino de la obtención de los mínimos diastólicos requeridos para la determinación de la amplitud del pulso también.La literatura que trata de diversos métodos de detección involucra,entre otros,la técnica de umbral adaptativo,técnicas robustas y la técnica del escalador,prueban que el comportamiento de cada una de ellas depende de las propiedades de la señal y de las perturbaciones [8],[9].

La elección del algoritmo debe hacerse dependiendo del objetivo del programa.Es particularmente crítico para un sistema diseñado para calcular el SPI asegurarse de que el algoritmo encuentre correctamente los picos y los valles relacionados con cada latido ya que los errores en su búsqueda afectarán la estimación del intervalo de tiempo entre los pulsos y el cálculo de la amplitud plethográfica.Por lo tanto la precisión en la búsqueda de los picos y los valles influye directamente en el resultado del cálculo [8],[9].

## G. Intervalo entre latidos y frecuencia cardíaca
El HBI (Intervalo del latido cardíaco) es igual al tiempo transcurrido entre un latido cardíaco y el siguiente.En una señal de un fotoplethysmograma (PPG) se puede medir a través de la diferencia de tiempo entre dos picos sistólicos siempre y cuando estos sean detectados con precisión. Si  $ t_{i} $  ti es el instante en el cual ocurre el pico de un latido cardíaco y  $ t_{i+1} $  el de el siguiente entonces el HBI se puede escribir como:

$$
HBI_i = t_{i+1} - t_i
$$

Cuando el intervalo se expresa en segundos, la frecuencia cardíaca puede estimarse mediante:

$$
HR = \frac{60}{HBI}
$$

Por lo tanto es importante tener en cuenta que una detección precisa del pico es muy esencial no solo para la determinación de la frecuencia cardíaca sino también para el cálculo del SPI.Un resultado falso positivo disminuirá artificialmente el intervalo entre latidos mientras que omitir un latido resulta en un intervalo entre latidos anormalmente alto.

## H. Amplitud del pulso pletismográfico
Cada amplitud de pulso se puede obtener usando el máximo y el mínimo que corresponde a ese pulso.Esto implica que para una amplitud de pulso de $ P_{max} $ y su mínimo de $ P_{min} $ , entonces la amplitud se define por:

$$
PPGA_i = P_{max,i} - P_{min,i}
$$

Este es un valor que muestra el tamaño de la señal pulsátil registrada por el sensor.Para calcular el SPI se debe normalizar primero la amplitud de cada pulso. Según la literatura del SPI el PPGA normalizado es uno de los dos parámetros claves que forman el SPI [10].

## I. Normalización de las variables para el cálculo del SPI
La normalización proporciona la posibilidad de convertir las variables HBI y PPGA las cuales tienen diferentes escalas y unidades a una uniforme.Como se hizo originalmente en el desarrollo del SPI las variables se normalizan con el uso de la información de la señal histórica y las distribuciones de referencia [10].

La importancia de este problema debe enfatizarse especialmente al implementar el SPI en el ambiente experimental. Una fórmula la cual se basa en el uso directo de los valores de amplitud y tiempo del sistema de adquisición no corresponde completamente al SPI implementado en las clínicas ya que el dispositivo comercial tiene su propio proceso de normalización. Si el laboratorio intenta desarrollar una implementación simplificada del índice entonces se debe enfatizar la diferencia entre ellos [10].

## J. Cold Pressor Test como estímulo fisiológico
La prueba del prensador frío (CPT) es un experimento donde el estímulo para una respuesta autónoma es un estímulo frío, el cual normalmente consiste en sumergir uno de los miembros en agua fría. La respuesta que se produce de este tipo de estímulo es una respuesta simpática,caracterizada por un aumento de la presión arterial,la frecuencia cardíaca y un cambio en el tono vascular periférico [12].

En cuanto al sistema cardiovascular la respuesta simpática provocada por la estimulación fría provoca la vasoconstricción y cambios en la actividad del corazón.Esto puede afectar directamente la amplitud de la señal del pulso y hace que la CPT sea una herramienta valiosa para estudiar sistemas basados en variables plethsmográficas [12].

A su vez la técnica CPT permite examinar si un sistema dado de adquisición y procesamiento de datos es capaz de registrar las reacciones fisiológicas asociadas a un estímulo controlado. Sin embargo la reacción que será provocada por el procedimiento dado no puede considerarse como un solo indicador del dolor ya que el estímulo frío provoca efectos relacionados con la temperatura [12].


# III. Resultados.


El código desarrollado en MATLAB tiene como objetivo **simular una señal PPG (Photoplethysmography)** y posteriormente identificar sus principales características, especialmente los **picos sistólicos y los valles**.

La señal se genera de manera artificial intentando incluir algunas características presentes en una señal PPG real, como la variación de la frecuencia cardíaca, cambios de amplitud entre latidos, onda dicrótica, muesca dicrótica, variación respiratoria y ruido.

Después de generar y suavizar la señal, se utiliza el **método MMPD**, denominado en el código como **método del alpinista**, para detectar los picos y valles. Finalmente, se calculan diferentes parámetros fisiológicos y se evalúa el desempeño del algoritmo comparando las detecciones con los latidos verdaderos utilizados para generar la simulación.

---

## 1. Configuración de la simulación

```matlab
Fs = 100;
T = 30;

t = 0:1/Fs:T-1/Fs;
N = length(t);

rng(10);
```

La simulación utiliza una frecuencia de muestreo de **100 Hz** y una duración de **30 segundos**.

La frecuencia de muestreo determina cada cuánto tiempo se toma una muestra:

$$
\Delta t=\frac{1}{F_s}=0.01\;s
$$

Por lo tanto, para 30 segundos se generan aproximadamente **3000 muestras**.

La instrucción `rng(10)` fija la semilla de generación de números aleatorios. Esto es importante porque el código utiliza valores aleatorios para simular variaciones fisiológicas y ruido. Al mantener la misma semilla, los resultados pueden reproducirse en diferentes ejecuciones.

---

## 2. Generación de los latidos cardíacos

Se establece una frecuencia cardíaca base de:

```matlab
HR_base = 72;
```

es decir, **72 BPM**.

El primer latido se establece en `0.8 s` y posteriormente se generan los siguientes latidos utilizando una frecuencia cardíaca que cambia ligeramente.

```matlab
HR_actual = HR_base ...
    + 3*sin(2*pi*beat_times(end)/15) ...
    + 0.8*randn;
```

La variación está compuesta por una parte periódica y otra aleatoria. Esto evita que todos los latidos aparezcan exactamente separados por el mismo tiempo.

Para cada latido se calcula el intervalo RR mediante:

$$
RR=\frac{60}{HR}
$$

Por ejemplo, para una frecuencia de 72 BPM:

$$
RR=\frac{60}{72}\approx0.833\;s
$$

El tiempo del siguiente latido se obtiene sumando este intervalo al tiempo del latido anterior.

---

## 3. Construcción de la señal PPG

Inicialmente se crea una señal de ceros:

```matlab
ppg = zeros(size(t));
```

Después, para cada latido se genera una forma de onda individual y se van sumando todos los pulsos.

### Pulso sistólico

El componente principal del latido se genera mediante:

```matlab
pulso(idx) = (x/0.10).^2 .* exp(-x/0.14);
```

Esta función permite obtener una forma de onda con un **ascenso relativamente rápido y un descenso más lento**, característica de la morfología de un pulso PPG.

El pulso se normaliza para que su amplitud máxima sea aproximadamente igual a 1.

---

## 4. Variación de amplitud

Para hacer que los latidos sean menos ideales, cada pulso tiene una pequeña variación de amplitud:

```matlab
amp = 0.85 ...
    * (1 + 0.05*sin(k)) ...
    * (1 + 0.025*randn);
```

Esto representa de forma simplificada la variabilidad que puede existir entre diferentes latidos.

Por lo tanto, aunque la forma general de los pulsos sea similar, no todos presentan exactamente la misma amplitud.

---

## 5. Onda y muesca dicrótica

Además del pulso sistólico principal, se agregan dos características secundarias.

### Onda dicrótica

```matlab
dic(idx_dic) = ...
    0.12 * ...
    exp(-((xd(idx_dic))/0.075).^2);
```

La onda dicrótica es una pequeña elevación que aparece durante la fase descendente de la señal PPG.

### Muesca dicrótica

```matlab
notch(idx_notch) = ...
    -0.035 * ...
    exp(-((xn(idx_notch))/0.035).^2);
```

La muesca dicrótica representa una pequeña disminución que aparece antes de la onda dicrótica.

Finalmente, todos los componentes se combinan:

```matlab
ppg = ppg + amp*pulso + dic + notch;
```

De esta forma, cada latido está compuesto por el pulso principal y sus características secundarias.

---

## 6. Línea base y variación respiratoria

Después de generar todos los latidos, la señal se normaliza:

```matlab
ppg = ppg / max(ppg);
```

y se establece una línea base:

```matlab
ppg = 0.25 + 0.70*ppg;
```

También se agrega una variación lenta asociada a la respiración:

```matlab
resp = 0.025*sin(2*pi*0.23*t);
ppg = ppg + resp;
```

La frecuencia utilizada es de `0.23 Hz`, que corresponde aproximadamente a:

$$
0.23\times60=13.8
$$

respiraciones por minuto.

Esta variación permite representar de manera sencilla cómo la respiración puede modificar lentamente la amplitud de una señal PPG.

---

## 7. Adición de ruido y suavizado

Para acercar la simulación a condiciones más realistas, se agrega ruido aleatorio:

```matlab
ruido = 0.008*randn(size(t));
ppg = ppg + ruido;
```

El ruido representa pequeñas perturbaciones que pueden aparecer durante la adquisición de una señal fisiológica.

Posteriormente se aplica un promedio móvil:

```matlab
ppg = movmean(ppg,3);
```

El suavizado reduce las fluctuaciones rápidas producidas por el ruido, facilitando la detección de los picos y valles sin modificar demasiado la forma general de la señal.

---

# 8. Detección mediante el método MMPD

Para detectar los picos se utiliza el método MMPD, denominado en el código **método del alpinista**.

La idea principal es analizar si la señal está **subiendo o bajando** y contar cuántos pasos consecutivos de subida presenta.

Inicialmente se establece:

```matlab
num_upsteps = 0;
threshold = 6;
```

El `threshold` corresponde al número mínimo de pasos ascendentes necesarios para considerar que puede existir un pico.

---

## Funcionamiento del detector

El algoritmo recorre la señal muestra por muestra.

Cuando:

```matlab
ppg(i) > ppg(i-1)
```

significa que la señal está subiendo y se incrementa el contador:

```matlab
num_upsteps = num_upsteps + 1;
```

Mientras la señal sube también se guarda la posición de un posible valle.

Cuando la señal deja de subir y comienza a bajar, el algoritmo revisa el número de pasos acumulados.

Si:

```matlab
num_upsteps >= threshold
```

se considera que se ha encontrado un **posible pico sistólico**.

El algoritmo guarda su posición y continúa analizando la señal para confirmar cuál fue realmente el punto máximo.

---

## 9. Detección de los valles

Una vez confirmado un pico, se busca el punto mínimo de la señal entre el pico anterior y el pico actual:

```matlab
[valor_valle,posicion_valle] = ...
    min(ppg(inicio_valle:fin_valle));
```

De esta manera, cada ciclo queda caracterizado aproximadamente por:

```text
Valle → Ascenso sistólico → Pico → Descenso → Valle
```

Los tiempos y amplitudes de estos puntos se almacenan en:

* `peak_times`
* `peaks`
* `valley_times`
* `valleys`

---

## 10. Umbral adaptativo

Una característica importante del algoritmo es que el umbral se modifica después de detectar cada pico:

```matlab
threshold = 0.6 * upsteps_at_peak;
```

Es decir, el nuevo umbral corresponde al **60 % de los pasos ascendentes registrados para el pico anterior**.

Esto permite que el detector se adapte al comportamiento de la señal en lugar de utilizar siempre un valor fijo.

---

# 11. Cálculo de parámetros fisiológicos

Una vez detectados los picos y valles, se calculan diferentes parámetros de la señal.

### Intervalo RR

Se obtiene mediante la diferencia entre los tiempos de picos consecutivos:

$$
RR_i=t_{pico(i+1)}-t_{pico(i)}
$$

En MATLAB:

```matlab
RR = diff(peak_times);
```

### Frecuencia cardíaca

A partir de cada intervalo RR:

$$
FC=\frac{60}{RR}
$$

```matlab
FC = 60 ./ RR;
```

Finalmente se calcula la frecuencia cardíaca promedio.

---

## 12. PPGA

La **PPGA (Photoplethysmographic Pulse Amplitude)** se obtiene como la diferencia entre la amplitud del pico y la amplitud del valle:

$$
PPGA=Pico-Valle
$$

En el código:

```matlab
PPGA = peaks(1:num_pulsos) - valleys(1:num_pulsos);
```

Después se calcula el valor promedio:

```matlab
PPGA_promedio = mean(PPGA);
```

Este parámetro permite conocer la amplitud promedio de los pulsos detectados.

---

## 13. Tiempo de subida sistólica

El tiempo de subida se obtiene restando el tiempo del valle al tiempo del pico:

$$
T_{subida}=T_{pico}-T_{valle}
$$

En el código:

```matlab
tiempo_subida(k) = ...
    peak_times(k) - valley_times(k);
```

Posteriormente se calcula el promedio de todos los latidos.

---

# 14. Tabla de resultados

El código genera una tabla que permite analizar los resultados **latido por latido**.

```matlab
Resultados = table(...)
```

La tabla contiene:

| Variable      | Descripción         |
| ------------- | ------------------- |
| `Latido`      | Número del latido   |
| `TiempoValle` | Instante del valle  |
| `TiempoPico`  | Instante del pico   |
| `Pico`        | Amplitud del pico   |
| `Valle`       | Amplitud del valle  |
| `PPGA_tabla`  | Amplitud del pulso  |
| `RR_tabla`    | Intervalo RR        |
| `FC_tabla`    | Frecuencia cardíaca |

Esto permite observar tanto los valores individuales como las variaciones existentes entre diferentes latidos.

---

# 15. Visualización de la señal

Se generan dos gráficas.

La primera muestra los **30 segundos completos** de la señal PPG, mientras que la segunda realiza un acercamiento entre los segundos 1 y 6.

Los elementos principales se representan de la siguiente manera:

* **Señal PPG:** onda completa.
* **Puntos rojos:** picos sistólicos detectados.
* **Puntos verdes:** valles detectados.

Estas gráficas permiten comprobar visualmente si el algoritmo está ubicando los puntos característicos de cada pulso en posiciones adecuadas.

---

# 16. Evaluación del algoritmo

Una ventaja de trabajar con una señal simulada es que se conocen los tiempos reales de los latidos mediante `beat_times`.

Por esto, los picos detectados pueden compararse con los valores verdaderos.

Se utiliza una tolerancia de:

```matlab
tolerancia = 0.05;
```

correspondiente a **50 ms**.

Si un pico detectado se encuentra dentro de esta tolerancia respecto a un latido verdadero, se considera una detección correcta.

Se calculan:

### TP — Verdaderos positivos

Latidos reales que fueron detectados correctamente.

### FN — Falsos negativos

Latidos reales que no fueron detectados.

### FP — Falsos positivos

Picos detectados que no corresponden a un latido real.

---

## 17. Indicadores de desempeño

### Sensibilidad

$$
Sensibilidad=\frac{TP}{TP+FN}\times100
$$

Indica qué porcentaje de los latidos reales fueron detectados por el algoritmo.

### Precisión

$$
Precisión=\frac{TP}{TP+FP}\times100
$$

Indica qué porcentaje de las detecciones realizadas por el algoritmo fueron correctas.

### Tasa de detección fallida

El código también calcula:

$$
FDR=\frac{FN+FP}{TP}\times100
$$

Este indicador combina los errores asociados con falsos positivos y falsos negativos respecto a los verdaderos positivos. En este proyecto se utiliza como una medida adicional del desempeño del detector.

---

# 18. Flujo general del código

```text
Configuración de parámetros
          ↓
Generación de latidos
          ↓
Construcción del pulso PPG
          ↓
Onda y muesca dicrótica
          ↓
Línea base + respiración
          ↓
Ruido
          ↓
Suavizado
          ↓
Detección MMPD
          ↓
Picos y valles
          ↓
Cálculo de RR y FC
          ↓
Cálculo de PPGA
          ↓
Tiempo de subida sistólica
          ↓
Comparación con latidos reales
          ↓
TP, FP y FN
          ↓
Sensibilidad y precisión
```

---

Como no fue posbile completar satisfactoriamente la adquisición experimental de la señal PPG a través del circuito desarrollado se realizó una simulación en MATLAB con el objetivo de desarrollar la etapa de procesamiento de la señal necesaria. De esta manera fue posible llevar a cabo la generación de una señal PPG y aplicar sobre ella el algoritmo de detección de máximo y mínimo utilizando el Método de Detección de Pico del Mountaineer (MMPD).

Esto se hizo por 30 segundos y con una frecuencia de muestreo de 100 Hz lo cual dio como resultado 3000 muestras. La señal fue generada mediante la incorporación de cambios en las amplitudes de los pulsos,pequeños cambios en la frecuencia cardíaca así como en la línea base y ruido de baja amplitud. Esto se hizo con el objetivo de generar una señal PPG simulada que se asemeje a una señal fisiológica.

<p align="center">
<img width="1046" height="618" alt="WhatsApp Image 2026-09-15 at 7 40 50 PM" src="https://github.com/user-attachments/assets/5cc203d0-b0db-4e07-b308-21694a38d9a3" />
</p>

<p align="center">
  <sub>Figura 1. Señal PPG simulada durante 30 s y detección de picos sistólicos y valles mediante el Método del Alpinista. Tomado de: Elaboración propia.</sub>
</p>

La Figura 1 presenta la señal simulada de PPG para el intervalo de 30 segundos. Se puede observar que hay una serie de pulsos correspondientes a diferentes ciclos cardíacos con variaciones en la amplitud y el tiempo entre ellos. Los puntos rojos indican los picos sistólicos detectados utilizando el Método Climber mientras que los puntos verdes representan los valles detectados. Es posible analizar la ubicación de los puntos a lo largo de toda la señal. Es interesante notar que existen algunas variaciones en la línea base y la forma de los pulsos. Además la señal completa puede ser analizada con sus puntos característicos ubicados por el algoritmo.

<p align="center">
<img width="1000" height="626" alt="WhatsApp Image 2026-09-15 at 7 41 05 PM" src="https://github.com/user-attachments/assets/ae447a84-7507-4c23-82a5-769aad7223b9" />
</p>

<p align="center">
  <sub>Figura 2. Detalle de la señal PPG simulada entre 1 y 6 s, mostrando la detección de los picos sistólicos y valles mediante el algoritmo MMPD. Tomado de: Elaboración propia.</sub>
</p>


