# Erro ao atualizar ou instalar algo no Arduino IDE (to mexendo num Esp32)
## Failed to install platform: 'XXXX'. 4 DEADLINE_EXCEEDED: net/http: request canceled (Client.Timeout or context cancellation while reading body)
### ou algum erro equivalente

### se voce tiver no linux voce vai abrir:

## /home/<username>/.arduinoIDE/arduino-cli.yaml

### se voce tiver no windows voce vai abrir:

## C:\Users<username>.arduinoIDE\arduino-cli.yaml
                                              *se voce tiver no mac recomendo se matar *
## depois de abrir o yaml voce vai adicionar:

network:
    connection_timeout: 600s


pode alterar esse tempo mas eu recomendo jogar esses 600s msm que funciona
se no seu yaml ja tiver algum campo de network é só alterar e adicionar um timeout mais longo pq o erro é basicamente timeout mt curto