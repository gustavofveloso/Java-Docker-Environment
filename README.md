# Java Docker Environment 🚀

Bem-vindo ao **Java Docker Environment**! Este projeto configura um ambiente Docker leve e prático para desenvolver e executar códigos Java, com persistência de arquivos entre sua máquina local e o container. Perfeito para estudos, experimentos ou projetos Java! ☕

## 📋 Descrição

Este repositório contém:

- Um `Dockerfile` baseado no Ubuntu 24.10, com Java 17 (Temurin) instalado via SDKMAN.
- Um `docker-compose.yml` para facilitar a execução do container com bind mount.
- Sincronização de arquivos entre sua máquina e o container, garantindo que seu código fique seguro mesmo se o container for excluído.

O objetivo é ter um ambiente Java portátil e reutilizável, ideal para quem está aprendendo ou trabalhando com Java.

## ✨ Funcionalidades

- **Java 17**: Instalado e pronto para uso.
- **Ferramentas básicas**: Inclui `vim`, `curl` e `zip`.
- **Persistência**: Arquivos salvos na pasta local da sua máquina são sincronizados com o container.
- **Docker Compose**: Configuração simples para rodar tudo com um comando.

## 📂 Estrutura do Projeto

```
especialista-java/
├── Codigos/              # Pasta sincronizada com o container
├── Dockerfile            # Configuração da imagem Docker
├── docker-compose.yml    # Configuração do Docker Compose
└── README.md             # Este arquivo
```

## 🛠️ Pré-requisitos

- [Docker](https://www.docker.com/get-started) instalado.
- [Docker Compose](https://docs.docker.com/compose/install/) instalado.
- Sistema operacional: Windows, Linux ou macOS.

## 🚀 Como Usar

### 1. Clone o Repositório

```
git clone https://github.com/seu-usuario/especialista-java.git cd especialista-java
```

### 2. Configurar a Pasta Local

- Os arquivos Java serão sincronizados com a pasta `Codigos/` na raiz do projeto.

- Se preferir outra pasta, edite o caminho no `docker-compose.yml` no campo `volumes`.

### 3. Construir e Iniciar o Container

```
docker-compose up --build
```

- Isso constrói a imagem e inicia o container em modo interativo.
- Você verá um terminal como `root@<container-id>:/usr/src/especialista-java#`.

### 4. Escrever e Rodar Código Java

- Crie um arquivo Java no container:

```
vim Main.java
```

Exemplo:

```
public class Main {
    public static void main(String[] args) {
        System.out.println("Olá do Docker!");
    }
}
```

- Compile e execute: `javac Main.java   java Main   `
- Os arquivos aparecerão na pasta `Codigos/` na sua máquina!

### 5. Parar o Container

`docker-compose down`

### 6. Rodar em Background (Opcional)

Para rodar em segundo plano: `docker-compose up -d`
Acesse o terminal: `docker-compose exec especialista-java`

## 🔧 Personalização

- **Adicionar ferramentas**: Edite o `Dockerfile` para instalar mais pacotes (ex.: `maven`, `git`).

```
RUN apt-get update && apt-get install -y maven git
```

- **Mudar a versão do Java**: Ajuste a linha do SDKMAN no `Dockerfile`:

```
dockerfile   sdk install java 21.0.1-tem
```

Reconstrua com:

```
docker-compose up --build
```

## 📜 Dockerfile

```
FROM ubuntu:24.10
RUN apt-get update && apt-get install -y vim curl zip
RUN curl -s "https://get.sdkman.io" | bash && \
    /bin/bash -c "source /root/.sdkman/bin/sdkman-init.sh && sdk install java 17.0.14-tem"
RUN echo "source /root/.sdkman/bin/sdkman-init.sh" >> /root/.bashrc
ENV JAVA_HOME="/root/.sdkman/candidates/java/current"
ENV PATH="$JAVA_HOME/bin:$PATH"
WORKDIR /usr/src/especialista-java
```

## ⚙️ Docker Compose

```
services:
  especialista-java:
    build:
      context: .
      dockerfile: Dockerfile
    image: especialista-java
    volumes:
      - C:/Users/Gustavo/Documents/Estudos/Full Cycle/especialista-java/Codigos:/usr/src/especialista-java
    tty: true
    stdin_open: true
    working_dir: /usr/src/especialista-java
```

## 💡 Dicas

- Use um editor como VS Code na pasta `Codigos/` para escrever código e compile no container.
- Para listar arquivos no Ubuntu, instale `lsd`: `apt-get update && apt-get install -y lsd`.

## 🤝 Contribuições

Sinta-se à vontade para abrir issues ou enviar pull requests com melhorias!

##

Feito com ❤️ por Gustavo Farias em 2025.
