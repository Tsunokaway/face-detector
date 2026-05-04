# Visão Computacional - Detecção de Faces de Personagens de Animes e Jogos

Este projeto reúne um detector de faces focado em personagens de animes e jogos. Ele inclui código para treinar um modelo, testar em imagens e capturar faces em tempo real via webcam.

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

## Objetivo

O objetivo é construir um pipeline de visão computacional capaz de localizar e detectar faces de personagens estilizados de animes e jogos. Isso pode ser usado para:

- analisar expressões e poses de personagens
- experimentar com datasets customizados de arte estilizada
- desenvolver aplicações de reconhecimento e tracking para conteúdo artístico

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

## Uso

### Treinar o modelo

Execute o script de treinamento para ajustar o detector ao seu conjunto de dados:

```powershell
python src\train.py
```

### Detectar faces em imagens

Use o script de detecção para processar imagens com o modelo treinado:

```powershell
python src\detect.py --source path\to\image.jpg
```

### Webcam em tempo real

Inicie a captura em tempo real para detectar faces de personagens diretamente pela webcam:

```powershell
python src\webcam.py
```

## Dados e anotações

- As imagens devem estar organizadas em `data/images/train`, `data/images/val` e `data/images/test`.
- As anotações correspondentes ficam em `data/labels` e devem seguir o mesmo padrão do conjunto de dados usado pelo detector.
- O arquivo `data.yaml` define os caminhos e classes usados durante o treinamento.

## Contribuição

Contribuições são bem-vindas! Você pode melhorar o projeto adicionando:

- mais imagens e rotulagens para personagens distintos
- suporte a diferentes arquiteturas de detecção
- melhorias na interface de webcam e salvamento de resultados

## Licença

Este projeto não possui licença explícita definida no repositório. Adicione um arquivo `LICENSE` se desejar tornar os termos de uso claros.
