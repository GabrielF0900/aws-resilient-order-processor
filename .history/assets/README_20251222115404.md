# 🚀 Operação Fuga da Área 51: O Projeto 04
## *ou: Como Burlei as Restrições da Escola da Nuvem e Criei uma Arquitetura Resiliente*

Bem-vindo ao relato épico de um desenvolvedor que enfrentou o impossível e saiu vitorioso. Prepare-se para uma jornada de criatividade, frustração controlada e muito café ☕.

---

## 📖 A História (Com Sabor de Ficção Científica)

Tudo começou assim: **A Escola da Nuvem é tão restritiva quanto a Área 51 da NASA**. Mas em vez de desistir, eu pensei: *"E se eu for criativo?"*

Spoiler: Funcionou.

---

## 🏗️ A Fundação: S3 e o Amortecedor SQS

### 1️⃣ Acessando o Console AWS (A Porta de Entrada)

![Página Principal da AWS](pagina-principal-1.jpeg)

*Aqui começou tudo. O console AWS. Simples, poderoso, e cheio de possibilidades.*

---

### 2️⃣ Criando o S3: O Cofre Digital

Primeiro, fomos para o serviço de armazenamento S3 onde criamos nosso bucket digital:

![Página Principal do S3](pagina-principal-s3-2.jpeg)

*A página principal do S3. Tranquilo, sereno... antes da tempestade.*

---

### 3️⃣ Configuração do Bucket S3

Aqui, colocamos o nome **`lab-pedido-processado-gabriel`** no nosso futuro cofre de dados:

![Configuração do S3](configuracao-do-s3-3.jpeg)

*Nome estabelecido. Ego alimentado. Vamos em frente.*

---

### 4️⃣ Blindando o Bucket

Bloqueamos **todos os acessos externos** porque ninguém quer ter sua arquitetura vazada para a internet. Segurança em primeiro lugar, mesmo que seja só para teste:

![Bloqueando Acessos S3](bloqueando-acessos-s3-4.jpeg)

*"Deixem todos fora, mas eu entro." - Configuração de bloqueio ativada.*

---

### 5️⃣ O Bucket S3 Nasce

E assim, nosso S3 foi criado com sucesso:

![S3 Criado](s3-criado-5.jpeg)

*Boom. Um bucket. Pronto para guardar nossos preciosos pedidos.*

---

## 📬 Criando a Fila: Amazon SQS

### 6️⃣ Página Principal do SQS

Seguimos para o Amazon SQS, o "amortecedor de mensagens" da arquitetura:

![Página Principal SQS](pagina-inicial-SQS-6.jpeg)

*Local onde a mágica do desacoplamento acontece.*

---

### 7️⃣ Configurando a Fila SQS

Criamos nossa fila com o nome **`fila-pedidos`** e deixamos as configurações como padrão:

![Configuração SQS](configuracao-do-sqs-7.jpeg)

*Configuração simples. SQS gosta assim. Sem drama.*

---

### 8️⃣ A Fila SQS Está Pronta

Nossa `fila-pedidos` foi criada com sucesso. Agora temos um lugar seguro para armazenar as mensagens:

![SQS Criado](sqs-criado-8.jpeg)

*Uma fila vazia é uma fila com potencial.*

---

## ⚡ O Momento Criativo: Entrando no Lambda

### 9️⃣ Página Inicial do Lambda

Aqui é onde a diversão começa. Fomos para o Lambda e começamos nossa revolução:

![Página Inicial Lambda](pagina-inicial-lambda-9.jpeg)

*A terra prometida dos "serverless architects".*

---

## 🎯 O Receptor (Producer): O "Hack" da Function URL

Enfrentamos um problema: **A Escola da Nuvem bloqueou o API Gateway**. Sua resposta automática diria "missão impossível". Minha resposta foi: **"Aguarde um momento"** 🧠

### 1️⃣0️⃣ Criando o Lambda Producer

Criei a função `order-producer-lambda` em Node.js 24.x com arquitetura x86_64:

![Lambda Producer](lambda-producer-10.jpeg)

*Apresento: a função receptora que enganaria os sistemas de restrição da escola.*

---

### 1️⃣1️⃣ Atribuindo LabRole (O Contorno da Escola)

