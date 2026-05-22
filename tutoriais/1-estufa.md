# SISTEMA IoT COM NODE-RED + MQTT + DASHBOARD

## O que vamos construir

Você vai montar um sistema capaz de:

* receber temperatura e umidade (simulado ou ESP32);
* exibir dados em tempo real em um painel visual;
* enviar comandos para um dispositivo (como um ventilador);
* testar tudo sem precisar de hardware inicialmente.

---

<details>
<summary><h2>Preparando o ambiente</h2></summary>

### Subindo o MQTT (Broker)

O MQTT precisa de um servidor (broker). Vamos usar o Mosquitto.

#### Execute:

```powershell id="mosq1"
docker run -it -p 1883:1883 --name mosquitto eclipse-mosquitto
```

Deixe esse terminal aberto.

#### O que é MQTT e para que serve

O MQTT é um protocolo de comunicação leve usado em IoT.

Ele funciona assim:

* um dispositivo envia dados (publica);
* outro recebe esses dados (assina / subscribe).

Exemplo:

* ESP32 envia temperatura → “30°C”
* Node-RED recebe e mostra no painel

Ele é muito usado porque:

* é rápido
* usa pouca internet
* funciona bem em sensores e dispositivos pequenos

---

### Subindo o Node-RED

Em outro terminal:

```powershell id="nodered1"
docker run -it -p 1880:1880 --name mynodered nodered/node-red
```

Acesse:

[http://localhost:1880](http://localhost:1880)

---

### Instalando o Dashboard (UI)

Entre no container:

```powershell id="ui1"
docker exec -it mynodered bash
```

Vá para a pasta de dados:

```bash id="ui2"
cd /data
```

Instale o dashboard:

```bash id="ui3"
npm install node-red-dashboard
```

Saia:

```bash id="ui4"
exit
```

Reinicie o Node-RED:

```powershell id="ui5"
docker restart mynodered
```

#### O que é o Dashboard (UI)

O Dashboard é a interface visual do Node-RED.

Ele permite criar telas como:

* medidores (temperatura, umidade)
* gráficos
* botões
* indicadores

É o que transforma dados em algo visual.

</details>

---

## 1. Configurando o MQTT no Node-RED

Agora vamos conectar o Node-RED ao MQTT.

No Node-RED, arraste:

* mqtt in
* mqtt out

---

### 2. configurar servidor MQTT

Abra o nó MQTT e configure:

* Server: host.docker.internal
* Port: 1883

Clique em Done.

<img width="1409" height="565" alt="image" src="https://github.com/user-attachments/assets/ead7ffdd-1b3a-40cb-bf8b-36d990fedfd9" />

---

### 3. Criando o sistema de temperatura

#### Passo 1

Arraste:

* mqtt in
* gauge

Conecte:

<img width="371" height="97" alt="image" src="https://github.com/user-attachments/assets/fe832e8e-8370-47da-b576-0ccd235c340e" />

---

#### Passo 2

Configure o mqtt in:

Topic:

estufa/temperatura

---

#### Passo 3

Configure o gauge:

* Adicione e configure um Grupo
* Label: Temperatura
* Units: °C
* Min: 0
* Max: 50

<img width="1042" height="705" alt="image" src="https://github.com/user-attachments/assets/3ae02f19-2ca7-4dfc-b9dc-105a3bdad1b4" />

<img width="1039" height="449" alt="image" src="https://github.com/user-attachments/assets/a14c55ff-1a1b-4e2b-8804-9fdbf43dccfc" />


---

### 4. Criando o sistema de umidade

Repita o mesmo processo:

mqtt in → gauge

<img width="449" height="171" alt="image" src="https://github.com/user-attachments/assets/995a29c1-e9f1-406a-9136-92b9e6b477b7" />

mqtt in:

<img width="848" height="425" alt="image" src="https://github.com/user-attachments/assets/cfa6eadc-5a10-45a8-9942-3737a41681b2" />


gauge:

<img width="515" height="707" alt="image" src="https://github.com/user-attachments/assets/57ac7bf3-a56e-4dbb-9b4e-57a80f80c846" />


---

### 5. Criando controle do ventilador

#### Passo 1

Adicione:

* switch
* mqtt out

Conecte:

<img width="335" height="83" alt="image" src="https://github.com/user-attachments/assets/41791ad9-80fe-4109-9344-40bf8e6e79a1" />

---

#### Passo 2

Configure switch:

<img width="508" height="681" alt="image" src="https://github.com/user-attachments/assets/898891fc-7707-457f-b3b6-45b414e4c452" />

---

#### Passo 3

Configure mqtt out:

<img width="511" height="436" alt="image" src="https://github.com/user-attachments/assets/c3f2c20c-f31a-497d-8e05-5e66a5cbe909" />

---

### 5. Criando dashboard

Depois de montar tudo:

Clique em:

DEPLOY (ou Implementar)

---

Acesse:

[http://localhost:1880/ui](http://localhost:1880/ui)

---

### 6. Testando sem ESP32

Você pode simular dados.

#### Exemplo temperatura:

Inject → mqtt out

<img width="436" height="95" alt="image" src="https://github.com/user-attachments/assets/9496bb8f-daa6-414d-a606-005bfb5eab7a" />


Inject

<img width="582" height="353" alt="image" src="https://github.com/user-attachments/assets/8c4be2bb-ce2c-461c-908a-cdd9a7d12908" />


MQTT out

<img width="518" height="419" alt="image" src="https://github.com/user-attachments/assets/28ae1251-4bb4-40dc-bbfe-b3d613a3656b" />


---

#### Exemplo umidade:

Inject → mqtt out

<img width="393" height="76" alt="image" src="https://github.com/user-attachments/assets/162a8945-e70d-41b5-879c-d8bdfab2c18f" />


Inject

<img width="580" height="359" alt="image" src="https://github.com/user-attachments/assets/8b857f16-17dd-4e8b-842e-e522fddd6c77" />


Topic:

<img width="519" height="453" alt="image" src="https://github.com/user-attachments/assets/40cc1394-e5de-4015-9c12-3c43d37e0cd4" />

---

### 7. Sistema funcionando

Se tudo estiver correto, você terá:

* temperatura em tempo real
* umidade em tempo real
* gráfico de dados
* botão de ventilador

<img width="1897" height="612" alt="image" src="https://github.com/user-attachments/assets/05f03068-38b1-44e6-9274-a520fee5a907" />


---

### Problemas comuns

#### MQTT não conecta

Verifique:

* broker rodando
* porta 1883 aberta
* server = host.docker.internal

---

#### Dashboard não aparece

Verifique:

* se instalou node-red-dashboard
* se clicou Deploy

---

#### Dados não chegam

Verifique:

* tópicos iguais no MQTT
* conexão dos nós

---
