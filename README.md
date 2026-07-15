# Gerenciamento de Instâncias EC2 na AWS

## Sobre o projeto

Este repositório foi desenvolvido como parte de um desafio prático da DIO sobre gerenciamento de instâncias EC2 na AWS.

O objetivo do projeto é documentar os principais conhecimentos adquiridos durante a criação, configuração, acesso e gerenciamento de uma máquina virtual na nuvem utilizando o serviço Amazon EC2.

Durante a prática, foi criada uma instância com sistema operacional Ubuntu Server, configurado o acesso por chave SSH e realizado o acesso remoto ao servidor por meio do terminal.

---

## Objetivos do desafio

- Aplicar os conceitos de computação em nuvem em um ambiente prático;
- Criar e configurar uma instância EC2;
- Entender o funcionamento dos grupos de segurança;
- Realizar o acesso remoto utilizando SSH;
- Compreender o ciclo de vida de uma instância;
- Documentar o processo de forma clara;
- Utilizar o GitHub para compartilhar documentação técnica.

---

## O que é o Amazon EC2?

O Amazon EC2, ou Amazon Elastic Compute Cloud, é um serviço da AWS que permite criar e utilizar servidores virtuais na nuvem.

Esses servidores são chamados de instâncias e podem ser configurados com diferentes sistemas operacionais, quantidades de memória, capacidade de processamento e armazenamento.

Uma instância EC2 pode ser utilizada para hospedar aplicações, APIs, bancos de dados, sites, automações e diversos outros serviços.

---

## Configuração da instância

Durante o laboratório, foi criada uma instância EC2 com a seguinte configuração:

- **Provedor:** Amazon Web Services;
- **Serviço:** Amazon EC2;
- **Nome da instância:** `DevPrimacy`;
- **Sistema operacional:** Ubuntu Server;
- **Tipo de instância:** `t3.micro`;
- **Região:** Norte da Virgínia — `us-east-1`;
- **Zona de disponibilidade:** `us-east-1c`;
- **Estado atual:** Em execução;
- **Verificação de status:** 3 de 3 verificações aprovadas;
- **Nome do par de chaves:** `devforge-key`;
- **Grupo de segurança:** `launch-wizard-1`;
- **Monitoramento detalhado:** Desativado;
- **Forma de acesso:** SSH;
- **Porta de acesso:** 22;
- **Data de criação:** 31 de maio de 2026.

> Por motivos de segurança, o endereço IP público, o DNS público e o identificador completo da instância não foram informados neste repositório.

---

## Etapas realizadas

### 1. Acesso ao serviço EC2

Primeiramente, acessei o Console de Gerenciamento da AWS e selecionei o serviço Amazon EC2.

Dentro do painel, utilizei a opção **Executar instância** para iniciar o processo de criação do servidor virtual.

---

### 2. Definição do nome da instância

Foi definido o nome `DevPrimacy` para facilitar a identificação da máquina no painel da AWS.

Esse nome permite diferenciar a instância de outros recursos que possam ser criados futuramente dentro da conta.

---

### 3. Escolha do sistema operacional

Foi selecionada uma imagem Ubuntu Server como sistema operacional da instância.

A imagem utilizada pela AWS é chamada de AMI, ou Amazon Machine Image.

A AMI contém o sistema operacional e as configurações iniciais necessárias para criar a máquina virtual.

---

### 4. Escolha do tipo de instância

Foi selecionado o tipo de instância `t3.micro`.

Esse tipo de instância é adequado para ambientes de estudo, testes e aplicações leves que não exigem grande capacidade de processamento.

O tipo da instância define características como:

- quantidade de memória RAM;
- quantidade de CPUs virtuais;
- desempenho de rede;
- capacidade de processamento;
- custo de utilização.

---

### 5. Configuração do par de chaves

Para permitir o acesso seguro à instância, foi utilizado o par de chaves chamado `devforge-key`.

A chave privada foi disponibilizada no formato `.pem` e utilizada durante a conexão SSH.

Por motivos de segurança, o arquivo da chave privada não foi adicionado ao repositório.

---

### 6. Configuração do grupo de segurança

O grupo de segurança funciona como um firewall da instância.

Foi utilizada uma regra de entrada para permitir o acesso SSH:

| Tipo | Protocolo | Porta | Finalidade |
|---|---|---:|---|
| SSH | TCP | 22 | Acesso remoto ao servidor |

Como boa prática de segurança, o acesso SSH deve ser permitido apenas para endereços IP confiáveis sempre que possível.

---

### 7. Inicialização da instância

Após finalizar as configurações, a instância foi iniciada.

No painel do EC2, foi possível acompanhar seu estado:

```text
Pendente → Em execução
```

Quando a instância ficou com o estado **Em execução** e as verificações de status foram aprovadas, o servidor estava pronto para receber conexões.

---

## Configuração da chave SSH

Antes de realizar a conexão, foi necessário ajustar a permissão do arquivo da chave privada.

No Linux ou macOS, foi utilizado o seguinte comando:

```bash
chmod 400 devforge-key.pem
```

Esse comando restringe o acesso ao arquivo, permitindo que apenas o proprietário consiga utilizá-lo.

Essa etapa é importante porque o SSH pode recusar chaves privadas com permissões muito abertas.

---

## Acesso à instância por SSH

O acesso remoto à instância `DevPrimacy` foi realizado pelo terminal utilizando o protocolo SSH.

O comando utilizado seguiu esta estrutura:

```bash
ssh -i devforge-key.pem ubuntu@IP_PUBLICO
```

Nesse comando:

- `ssh` inicia uma conexão remota segura;
- `-i` indica qual arquivo de chave privada será utilizado;
- `devforge-key.pem` representa a chave associada à instância;
- `ubuntu` é o usuário padrão do Ubuntu Server;
- `IP_PUBLICO` representa o endereço público da instância.

O endereço IP real não foi publicado por motivos de segurança.

---

## Comandos executados no servidor

Após acessar a instância, alguns comandos podem ser utilizados para verificar e atualizar o ambiente.

### Atualização da lista de pacotes

```bash
sudo apt update
```

Esse comando atualiza a lista de pacotes disponíveis nos repositórios do Ubuntu.

### Atualização dos pacotes instalados

```bash
sudo apt upgrade -y
```

Esse comando atualiza os pacotes instalados na máquina.

### Verificação do sistema operacional

```bash
uname -a
```

Esse comando apresenta informações sobre o sistema e o kernel.

### Verificação da memória

```bash
free -h
```

Esse comando apresenta informações sobre a memória RAM utilizada e disponível.

### Verificação do armazenamento

```bash
df -h
```

Esse comando apresenta o espaço utilizado e disponível nos discos.

---

## Ciclo de vida de uma instância

Durante o laboratório, também foi possível compreender os principais estados de uma instância EC2.

### Iniciar

Liga uma instância que estava parada.

```text
Parada → Em execução
```

### Parar

Desliga a máquina virtual, mas mantém suas configurações e seu armazenamento.

Mesmo com a instância parada, alguns recursos, como volumes de armazenamento, ainda podem gerar custos.

### Reinicializar

Reinicia o sistema operacional da instância.

Essa operação é semelhante à reinicialização de um computador físico.

### Encerrar

Remove a instância.

```text
Em execução → Encerrada
```

É necessário ter cuidado, pois essa ação pode remover permanentemente a máquina e seus dados.

---

## Boas práticas de segurança

Durante a prática, foram identificadas algumas boas práticas importantes:

- não compartilhar o arquivo `.pem`;
- não publicar credenciais da AWS;
- não adicionar chaves privadas ao GitHub;
- limitar o acesso SSH ao próprio endereço IP;
- não liberar portas desnecessárias;
- utilizar autenticação multifator na conta AWS;
- revisar regularmente as regras dos grupos de segurança;
- utilizar apenas os recursos necessários;
- encerrar recursos que não serão mais utilizados.

---

## Cuidados com custos

Mesmo em ambientes de estudo, é importante acompanhar os recursos utilizados na AWS.

Alguns cuidados adotados ou recomendados são:

- utilizar instâncias de baixo custo;
- verificar se o recurso está coberto pela camada gratuita ou por créditos;
- parar ou encerrar instâncias que não estejam sendo utilizadas;
- acompanhar o painel de faturamento;
- configurar alertas e orçamentos;
- verificar volumes de armazenamento que continuam ativos;
- evitar deixar recursos executando sem necessidade.

Também foram configurados alertas de faturamento para acompanhar os gastos e reduzir o risco de cobranças inesperadas.

---

## Estrutura do repositório

```text
desafio-aws-ec2/
│
├── README.md
├── .gitignore
│
└── images/
    └── instancia-devprimacy-executando.png
```

A pasta `images` é opcional e pode ser utilizada para armazenar capturas de tela da prática.

---

## Evidências da prática

### Instância EC2 em execução

A imagem abaixo apresenta a instância `DevPrimacy` em execução no console da AWS.

```markdown
![Instância DevPrimacy em execução](images/instancia-devprimacy-executando.png)
```

Antes de publicar a imagem, é importante esconder informações sensíveis, como IP público, DNS público, identificador da instância e dados da conta AWS.

---

## Dificuldades encontradas

Durante a atividade, uma das principais etapas de atenção foi a configuração da chave privada utilizada no acesso SSH.

Foi necessário ajustar a permissão do arquivo `.pem` para que o SSH aceitasse a chave.

Também foi importante compreender que a porta 22 precisava estar liberada no grupo de segurança para permitir a conexão com a instância.

Outra etapa importante foi entender a diferença entre parar e encerrar uma instância. Ao parar, a máquina pode ser iniciada novamente. Ao encerrar, ela é removida e seus dados podem ser perdidos.

---

## Aprendizados adquiridos

Com a realização deste desafio, aprendi:

- como criar uma máquina virtual na AWS;
- como selecionar uma imagem de sistema operacional;
- como escolher um tipo de instância;
- como configurar um grupo de segurança;
- como utilizar uma chave privada para autenticação;
- como acessar um servidor Ubuntu por SSH;
- como executar comandos básicos no Linux;
- como iniciar, parar, reiniciar e encerrar uma instância;
- como aplicar cuidados básicos de segurança;
- como monitorar custos e evitar cobranças desnecessárias;
- como documentar uma experiência técnica utilizando Markdown e GitHub.

---

## Conclusão

O laboratório permitiu aplicar, de forma prática, os conceitos básicos de computação em nuvem e gerenciamento de servidores virtuais.

A criação da instância EC2 ajudou a compreender como um servidor pode ser configurado e disponibilizado na internet sem a necessidade de adquirir uma máquina física.

Além da parte técnica, o desafio reforçou a importância da segurança, do acompanhamento de custos e da documentação dos procedimentos realizados.

---

## Referências

- Documentação oficial da Amazon EC2;
- Documentação da AWS sobre conexão com instâncias Linux;
- Documentação do GitHub;
- Guia de Markdown do GitHub;
- Conteúdos e aulas disponibilizados pela DIO.

---

## Autor

**Andrew Benvenuto Dias dos Santos**

Desenvolvedor Python com experiência em automações, APIs, bancos de dados e soluções em nuvem.
