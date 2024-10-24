
# Cliente de Conversão de Voz em Tempo Real para RVC Tutorial (v.1.5.3.13)

[Japanese/日本語](/tutorials/tutorial_rvc_ja_latest.md) [Korean/한국어](/tutorials/tutorial_rvc_ko_latest.md)

## Introdução

Este aplicativo é um software cliente para conversão de voz em tempo real que suporta vários modelos de conversão de voz. Ele suporta modelos como RVC, MMVCv13, MMVCv15, So-vits-svcv40, entre outros. No entanto, este documento foca na [RVC (Retrieval-based-Voice-Conversion)](https://github.com/liujing04/Retrieval-based-Voice-Conversion-WebUI) para conversão de voz como material de tutorial. As operações básicas para cada modelo são essencialmente as mesmas.

A partir daqui, a [Retrieval-based-Voice-Conversion-WebUI](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI) original será chamada de "original-RVC", e a [RVC-WebUI](https://github.com/ddPn08/rvc-webui) criada por ddPn08 será chamada de "ddPn08-RVC".

## Observações

- O treinamento de modelos deve ser feito separadamente.
  - Se você quiser aprender por conta própria, consulte [original-RVC](https://github.com/liujing04/Retrieval-based-Voice-Conversion-WebUI) ou [ddPn08RVC](https://github.com/ddPn08/rvc-webui).
  - O [App de Gravação no Github Pages](https://w-okada.github.io/voice-changer/) é conveniente para preparar a voz para aprendizado no navegador.
    - [Vídeo Explicativo](https://youtu.be/s_GirFEGvaA)
  - Consulte [Dicas para Treinamento](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/blob/main/docs/training_tips_en.md) para mais detalhes.

## Passos até a Inicialização

### Versão para Windows

Descompacte o arquivo ZIP baixado e execute `start_http.bat`.

Se você tiver uma versão antiga, certifique-se de descompactá-la em uma pasta separada.

### Versão para Mac

O procedimento é o seguinte:

1. Descompacte o arquivo baixado.
2. Em seguida, execute o **MMVCServerSIO** mantendo pressionada a tecla de controle e clicando nele (ou clique com o botão direito para executar). Se aparecer uma mensagem dizendo que o desenvolvedor não pode ser verificado, execute-o novamente pressionando a tecla de controle e clicando nele (ou clique com o botão direito para executar). O terminal será aberto e o processo terminará em alguns segundos.
3. Execute o arquivo **startHTTP.command** mantendo pressionada a tecla de controle e clicando nele (ou clique com o botão direito para executar). Se aparecer uma mensagem dizendo que o desenvolvedor não pode ser verificado, repita o processo. Um terminal será aberto, iniciando o processo de inicialização.

- **Nota**: O importante é executar o **MMVCServerSIO** primeiro e depois o **startHTTP.command**.

Se você tiver uma versão antiga, certifique-se de descompactá-la em uma pasta separada.

### Precauções ao Conectar-se Remotamente

Ao se conectar remotamente, use o arquivo `.bat` (Windows) ou `.command` (Mac), onde o HTTP foi substituído por HTTPS.

Acesse com um navegador (atualmente, apenas o Chrome é suportado) e você verá a interface gráfica.

### Console

Ao executar o arquivo `.bat` (Windows) ou `.command` (Mac), uma tela como a seguinte será exibida, e vários dados serão baixados da Internet na inicialização. Dependendo do ambiente, isso pode levar de 1 a 2 minutos.

![image](https://github.com/w-okada/voice-changer/assets/48346627/88a30097-2fb3-4c50-8bf1-19c41f27c481)

### Interface Gráfica (GUI)

Após o download dos dados necessários, uma tela como a abaixo será exibida. Se desejar, pressione o ícone amarelo para recompensar o desenvolvedor com uma xícara de café. Pressionar o botão "Start" fará com que o diálogo desapareça.

![image](https://github.com/w-okada/voice-changer/assets/48346627/a8d12b5c-d1e8-4ca6-aed0-72cee6bb97c1)

## Visão Geral da Interface Gráfica

Use esta tela para operar o software.

![image](https://github.com/w-okada/voice-changer/assets/48346627/27add00d-5059-4cbf-a732-9deb6dc309ff)

## Início Rápido

Você pode realizar a conversão de voz imediatamente usando os dados baixados na inicialização.

### Operação

1. Para começar, clique na área de seleção de modelos para escolher o modelo que deseja usar. Após o carregamento, as imagens dos personagens serão exibidas na tela.
2. Selecione o microfone (entrada) e o alto-falante (saída) que deseja usar. Recomendamos que escolha o cliente e depois selecione seu microfone e alto-falante. (Explicaremos a diferença entre servidor mais tarde).
3. Quando você pressionar o botão "Start", a conversão de áudio começará após alguns segundos de carregamento. Fale algo no microfone, e você deverá ouvir o áudio convertido no alto-falante.

![image](https://github.com/w-okada/voice-changer/assets/48346627/883b296e-e5ca-4571-8fed-dcf7495ebb92)

### Perguntas Frequentes sobre o Início Rápido

**P1. O áudio está cortando ou gaguejando.**

R1. É possível que o desempenho do seu PC não seja suficiente. Tente aumentar o valor do CHUNK (como mostrado na figura com a letra A, por exemplo, para 1024). Também tente configurar o F0 Det para "dio" (como mostrado na figura com a letra B).

![image](https://github.com/w-okada/voice-changer/assets/48346627/3c485d9b-53be-47c1-85d9-8663363b06f9)

**P2. A voz não está sendo convertida.**

R2. Consulte [este link](https://github.com/w-okada/voice-changer/blob/master/tutorials/trouble_shoot_communication_ja.md) para identificar o problema e buscar uma solução.

**P3. O tom está fora do esperado.**

R3. Embora não explicado no Início Rápido, se o modelo for compatível com ajuste de tom, você pode alterá-lo com o controle "TUNE". Consulte a explicação detalhada abaixo.

**P4. A janela não aparece ou aparece mas sem conteúdo, e um erro de console como `electron: Failed to load URL: http://localhost:18888/ with error: ERR_CONNECTION_REFUSED` é exibido.**

R4. Pode ser que o antivírus esteja interferindo. Aguarde ou defina a pasta como uma exceção no antivírus (por sua própria conta e risco).

**P5. O erro `[4716:0429/213736.103:ERROR:gpu_init.cc(523)] Passthrough is not supported, GL is disabled, ANGLE is` está aparecendo.**

R5. Este é um erro da biblioteca usada pelo aplicativo, mas não afeta o funcionamento, então ignore.

**P6. Minha GPU AMD não está sendo usada.**

R6. Use a versão DirectML. GPUs AMD só são compatíveis com modelos ONNX. Verifique o aumento no uso da GPU no Monitor de Desempenho.

**P7. O onxxruntime não está iniciando e exibe um erro.**

R7. Um erro pode ocorrer se o caminho da pasta contiver caracteres Unicode. Extraia o arquivo para um local que contenha apenas caracteres alfanuméricos.
