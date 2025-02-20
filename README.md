# 🖼️ Criação de uma Base de Dados e Treinamento da Rede YOLO  

Bem-vindo(a)! Este repositório contém um guia completo para configurar o YOLO (You Only Look Once) utilizando o framework Darknet. Você aprenderá a configurar o ambiente, criar uma base de dados personalizada e realizar detecção de objetos com um dos modelos mais eficientes de visão computacional.  

---

## 🚀 Objetivos  

1. Verificar a disponibilidade de GPU no ambiente.  
2. Clonar e configurar o repositório do Darknet.  
3. Ajustar o ambiente para utilizar o YOLO com suporte a GPU, OpenCV e CUDNN.  
4. Realizar detecções em imagens.  
5. Visualizar os resultados utilizando Python e bibliotecas gráficas.  

---

## 🛠️ Pré-requisitos  

Para garantir que tudo funcione corretamente, você precisará dos seguintes itens:  

- **Python** (versão 3.6 ou superior).  
- **TensorFlow** (para verificar GPU).  
- **OpenCV** (para manipulação de imagens).  
- **CUDA** e **cuDNN** (para uso de GPU).  
- **Git** e **Make** (para clonar e compilar).  
- **Matplotlib** (para exibir resultados).  

Certifique-se de que sua GPU está configurada e que os drivers necessários estão instalados.  

---

## 📋 Passo a Passo  

### 1. Verifique a Disponibilidade da GPU  

Antes de começar, veja se a GPU está disponível com o código abaixo:  

```python
import tensorflow as tf
device_name = tf.test.gpu_device_name()
print(device_name)
```

Se a saída incluir algo como `/device:GPU:0`, você está pronto para avançar!  

---

### 2. Clone o Repositório do Darknet  

Utilize o comando abaixo para clonar o repositório:  

```bash
!git clone https://github.com/AlexeyAB/darknet.git
```

> **Nota:** Certifique-se de que o link está correto e de que você tem conexão com a internet.  

---

### 3. Entre no Diretório Clonado  

Navegue até o diretório do Darknet:  

```bash
cd darknet
```

---

### 4. Configure o Makefile  

Para habilitar o uso de GPU, OpenCV e cuDNN, atualize o arquivo `Makefile` com os comandos:  

```bash
!sed -i 's/OPENCV=0/OPENCV=1/g' Makefile
!sed -i 's/GPU=0/GPU=1/g' Makefile
!sed -i 's/CUDNN=0/CUDNN=1/g' Makefile
```

> **Nota:** Caso o arquivo `Makefile` não seja encontrado, revise o processo de clonagem.  

---

### 5. Compile o Darknet  

Rode o comando para compilar o Darknet:  

```bash
!make
```

Se tudo correr bem, você verá a mensagem de sucesso na saída.  

---

### 6. Baixe o Modelo Pré-treinado  

Baixe os pesos do modelo YOLOv4 com o comando:  

```bash
!wget https://github.com/AlexeyAB/darknet/releases/download/yolov4/yolov4.weights
```

---

### 7. Realize a Detecção  

Agora, execute a detecção utilizando o modelo baixado:  

```bash
!./darknet detect cfg/yolov4.cfg yolov4.weights
```

Isso gerará uma imagem de saída com as detecções realizadas.  

---

## 🖼️ Visualização dos Resultados  

Para exibir as imagens com os resultados de forma clara, utilize o seguinte código em Python:  

```python
import cv2
import matplotlib.pyplot as plt

def mostrar(frame):
    imagem = cv2.imread(frame)
    fig = plt.gcf()  # Cria uma figura
    fig.set_size_inches(18, 10)  # Define o tamanho da figura
    plt.axis('off')  # Remove os eixos
    plt.imshow(cv2.cvtColor(imagem, cv2.COLOR_BGR2RGB))  # Converte e exibe a imagem
    plt.show()
```

Substitua `frame` pelo caminho da imagem gerada pela detecção.  

---

## 🛑 Solução de Problemas  

1. **Erro "Repository not found"**  
   - Certifique-se de usar o link correto: `https://github.com/AlexeyAB/darknet.git`.  

2. **Arquivo `Makefile` não encontrado**  
   - Verifique se você está no diretório correto (`cd darknet`).  

3. **Erro na execução do Darknet**  
   - Confirme que os arquivos de pesos e configuração estão no local correto.  

---

## 📚 Conclusão  

Este repositório oferece uma base sólida para criar bases de dados personalizadas e treinar o YOLO para detecção de objetos. Siga os passos descritos para configurar seu ambiente e experimentar os resultados.
