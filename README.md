
# Cliente VC

## Novidades!

- Lançamento do cliente Text To Speech, um software irmão.
  - Você pode se divertir gerando voz com um simples IF.
  - Veja mais detalhes [aqui](https://github.com/w-okada/ttsclient).
- Código de treinamento do **Beatrice V2** liberado!
  - [Repositório de código de treinamento](https://huggingface.co/fierce-cats/beatrice-trainer)
  - [Versão no Colab](https://github.com/w-okada/beatrice-trainer-colab)
- **v.2.0.65-beta**
  - [Veja mais aqui](https://github.com/w-okada/voice-changer/tree/v.2)
  - Nova funcionalidade: Suporte para o Beatrice v2 beta.1, possibilitando uma conversão de voz ainda mais avançada.
- **v.2.0.61-alpha**
  - [Veja mais aqui](https://github.com/w-okada/voice-changer/tree/v.2)
  - Funcionalidade:
    - Agora é possível definir o tempo de transição (crossfade).
  - Correções:
    - Modelos que não são usados em mesclagem agora têm seus elementos zerados e funcionam corretamente.
- **v.2.0.60-alpha**
  - [Veja mais aqui](https://github.com/w-okada/voice-changer/tree/v.2)
  - Funcionalidade:
    - [Modo escuro](https://github.com/w-okada/voice-changer/issues/1306)
    - [Reintrodução do PyTorch RMVPE](https://github.com/w-okada/voice-changer/issues/1319)
    - [Seleção de modo exclusivo WASAPI](https://github.com/w-okada/voice-changer/issues/1305)
- **v.2.0.58-alpha**
  - [Veja mais aqui](https://github.com/w-okada/voice-changer/tree/v.2)
  - Funcionalidade:
    - Transmissão via SIO
    - ngrok integrado (experimental)
  - Melhorias:
    - Ajustes para melhor uso em dispositivos móveis.
  - Correções:
    - Problema com codificação de mensagens CUI no macOS.
- **v.2.0.55-alpha**
  - [Veja mais aqui](https://github.com/w-okada/voice-changer/tree/v.2)
  - Melhorias:
    - Redução do uso de CPU no RVC.
    - Suporte para WebSocket.
  - Alterações:
    - Ativação da opção `no_cui` no script de inicialização.

## O que é o VC Client?

1. O **VC Client** é um software cliente para conversão de voz em tempo real usando diversas IAs de conversão de voz (VC - Voice Conversion). Ele suporta as seguintes IAs de conversão:

   - **AI de conversão de voz suportadas (VCs)**:
     - [MMVC](https://github.com/isletennos/MMVC_Trainer) (somente v1)
     - [so-vits-svc](https://github.com/svc-develop-team/so-vits-svc) (somente v1)
     - [RVC (Retrieval-based-Voice-Conversion)](https://github.com/liujing04/Retrieval-based-Voice-Conversion-WebUI)
     - [DDSP-SVC](https://github.com/yxlllc/DDSP-SVC) (somente v1)
     - [Beatrice JVS Corpus Edition](https://prj-beatrice.com/) *experimental, (***NÃO LICENÇA MIT***) veja [readme](https://github.com/w-okada/voice-changer/blob/master/server/voice_changer/Beatrice/) * Apenas para Windows, dependente de CPU (somente para v1)
     - [Beatrice v2](https://prj-beatrice.com/) (somente para v2)
   
2. Este software pode ser utilizado através de rede, permitindo que o processamento de conversão de voz seja offloadado para outro dispositivo, ideal para uso com aplicações de alta demanda como jogos.

3. Suporta múltiplas plataformas:

   - Windows, Mac (M1), Linux, Google Colab

## Softwares Relacionados

- [VCClient - Conversor de Voz em Tempo Real](https://github.com/w-okada/voice-changer)
- [TTSClient - Leitura em Voz Alta](https://github.com/w-okada/ttsclient)
- [ASRClient - Reconhecimento de Voz em Tempo Real](https://github.com/w-okada/asrclient)

## Como Usar

Há duas formas principais de usar este software, em ordem de dificuldade:

1. Utilizando os binários pré-construídos.
2. Configurando o ambiente via Docker ou Anaconda.

Se você for iniciante com o MMVC ou este software, é recomendado começar pela opção mais simples e ir se familiarizando aos poucos.

### (1) Utilizando os Binários Pré-construídos

- Consulte o [tutorial](tutorials/tutorial_rvc_ja_latest.md). Veja também a [solução de problemas de rede](https://github.com/w-okada/voice-changer/blob/master/tutorials/trouble_shoot_communication_ja.md).

- Agora você pode testar facilmente no [Google Colaboratory](https://github.com/w-okada/voice-changer/tree/v.2/w_okada's_Voice_Changer_version_2_x.ipynb). Clique em **Open in Colab** no canto superior esquerdo.

  ![Imagem](https://github.com/w-okada/voice-changer/assets/48346627/3f092e2d-6834-42f6-bbfd-7d389111604e)

- As versões para Windows e Mac estão disponíveis para download no [Hugging Face](https://huggingface.co/wok000/vcclient000/tree/main).
  
  - **v2 para Windows**:
    - Baixe o `vcclient_win_std_xxx.zip`. Isso permitirá a conversão de voz sem usar a GPU, usando um processador relativamente potente ou a GPU através do DirectML.
    - Para quem possui uma GPU Nvidia, use o `vcclient_win_cuda_xxx.zip` para uma conversão de voz mais rápida.
  
  - **v2 para Mac (Apple Silicon)**:
    - Baixe o `vcclient_mac_xxx.zip`.

  - **v1**:
    - Para Windows com GPU Nvidia, baixe o ONNX (cpu, cuda) ou PyTorch (cpu, cuda).
    - Para AMD/Intel, baixe o ONNX (cpu, DirectML) ou PyTorch (cpu, cuda).
    - Para quem não usará GPU, também pode baixar o ONNX (cpu, cuda) ou PyTorch (cpu, cuda).

- No Windows, extraia o arquivo ZIP baixado e execute o `start_http.bat`.

- No Mac, extraia o arquivo e execute `startHttp.command`. Caso o sistema bloqueie, clique com o botão direito ou use a tecla de controle para clicar e executar.

- Na primeira execução, alguns dados serão baixados, o que pode demorar. Após o download, o navegador será aberto automaticamente.

- Para acesso remoto, use os arquivos `.bat` (Windows) ou `.command` (Mac) substituindo `http` por `https`.

- **Nota**: DDSP-SVC suporta apenas o encoder hubert-soft.

- Faça o download [aqui no Hugging Face](https://huggingface.co/wok000/vcclient000/tree/main).

### (2) Usando Docker ou Anaconda

Clonando o repositório e configurando o ambiente:

- No Windows, é obrigatório configurar o WSL2, além de Docker ou Anaconda.
- No Mac, é necessário configurar o Anaconda ou outro ambiente virtual Python.

Esse método oferece a melhor performance em várias plataformas, mesmo sem uma GPU, desde que seu processador seja relativamente moderno. Veja os vídeos de instalação do [WSL2 e Docker](https://youtu.be/POo_Cg0eFMU) e do [WSL2 e Anaconda](https://youtu.be/fba9Zhsukqw).

Para executar via Docker, consulte [Docker README](docker_vcclient/README.md). Para Anaconda, veja a [página do desenvolvedor](README_dev_ja.md).

## Solução de Problemas

- [Problemas de comunicação](tutorials/trouble_shoot_communication_ja.md)

## Assinatura do Desenvolvedor

Este software não é assinado digitalmente pelo desenvolvedor. No macOS, será exibido um aviso de segurança, mas você pode ignorá-lo clicando com a tecla de controle pressionada e selecionando “Abrir”.


