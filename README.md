🚗 Estacionamento Seguro: monitoramento de vagas com visão computacional
Sistema em Python que usa visão computacional e Deep Learning (YOLOv8) para contar as vagas livres de um estacionamento em tempo real, a partir de uma câmera lateral fixa. Também emite um alerta sonoro quando uma pessoa é detectada na área monitorada.

Projeto acadêmico (APS) do 6º semestre de Ciência da Computação, UNIP Ribeirão Preto (2025). Disciplina: Processamento Digital de Imagens.

📺 Vídeo de apresentação: https://youtu.be/CmQ4C49IDJ4

✨ Funcionalidades
Detecção de veículos em tempo real com o modelo YOLOv8n (classes carro, moto e caminhão do COCO).
Contagem de vagas livres, exibida em um painel sobre o vídeo (VAGAS LIVRES: x/8).
Alerta de pessoa na área: quando alguém entra no recorte monitorado, o status muda para ALERTA: PESSOA e toca um bipe.
Interface gráfica feita com OpenCV: tela inicial com fundo em gradiente, botões com efeito hover e painel semitransparente.
Controles: iniciar (S ou clique), sair (Q, Esc ou botão SAIR).
🧠 Como funciona
Câmera ─► OpenCV (captura e recorte da área) ─► YOLOv8 (detecção) ─► Contagem ─► Painel / alerta
O OpenCV captura o vídeo da câmera e recorta a região do estacionamento (CROP_AREA).
Cada quadro passa pelo YOLOv8n, que devolve as caixas dos objetos detectados.
As detecções das classes de veículo (2, 3, 7) são contadas, e vagas livres = total de vagas − veículos detectados.
Se for detectada uma pessoa (classe 0), o sistema dispara o alerta sonoro em uma thread separada, para o vídeo não travar.
Por que YOLO?
Nos primeiros testes, os métodos clássicos do OpenCV (sem redes neurais) erravam muito por causa de sombras, variações de iluminação e do ângulo oblíquo da câmera lateral. Por isso o grupo passou a usar o YOLO, que é bem mais preciso.

🛠️ Tecnologias
Tecnologia	Uso
Python 3.11	Linguagem principal
Ultralytics YOLOv8	Detecção de objetos
OpenCV (opencv-python)	Captura de vídeo e interface
NumPy	Gradientes e manipulação de imagens
winsound / threading	Alerta sonoro assíncrono
▶️ Como executar
⚠️ O alerta sonoro usa winsound, que só existe no Windows.

# 1. Clone o repositório
git clone https://github.com/<seu-usuario>/<nome-do-repo>.git
cd <nome-do-repo>

# 2. (Opcional) Crie um ambiente virtual
python -m venv venv
venv\Scripts\activate

# 3. Instale as dependências
pip install ultralytics opencv-python numpy

# 4. Execute
python EstacionamentoSeguro.py
Na primeira execução, a Ultralytics baixa automaticamente o arquivo yolov8n.pt.

Configuração
No código, ajuste conforme o seu ambiente:

Variável	Padrão	Descrição
cv2.VideoCapture(1)	1	Índice da câmera (use 0 para a webcam padrão ou o caminho de um vídeo)
total_vagas	8	Quantidade de vagas na área monitorada
CROP_AREA	(300, 70, 950, 600)	Recorte (x1, y1, x2, y2) da região do estacionamento
📸 Capturas de tela
🚀 Melhorias futuras
Mapear cada vaga individualmente (ROIs) e usar IoU para saber exatamente qual vaga está ocupada.
Trocar o winsound por uma biblioteca multiplataforma (ex.: playsound ou simpleaudio).
Ler as configurações (câmera, vagas, recorte) de um arquivo config.json.
Treinar o modelo com imagens do próprio estacionamento para ganhar precisão.
👥 Equipe
Victor Hugo Nascimento dos Santos
Victor Martins Carneiro Mourão
Diogo Gonçalves Siscati
Guilherme Enz Oliveira
Murilo Gonçalves
Orientação: Prof. Dr. Kleython José Coriolano Cavalcanti de Lacerda
