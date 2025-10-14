# fase6cap1
# Projeto Fase 6 - YOLOv5 (Banana e Garrafa)

Este projeto foi desenvolvido na Fase 6 do curso de Inteligência Artificial da FIAP, no desafio FarmTech Solutions. O objetivo foi criar um modelo de visão computacional com YOLOv5 capaz de identificar bananas e garrafas em imagens. O trabalho foi feito no Google Colab, usando o Google Drive para armazenar o dataset e o MakeSense.ai para rotular as imagens. Foram realizados dois treinos, um com 30 épocas e outro com 60 épocas, para comparar o aprendizado e o desempenho da rede.

O dataset foi organizado em pastas de treino, validação e teste dentro do Drive: https://drive.google.com/drive/folders/1C_-ohKDnivyeTXWgBuGyBrxXZXDTZhB-  
A estrutura ficou assim:
dataset_yolo/
 ├── train/
 │   ├── banana/
 │   └── garrafa/
 ├── val/
 │   ├── banana/
 │   └── garrafa/
 ├── test/
 │   ├── banana/
 │   └── garrafa/
 └── data.yaml

O arquivo data.yaml contém:
train: /content/drive/MyDrive/dataset_yolo/train  
val: /content/drive/MyDrive/dataset_yolo/val  
test: /content/drive/MyDrive/dataset_yolo/test  
nc: 2  
names: ['banana', 'garrafa']

No Colab, o processo foi feito em cinco etapas:
1. Montar o Google Drive e instalar o YOLOv5:
from google.colab import drive
drive.mount('/content/drive')
!git clone https://github.com/ultralytics/yolov5
%cd /content/yolov5
!pip install -r requirements.txt --quiet


2. Treinar os modelos:
- Modelo A (30 épocas):
  ```
  python train.py --img 640 --batch 16 --epochs 30 --data /content/drive/MyDrive/dataset_yolo/data.yaml --weights yolov5s.pt --project runs/train --name expA --exist-ok
  ```
- Modelo B (60 épocas):
  ```
  python train.py --img 640 --batch 16 --epochs 60 --data /content/drive/MyDrive/dataset_yolo/data.yaml --weights yolov5s.pt --project runs/train --name expB --exist-ok
  ```
3. Fazer a inferência nas imagens de teste:
python detect.py --weights runs/train/expB/weights/best.pt --source /content/drive/MyDrive/dataset_yolo/test --project runs/detect --name expB_test --exist-ok

4. Comparar os resultados lendo os arquivos results.csv dos dois treinos.
5. Visualizar as imagens geradas nas pastas yolov5/runs/detect/expA_test e yolov5/runs/detect/expB_test.

Resultados e comparações:
- Treino de 30 épocas: https://drive.google.com/drive/folders/1uyQbL4YneRf2E-6yVJxL0UHO67Ct7mul  
- Treino de 60 épocas: https://drive.google.com/drive/folders/1X0Rx18yCsEFk9wmiFi6lulVm5TyjxsEM  

Métricas aproximadas:
| Modelo | Épocas | Precision | Recall | mAP@0.5 | mAP@0.5:0.95 |
|:-------|:-------:|:----------:|:--------:|:--------:|:-------------:|
| YOLOv5s (30) | 30 | 0.85 | 0.80 | 0.87 | 0.68 |
| YOLOv5s (60) | 60 | 0.91 | 0.88 | 0.93 | 0.74 |

Conclusões:
O modelo de 60 épocas apresentou melhor desempenho geral, com métricas mais altas e detecções mais precisas. O de 30 épocas teve um bom resultado inicial, mas com mais erros em imagens de ângulo ou iluminação diferentes. Mesmo com um dataset pequeno, o YOLOv5 mostrou bom aprendizado. A precisão e o recall indicaram que o modelo conseguiu identificar corretamente a maioria dos objetos com poucos falsos positivos e falsos negativos. As imagens processadas mostraram caixas de detecção bem posicionadas e confiáveis. O aumento das épocas ajudou o modelo a aprender melhor as características das classes.

Melhorias futuras:
- Aumentar o número de imagens no dataset;
- Aplicar data augmentation;
- Testar versões maiores do YOLO (v5m, v5l);
- Avaliar detecção em vídeo ou câmera ao vivo.

Links:
- 📘 Notebook no Colab: https://colab.research.google.com/drive/1vCccYQXcjkOQeCdrnp1lhiGr7IvJORoa  
- 📁 Dataset: https://drive.google.com/drive/folders/1C_-ohKDnivyeTXWgBuGyBrxXZXDTZhB-  
- 📁 Resultados 30 épocas: https://drive.google.com/drive/folders/1uyQbL4YneRf2E-6yVJxL0UHO67Ct7mul  
- 📁 Resultados 60 épocas: https://drive.google.com/drive/folders/1X0Rx18yCsEFk9wmiFi6lulVm5TyjxsEM  


Vivian Amorim 565078
Ana Carolina Belchior 565875
Leonardo De Sena 563351
FIAP – Curso de Inteligência Artificial  
Fase 6 – FarmTech Solutions • 2025
Em resumo, o projeto atingiu seu objetivo de demonstrar como um modelo de visão computacional pode identificar objetos específicos com boa precisão, validando o funcionamento prático da rede neural YOLOv5.


