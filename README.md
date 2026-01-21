# Segmentação Semântica de Mitocôndrias com U-Net

Este projeto implementa uma **U-Net do zero em Keras/TensorFlow** para realizar **segmentação semântica de mitocôndrias** em imagens de microscopia eletrônica.  
Todo o pipeline foi desenvolvido em **Python**, executado no **Google Colab**, e cobre desde o carregamento dos dados até a avaliação quantitativa e visual dos resultados.

---

## 🧬 Contexto do Projeto

A segmentação de estruturas celulares é um problema clássico em **visão computacional aplicada à biomedicina**.  
Neste projeto, o objetivo é identificar automaticamente **regiões de mitocôndrias** em imagens grayscale, produzindo máscaras binárias pixel a pixel.

O modelo utilizado é a **U-Net**, arquitetura amplamente empregada em tarefas de segmentação biomédica devido às suas *skip connections*, que preservam detalhes espaciais finos.

---

## 📂 Dataset

- Imagens de microscopia eletrônica em escala de cinza (`.tif`)
- Máscaras binárias correspondentes (`.tif`)
- Resolução: **256 × 256**
- Dataset baixado automaticamente via link público (arquivo `.zip`)

Estrutura após extração:

256/

├── images/

│ └── *.tif

└── masks/


└── *.tif


---

## 🔄 Pipeline do Projeto

1. Download e extração automática do dataset  
2. Leitura e organização de imagens e máscaras  
3. Normalização dos pixels (0–1)  
4. Divisão em treino e teste  
5. Implementação manual da arquitetura **U-Net**  
6. Treinamento supervisionado  
7. Avaliação com métricas apropriadas para segmentação  
8. Visualização das predições  

---

## 🧠 Arquitetura do Modelo

O modelo segue a arquitetura clássica da **U-Net**, composta por:

- **Encoder (Downsampling)**  
  Blocos convolucionais com `Conv2D + BatchNormalization + ReLU` e `MaxPooling`

- **Bridge**  
  Camada mais profunda da rede com maior número de filtros

- **Decoder (Upsampling)**  
  `Conv2DTranspose`, *skip connections* e novos blocos convolucionais

- **Saída**
  - 1 canal
  - Ativação `sigmoid`
  - Segmentação binária (mitocôndria vs fundo)

---

## ⚙️ Configuração de Treinamento

- Otimizador: **Adam**
- Learning rate: `1e-3`
- Loss: **Binary Crossentropy**
- Batch size: `16`
- Épocas: `30`
- Shuffle: `False`

---

## 📊 Métricas Utilizadas

Além da acurácia pixel a pixel, foram usadas métricas mais adequadas para segmentação:

- **Dice Coefficient**
- **IoU (Intersection over Union)**
- **Precision**
- **Recall**
- **Binary Accuracy (com threshold 0.5)**

Essas métricas permitem avaliar melhor a sobreposição entre predição e máscara real.

---

## 📈 Resultados

Durante o treinamento, são gerados gráficos de:

- Loss (treino e validação)
- Accuracy
- Dice Coefficient
- Precision
- Recall

Além disso, o projeto inclui **inferência visual**, comparando:

- Imagem original  
- Máscara real (ground truth)  
- Máscara predita pelo modelo  

---

## 💾 Salvamento do Modelo

O modelo treinado é salvo em disco no formato `.hdf5`, permitindo:

- Reuso posterior
- Avaliação sem necessidade de retreinamento
- Deploy futuro

---

## 🚀 Como Executar

1. Abra o notebook no Google Colab  
2. Execute as células em ordem  
3. O dataset será baixado automaticamente  
4. O treinamento será iniciado após o pré-processamento  

Notebook Colab:  
👉 https://colab.research.google.com/drive/1LKnQIgs7KLYpeMzZysGZCPGTWymeYZ2_

---

## 🛠️ Tecnologias Utilizadas

- Python
- TensorFlow / Keras
- NumPy
- OpenCV
- Matplotlib
- Scikit-learn
- Google Colab

---

## 📌 Observações

Este projeto tem foco **educacional e demonstrativo**, com ênfase em:
- entendimento da arquitetura U-Net
- métricas corretas para segmentação
- boas práticas em pipelines de visão computacional

---

## 📜 Licença

Projeto desenvolvido para fins de estudo e portfólio.