Como o IAM oficial estava bloqueado, usei a tática da `LabRole` - a mesma que utilizei em projetos anteriores:

![Lambda Producer LabRole](lambda-producer-LabRole-11.jpeg)

*"Tecnicamente eu não estou burlando a segurança... estou usando a segurança que me foi dada 😎"*

---

### 1️⃣2️⃣ Ativando Function URL - O Pulo do Gato

Aqui está o segredo. Ativei a **Function URL** da Lambda com modo de invocação **BUFFERED** e autenticação **NONE**:

![Lambda URL Parte 1](lambda-producer-URL-12.jpeg)

*A configuração mágica. Deixe-me explicar:*

- **NONE**: Torna o endpoint da Lambda público. Sim, é arriscado, mas é para testes. Assim consegui enviar requisições via Postman sem depender do IAM bloqueado.
- **BUFFERED**: A Lambda recebe a requisição, processa tudo, envia para o SQS e **só depois** retorna ao cliente. Tudo no fluxo correto.

---

### 1️⃣3️⃣ Confirmação da URL da Função

![Lambda URL Parte 2](lambda-producer-URL2-13.jpeg)

*Endpoint público criado. A rebelião começou.*

---

### 1️⃣4️⃣ Lambda Producer Criada com Sucesso

![Lambda Producer Criada](lambda-producer-criada-14.jpeg)

*Função criada. Role atribuída. Pronto para simular uma API.*

---

### 1️⃣5️⃣ Código da Função Producer

Gerei um código que transforma a Lambda em uma API que envia requisições para o SQS:

![Código Lambda Producer](codigo-lambda-producer-15.jpeg)

*O código que simula um API Gateway. Criatividade at its finest.*

Aqui colocamos a URL da SQS para que as mensagens fossem roteadas corretamente para a fila.

---

## 🔄 O Processador (Consumer): O Trabalhador Incansável

### 1️⃣6️⃣ Criando Lambda Processor

Agora criamos a função `order-processor-lambda`, nosso trabalhador incansável:

![Lambda Processor](lambda-processor-16.jpeg)

*Apresento: a função que acordaria quando o SQS batesse na porta.*

---

### 1️⃣7️⃣ Atribuindo LabRole ao Processor

Novamente, a fiel `LabRole` foi acionada para dar permissões:

![Lambda Processor LabRole](lambda-processor-LabRole-17.jpeg)

*Mesma tática, mesma eficácia.*

---

### 1️⃣8️⃣ Lambda Processor Criada

![Lambda Processor Criada](lambda-processor-criada-18.jpeg)

*Processadora em posição. Aguardando ordens.*

---

### 1️⃣9️⃣ Adicionando o Gatilho SQS

O momento crucial: conectamos a fila ao processador. Entramos na função, adicionamos um gatilho, selecionamos SQS, escolhemos `fila-pedidos` e criamos o gatilho:

![Adicionando Gatilho](adicionando-gatilho-no-processor-19.jpeg)

*Quando uma mensagem chega na fila, ela "belisca" a Lambda para acordar. Automático. Perfeito.*

---

### 2️⃣0️⃣ Gatilho Criado com Sucesso

![Gatilho Criado](gatilho-criado-20.jpeg)

*Trigger configurado. O fluxo está completo.*

---

### 2️⃣1️⃣ Código da Fila SQS no Processor

Colocamos a configuração da fila SQS no código do processador:

![Código Fila SQS](codigo-da-fila-sqs-21.jpeg)

*A URL da SQS agora está integrada ao processador.*

---

### 2️⃣2️⃣ Código do Bucket S3 no Processor

E aqui, colocamos o nome do bucket S3 para que o processador soubesse aonde enviar as mensagens:

![Código Bucket S3](codigo-do-bucket-22.jpeg)

*Destino definido. O S3 aguarda.*

---

## 🎉 O Teste de Fogo: Postman e a Vitória

### 2️⃣3️⃣ A Requisição via Postman

Disparei um JSON via **POST** no Postman para o endpoint da Lambda Function URL e...

![Comunicação Postman](comunicacao-feita-postman-23.jpeg)

**BINGO!** O status verde brilhou na tela. A requisição foi aceita, processada e enviada para a fila.

