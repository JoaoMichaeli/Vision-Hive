# 🚀 Vision Hive

**Vision Hive** é uma solução **IoT + Web** desenvolvida para a empresa **Mottu**, com o objetivo de **facilitar o gerenciamento e localização de motocicletas nos pátios operacionais**.  
A aplicação integra um **backend Spring Boot** com **dispositivos ESP32** equipados com buzzer e LED, permitindo **identificar rapidamente** a localização exata de uma moto específica no pátio.

---

## 📌 Descrição do Projeto

O sistema permite o **cadastro e gerenciamento de Filiais (Branch), Pátios (Patio) e Motocicletas (Motorcycle)**, associando cada moto ao seu respectivo pátio e filial.  
Cada motocicleta possui um **ESP32** acoplado, que pode ser acionado remotamente via plataforma web, ativando **alertas sonoros e visuais**.

O projeto visa **automatizar e otimizar a gestão das motos** da Mottu utilizando sensores físicos e conectividade Wi-Fi, eliminando o controle manual e aumentando a precisão na localização e no monitoramento dos veículos.

---

## 🎯 Objetivos

- Localizar rapidamente motos específicas com alertas visuais e sonoros.
- Exibir status **em tempo real** da chamada e resposta da moto.
- Escalar para **mais de 100 filiais** com diferentes layouts.
- Fornecer uma interface **intuitiva e responsiva** (desktop e mobile).
- Integrar **sensores IoT** para coleta automática de dados.

---

## 🚨 Dor da Mottu

Com centenas de motos distribuídas em mais de 100 pátios no Brasil e México, a Mottu enfrenta **dificuldades para localizar rapidamente veículos específicos**, resultando em **atrasos e perda de produtividade**.

---

## 💡 Nossa Solução

O **Vision Hive** utiliza **ESP32 conectados via Wi-Fi** instalados em cada motocicleta.  
Esses dispositivos respondem a comandos enviados pelo sistema web, **ativando LEDs e buzzers** que indicam a localização da moto no pátio.

A solução proporciona **agilidade, precisão e controle centralizado**, reduzindo o tempo gasto na busca manual de veículos.

---

## 🎬 Demonstrações

