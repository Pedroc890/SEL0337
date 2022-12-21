# SEL0337

Relatório Prática 6

Projetos em Sistemas Embarcados - SEL0337

Prof. Pedro de Oliveira C. Junior

Matheus Marques Jacobsen - 10312403

Pedro Cavallini - 11801007

São Carlos, 21 de dezembro de 2022

## Prática 6 - Introdução a interfaces de visão computacional, sistemas de versionamento de arquivos e APIs públicas

### Introdução

Esta prática tem como objetivo o estudo de três tópicos: interfaces de visão computacional, sistemas de controle de versão e uso de APIs públicas. Para o tópico de visão computacional, foi abordado a utilização do módulo de câmera embarcado próprio da RaspBerry Pi e sua integração com Python através do módulo PiCamera. Já para sistemas de controle de versão, foi exemplificado o uso desses sistemas no desenvolvimento de software através dos próprios códigos e arquivos desenvolvidos na prática, utilizando o GitHub como plataforma de hospedagem desses arquivos. Por fim, visando o estudo de APIs públicas, foi utilizada a API de clima da Oracle para realizar um código em Python capaz de obter os dados de uma estação específica.

### Desenvolvimento

A fim de abordar de maneira mais detalhada as atividades desenvolvidas nesta prática, estas serão divididas nos três tópicos trabalhados.

#### Introdução a interfaces de visão computacional

Primeiramente, foi conectada a câmera no slot próprio para ela na RaspBerry Pi. Em seguida, foram habilitadas as interfaces da câmera e da conexão I2C a fim de garantir a conexão com o código em Python. Dessa forma, foi desenvolvido o script em Python abaixo:

```python
from time import sleep
from picamera import PiCamera

camera = PiCamera()
camera.resolution = (1024, 768)
camera.start_preview()
sleep(30)
camera.capture('sel0337.jpg')
```

Com isso, foi possível obter da cãmera a imagem abaixo:

<img src="/sel0337.jpg" alt="PiCamera" width="500"/>


#### Sistemas de versionamento de arquivos

Durante a execução dos scripts dos outros tópicos dessa prática e adição de arquivos a mesma, todo esse conteúdo foi para esta pasta do GitHub a fim de se aprender os comandos básicos do mesmo:

- *git clone <repository>*: clona um repositório para a pasta local
- *git add*: adiciona as mudanças feitas no diretório de trabalho
- *git commit -a -m "mensagem"*: guarda o estado do repositório com uma mensagem
- *git push*: envia o conteúdo salvo do repositório para um repositório remoto

#### APIs públicas

Foi construído o script em Python abaixo utilizando a API de clima da Oracle a fim de extrair os dados climáticos de uma base instalada na UFSC, cujo ID é 966583:

```python
from requests import get
import json
from pprint import pprint

stations = 'https://apex.oracle.com/pls/apex/raspberrypi/weatherstation/getallstations'
weather = 'https://apex.oracle.com/pls/apex/raspberrypi/weatherstation/getlatestmeasurements/'

weather = weather + '966583'

my_weather = get(weather).json()['items']
pprint(my_weather)
```

Dessa forma, a resposta obtida da base climática foi:

```
[{'air_pressure': 1010.51,
  'air_quality': 48.8,
  'ambient_temp': 29.93,
  'created_by': 'UFSC',
  'created_on': '2018-09-27T16:10:21Z',
  'ground_temp': 23.06,
  'humidity': 46.42,
  'id': 13228613,
  'rainfall': 0,
  'reading_timestamp': '2018-09-27T16:10:21Z',
  'updated_by': 'UFSC',
  'updated_on': '2018-10-04T15:35:19.899Z',
  'weather_stn_id': 966583,
  'wind_direction': 90,
  'wind_gust_speed': 0,
  'wind_speed': 0}]
```
