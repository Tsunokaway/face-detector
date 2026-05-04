# 🥷 Jujutsu Kaisen Hand Signs Detector

> Projeto de visão computacional para reconhecimento de hand signs do anime Jujutsu Kaisen em tempo real, utilizando YOLOv8 e dataset customizado.

---

## 🎯 Objetivo

Treinar um modelo de detecção de objetos capaz de identificar os **5 signos cursed** do JJK a partir de imagens e vídeo em tempo real:

| Classe | Signo |
|--------|-------|
| `wolf` | Signo do Lobo |
| `gojo` | Signo do Gojo |
| `nue` | Signo do Nue |
| `sukuna` | Signo do Sukuna |
| `toad` | Signo do Sapo |

---

## 🗺️ Arquitetura do Projeto

```
┌─────────────────────────────────────────────────────┐
│              1. COLETA DO DATASET                   │
│                                                     │
│  Roboflow Universe → Fork → 980 imagens, 5 classes  │
└─────────────────────┬───────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────┐
│            2. PREPARAÇÃO NO ROBOFLOW                │
│                                                     │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐ │
│  │ Train 70%   │  │Augmentation │  │Export YOLOv8│ │
│  │ Val   20%   │  │980 → 2353   │  │  data.yaml  │ │
│  │ Test  10%   │  │  imagens    │  │  + snippet  │ │
│  └─────────────┘  └─────────────┘  └─────────────┘ │
└─────────────────────┬───────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────┐
│             3. TREINO COM YOLOv8                    │
│                                                     │
│  Ambiente : Google Colab (GPU T4)                   │
│  Modelo   : yolov8n.pt (pré-treinado)               │
│  Épocas   : 50                                      │
│  Imgsz    : 640                                     │
│                                                     │
│  Output → runs/detect/train/weights/best.pt         │
└─────────────────────┬───────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────┐
│           4. AVALIAÇÃO DOS RESULTADOS               │
│                                                     │
│  mAP@50          → precisão geral do modelo         │
│  Matriz confusão → quais classes são confundidas    │
│  Loss curves     → evolução do aprendizado          │
└─────────────────────┬───────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────┐
│            5. DEPLOY / DEMONSTRAÇÃO                 │
│                                                     │
│  • Detecção em tempo real via webcam                │
│  • Interface web com Streamlit                      │
│  • Demo publicado no GitHub                         │
└─────────────────────────────────────────────────────┘
```

---

## 🛠️ Stack Tecnológica

| Ferramenta | Função |
|------------|--------|
| [Roboflow](https://roboflow.com) | Gerenciamento e preparação do dataset |
| [YOLOv8](https://github.com/ultralytics/ultralytics) | Modelo de detecção de objetos |
| [Google Colab](https://colab.research.google.com) | Ambiente de treino com GPU |
| [OpenCV](https://opencv.org) | Captura e processamento de vídeo |
| [Streamlit](https://streamlit.io) | Interface web para demonstração |

---

## 📁 Estrutura de Pastas

```
jjk-hand-signs-detector/
│
├── data/                        # Dataset exportado do Roboflow
│   ├── images/
│   │   ├── train/
│   │   ├── valid/
│   │   └── test/
│   └── labels/
│       ├── train/
│       ├── valid/
│       └── test/
│
├── runs/                        # Resultados do treino (gerado automaticamente)
│   └── detect/
│       └── train/
│           └── weights/
│               └── best.pt      # Modelo treinado
│
├── src/
│   ├── train.py                 # Script de treino
│   ├── detect.py                # Inferência em imagem/vídeo
│   └── webcam.py                # Detecção em tempo real
│
├── app.py                       # Interface Streamlit
├── data.yaml                    # Configuração das classes
├── requirements.txt
└── README.md
```

---

## ⚙️ Como Rodar

### 1. Clone o repositório
```bash
git clone https://github.com/seu-usuario/jjk-hand-signs-detector
cd jjk-hand-signs-detector
```

### 2. Instale as dependências
```bash
pip install -r requirements.txt
```

### 3. Baixe o dataset
```python
from roboflow import Roboflow
import os

rf = Roboflow(api_key=os.environ.get("ROBOFLOW_API_KEY"))
project = rf.workspace("yasmin-tsunokawa").project("jujutsu-kaisen-hand-signs-upire")
version = project.version(1)
dataset = version.download("yolov8")
```

### 4. Treine o modelo
```bash
yolo task=detect mode=train \
  model=yolov8n.pt \
  data=data.yaml \
  epochs=50 \
  imgsz=640
```

### 5. Rode a detecção em tempo real
```bash
python src/webcam.py
```

### 6. Rode a interface web
```bash
streamlit run app.py
```

---

## 📊 Resultados

> ⏳ Seção a ser preenchida após o treino.

| Métrica | Valor |
|---------|-------|
| mAP@50 | - |
| Precision | - |
| Recall | - |
| Épocas | 50 |

---

## Estrutura do projeto

- `face-detector/`
  - `data.yaml` - configuração do conjunto de dados para treinamento e validação.
  - `requirements.txt` - dependências Python necessárias.
  - `data/`
    - `images/`
      - `train/` - imagens de treino.
      - `val/` - imagens de validação.
      - `test/` - imagens de teste.
    - `labels/` - arquivos de anotação correspondentes às imagens.
  - `notebooks/`
    - `exploratory.ipynb` - notebook para exploração dos dados e análise inicial.
  - `runs/` - resultados de treino e checkpoints gerados.
  - `src/`
    - `detect.py` - script para detecção de faces em imagens usando o modelo treinado.
    - `train.py` - script para treinar o detector de faces.
    - `webcam.py` - script para captura em tempo real com webcam.



## Pré-requisitos

- Python 3.8+ (recomendado)
- Ambiente virtual (`venv`, `virtualenv`, `conda`, etc.)

## Instalação

1. Navegue até a pasta do projeto:

```powershell
cd "c:\Users\tsuno\projetos pessoais\visao-computacional\face-detector"
```

2. Crie e ative um ambiente virtual:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

3. Instale as dependências:

```powershell
pip install -r requirements.txt
```


## Dados e anotações

- As imagens devem estar organizadas em `data/images/train`, `data/images/val` e `data/images/test`.
- As anotações correspondentes ficam em `data/labels` e devem seguir o mesmo padrão do conjunto de dados usado pelo detector.
- O arquivo `data.yaml` define os caminhos e classes usados durante o treinamento.

---


## 📌 Próximos Passos

- [ ] Treinar modelo no Google Colab
- [ ] Avaliar métricas e ajustar hiperparâmetros
- [ ] Implementar detecção via webcam
- [ ] Criar interface com Streamlit
- [ ] Publicar demo no GitHub Pages

---

## 👩‍💻 Autora

Feito por **Yasmin Tsunokawa** como projeto de portfólio em Visão Computacional.