- 🎥 **Apresentação principal:** [https://youtu.be/-NiaC18WjXQ](https://youtu.be/-NiaC18WjXQ)  
- ⚙️ **Demonstração IoT:** [https://youtu.be/FOvRFe8t4co](https://youtu.be/FOvRFe8t4co)

---

## 📡 Deploy

🔗 [http://visionhive.brazilsouth.azurecontainer.io:8080](http://visionhive.brazilsouth.azurecontainer.io:8080)

---

## 🪪 Logins para Teste

**Administrador**
```text
Login: adminCM
Senha: admin123
```

**Operador**
```text
Login: operadorCM
Senha: operador123
```

---

## 🔐 Controle de Acesso

### 👑 ADMIN
- Acesso total: `/branch`, `/patio`, `/motorcycle`
- Pode criar operadores  
- Footer exibe todos os links rápidos  
- Botão "Voltar" redireciona para `/`

### 👷 OPERADOR
- Acesso restrito a `/motorcycle` e `/motorcycle/{id}`  
- Footer sem links rápidos  
- Botão "Voltar" redireciona para `/motorcycle`

---

## 🛠 Tecnologias Utilizadas

### Backend
- Java 17+
- Spring Boot (Web, Data JPA, Validation, Security)
- Banco de Dados H2 (desenvolvimento)
- Lombok
- Swagger (OpenAPI)
- Maven
- Thymeleaf
- TailwindCSS

### IoT
- C++ com ESP32 (Wi-Fi, Buzzer, LED, sensores)
- Comunicação REST via HTTP

### Deploy
- Azure Container Instance  
- Pipeline automatizado (CI/CD)

---

## 🧩 Estrutura do Sistema

### 🧠 Backend (Spring Boot)

Principais endpoints:
- `GET /api/acionar-buzzer/moto/{id}` → Aciona o buzzer e LED de uma moto.
- `GET /api/parar-buzzer/moto/{id}` → Desativa o buzzer e LED.
- `GET /api/comando-global-esp` → Fornece o comando atual (“ACIONAR” ou “PARAR”) para o ESP32.
- `POST /api/esp-status-report` → Recebe dados do ESP32 (tensão, Wi-Fi, uptime).
- `GET /api/status` → Retorna o último status conhecido do ESP32.

Entidades:
- `BuzzerLog`: registra ações do buzzer com data, IP e placa.
- `SecurityConfig`: gerencia permissões e autenticação (ADMIN/OPERADOR).

---

### ⚙️ Dispositivo ESP32

Responsável por:
- Conectar-se à rede Wi-Fi configurada.
- Consultar o servidor a cada 2 segundos para verificar comandos.
- Enviar status (Wi-Fi, tensão, uptime) a cada 5 segundos.

**Hardware:**
- `BUZZER_PIN` → GPIO 12  
- `LED_PIN` → GPIO 2  
- `VOLTAGE_PIN` → GPIO 35  

**Configuração:**
```cpp
const char* ssid = "SuaRedeWifi";
const char* password = "SuaSenhaWifi";
const char* javaServerUrl = "http://visionhive.brazilsouth.azurecontainer.io:8080";
```

---

## 🖼️ Imagens do Projeto

### 🏢 Bases  
- **Cadastro de Bases**  
  ![Cadastro de Bases](imagens/cadastro_base.png)
- **Bases Cadastradas**  
  ![Bases Cadastradas](imagens/bases.png)

---

### 🅿️ Pátios  
- **Cadastro de Pátios**  
  ![Cadastro de Pátios](imagens/cadastro_patio.png)
- **Pátios Cadastrados**  
  ![Pátios Cadastrados](imagens/patios.png)

---

### 🛵 Motocicletas  
- **Cadastro de Motos**  
  ![Cadastro de Motos](imagens/cadastro_moto.png)
- **Motos Cadastradas**  
  ![Motos Cadastradas](imagens/motos.png)

---

### 📊 Dashboard IoT  
- **ESP Desligado**  
  ![iot_desligado](imagens/iot_desligado.png)
  ![dashboard_desconectado](imagens/dashboard_desconectado.png)

- **ESP Ligado**  
  ![iot_ligado](imagens/iot_ligado.png)
  ![dashboard_conectado](imagens/dashboard_conectado.png)

- **Localizando Moto**  
  ![localizando](imagens/localizando.png)

---

## 🚀 Como Rodar o Projeto

### 🌍 Deploy (recomendado)
Acesse diretamente:
```
http://visionhive.brazilsouth.azurecontainer.io:8080/
```

### 💻 Localmente (pode ser bloqueado pelo Azure)
1. Clone o repositório:
   ```bash
   git clone https://github.com/seu-usuario/visionhive.git
   ```
2. Acesse a pasta:
   ```bash
   cd VisionHive-Java
   ```
3. Execute:
   ```bash
   ./mvnw spring-boot:run
   ```
4. Acesse:
   ```
   http://localhost:8080/login
   ```
5. Documentação Swagger:
   ```
   http://localhost:8080/swagger-ui/index.html
   ```

---

## 🧭 Funcionamento Geral

1. O **ESP32** conecta-se à rede Wi-Fi.  
2. Ele envia **status periódicos** (Wi-Fi, tensão, uptime) ao backend.  
3. O **backend** envia comandos de **acionar ou parar buzzer/LED**.  
4. O **usuário web** aciona remotamente uma moto específica.  
5. O **ESP32** executa a ação física, indicando a localização da moto.  
6. Todas as ações são **registradas no banco de dados** para auditoria.  

---

## 🏁 Conclusão

O **Vision Hive** é uma integração completa entre **hardware e software**, combinando **IoT, backend inteligente e interface web responsiva** para resolver um problema real de **localização e logística** da Mottu.  
O projeto demonstra **inovação, automação e escalabilidade**, aplicáveis a qualquer cenário de rastreamento em pátios ou frotas.