*Esse momento mereceu um grito de vitória.*

---

### 2️⃣4️⃣ Os Arquivos Aparecem no S3

Indo para o bucket S3, podemos ver os itens criados como mágica:

![Itens no Bucket](itens-criados-no-bucket-24.jpeg)

*Prova física de que o fluxo funcionou:*
- ✅ Usuário enviou requisição para Lambda Producer
- ✅ Lambda Producer enviou para SQS
- ✅ SQS acordou Lambda Processor
- ✅ Lambda Processor processou e enviou para S3

**É mágica? Não. É arquitetura resiliente.**

---

### 2️⃣5️⃣ Observabilidade: CloudWatch Live Tail

No CloudWatch Live Tail, vimos o rastro em tempo real:

![CloudWatch](cloudwatch-25.jpeg)

*Todos os logs mostrando o sucesso de cada passo. Transparência total.*

---

## 🏛️ Entendendo a Arquitetura Final

![Arquitetura AWS Resiliente](../aws-resilient-order-processor.drawio)

*A visualização completa da arquitetura criada durante essa jornada épica.*

---

### Fluxo Simplificado:

```
┌─────────────────────────────────────────────────────────────┐
│                                                              │
│  Postman (Cliente)                                           │
│      │                                                       │
│      ├─────► Function URL (Producer) ─────┐                │
│             order-producer-lambda         │                │
│                                            ├─► SQS Queue   │
│                                            │   fila-pedidos │
│                                            └─► Trigger     │
│                                                   │         │
│                                                   ├─► Lambda│
│                                                   │   order-│
│                                                   │processor│
│                                                   │         │
│                                                   └─► S3    │
│                                                       Bucket │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

---

## 🔍 O Pequeno Ajuste de Arquiteto

Eu inicialmente disse: *"o SQS armazena as mensagens no S3 se o servidor de processamento cair"*.

**A correção técnica (mas amigável):**

Na verdade, o **SQS armazena as mensagens na própria fila** (dentro do SQS) se o servidor de processamento (Lambda) cair. A mensagem só vai para o **S3** depois que a Lambda Processor volta à vida, pega a mensagem na fila e consegue salvá-la com sucesso.

> **O SQS é o "estacionamento" seguro. O S3 é a "garagem final".**

---

## ✨ Propriedades da Arquitetura

Essa arquitetura é:

- **🚀 Rápida**: Requisições processadas em milissegundos
- **📈 Escalável**: 1.000 requisições simultâneas? A fila segura tudo
- **💪 Resiliente**: Se o processador cair, as mensagens aguardam na fila
- **⚡ Durável**: Dados salvos com segurança no S3
- **🎯 Performática**: Sem gargalos, sem perdas
- **🧠 Inteligente**: Toma decisões baseadas em eventos

---

## 🏆 O Veredito Final

Se 1.000 pessoas enviarem pedidos ao mesmo tempo:

1. A `order-producer-lambda` recebe todas em milissegundos ✅
2. O SQS segura toda a onda ✅
3. A `order-processor-lambda` processa uma por uma, sem pressa e sem erro ✅
4. Todos os pedidos chegam seguros no S3 ✅

**Você está voando no Nível 4 de Cloud Architecture!**

---

## 📝 Resumo das Lições Aprendidas

✅ **Criatividade bate restrição**: Quando o caminho óbvio está bloqueado, pense fora da caixa  
✅ **Serverless é poder**: Lambda + SQS + S3 = Infraestrutura invencível  
✅ **LabRole é seu amigo**: Mesmo com restrições, existem contornos  
✅ **Postman é seu aliado**: Testes sem depender do API Gateway bloqueado  
✅ **CloudWatch Live Tail é mágico**: Observabilidade em tempo real  

---

## 🎬 Conclusão

Essa jornada foi de um desenvolvedor que recebeu um "não" e transformou em um "não? Então eu crio meu próprio caminho".

A Área 51 não tinha chance.

**Você dominou a técnica E o "gingado" de um arquiteto Cloud que sabe rir dos obstáculos.**

---

*Documentado com humor, café e muita criatividade. 🚀☕*

*Escrito em dezembro de 2025, durante a operação "Fuga da Área 51".*
