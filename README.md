# fase6cap1
# Projeto Fase 6 - YOLOv5 (Banana e Garrafa)

Este projeto faz parte da Fase 6 da FIAP, na disciplina de Inteligência Artificial. O objetivo foi criar um modelo de visão computacional usando o YOLOv5 para identificar dois objetos: **banana** e **garrafa**. 
As imagens foram rotuladas no MakeSense.ai e organizadas em pastas de treino, validação e teste dentro do Google Drive. O trabalho foi feito no Google Colab com integração ao YOLOv5.

Foram realizados dois treinos para comparação: um com **30 épocas** e outro com **60 épocas**. O modelo de 60 épocas apresentou melhor desempenho, com mais acertos nas detecções e melhor mAP. As imagens de teste mostraram que o YOLOv5 conseguiu identificar corretamente as classes na maioria dos casos.

As etapas principais foram:
1. Montar o Google Drive no Colab.
2. Clonar o repositório do YOLOv5 e instalar as dependências.
3. Executar o treino do modelo com o comando:  
   `python train.py --img 640 --batch 16 --epochs 60 --data /content/drive/MyDrive/dataset_yolo/data.yaml --weights yolov5s.pt`
4. Fazer a inferência com o modelo treinado para testar nas imagens de `/test`.
5. Comparar os resultados entre os dois treinos.

Mesmo com uma base pequena de imagens (cerca de 80), o modelo teve bom desempenho. Como melhoria, seria interessante aumentar o dataset, aplicar técnicas de data augmentation e testar outras versões do YOLO (como yolov5m ou yolov5l).

📘 Notebook Colab: [Abrir aqui](https://colab.research.google.com/drive/1vCccYQXcjkOQeCdrnp1lhiGr7IvJORoa)  
🎥 Vídeo de demonstração: *(adicionar link do YouTube)*  

Durante os testes realizados com o YOLOv5, foi possível observar diferenças claras entre o treino com 30 épocas e o treino com 60 épocas.  
Os resultados ficaram salvos nas pastas geradas automaticamente pelo YOLOv5:  
`/content/yolov5/runs/detect/expA_test` e `/content/yolov5/runs/detect/expB_test`.

O modelo treinado com **60 épocas** apresentou melhor desempenho geral, com maior precisão e recall. Ele conseguiu detectar com mais facilidade as **bananas** e as **garrafas**, mesmo quando as imagens tinham variações de iluminação e posição.  
Já o modelo com **30 épocas** foi mais rápido para treinar, mas teve alguns erros de detecção em imagens mais complexas.

Nos testes de validação, as métricas mostraram uma melhora no **mAP** e na **precisão** conforme o número de épocas aumentou, comprovando que o modelo aprendeu melhor os padrões das classes.  
As imagens processadas (armazenadas em `yolov5/runs/detect/expX`) mostram claramente as detecções corretas, com caixas delimitando os objetos e o nome da classe identificado.

De forma geral, os resultados foram positivos. Mesmo com um dataset pequeno, o YOLOv5 conseguiu alcançar bons índices de acerto.  
Como melhorias futuras, seria interessante:
- Aumentar a quantidade e diversidade de imagens no dataset;  
- Aplicar **data augmentation** para melhorar a generalização;  
- Testar outras arquiteturas do YOLO, como **yolov5m** ou **yolov5l**;  

Em resumo, o projeto atingiu seu objetivo de demonstrar como um modelo de visão computacional pode identificar objetos específicos com boa precisão, validando o funcionamento prático da rede neural YOLOv5.

Feito por **Vivian Amorim**  
FIAP • Curso de Inteligência Artificial • Fase 6
