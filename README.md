# RUBY NO MACBOOK COM PROCESSADOR M1 - APPLE SILICON

Repositório criado com intuito de ajudar a instalação do Ruby utilizando processadores Apple Silicon (m1).

# Instalando o Ruby

Primeiro devemos aceitar a licença do Xcode. Para isto, rode o seguinte comando:

    sudo xcodebuild -license agree

Adiciona os seguintes comandos no arquivo `.zshrc`:

    export PKG_CONFIG_PATH="/opt/homebrew/opt/readline/lib/pkgconfig"
    export PKG_CONFIG_PATH="/opt/homebrew/opt/libffi/lib/pkgconfig:$PKG_CONFIG_PATH"
    export LDFLAGS="-L/opt/homebrew/opt/zlib/lib"
    export CPPFLAGS="-I/opt/homebrew/opt/zlib/include"
    export RUBY_CONFIGURE_OPTS="--with-openssl-dir=$(brew --prefix openssl@1.1)"
    export PATH="/opt/homebrew/opt/sqlite/bin:$PATH"
    alias abrew='/opt/homebrew/bin/brew'
    alias ibrew='arch -x86_64 /usr/local/bin/brew'

Reinicia o shell:

    exec $SHELL

Instala as dependências:

    brew install openssl libffi zlib rbenv readline ruby-build

Reinicia a máquina.

Instala de fato o Ruby (no caso, o 2.7.1) (cola tudo de uma vez):

    RUBY_CONFIGURE_OPTS=--with-readline-dir="$(abrew --prefix readline)" \ rbenv install 2.7.1

Caso o comando acima não funcione (cola tudo de uma vez):

    LDFLAGS="-L/opt/homebrew/opt/libffi/lib" CPPFLAGS="-I/opt/homebrew/opt/libffi/include" RUBY_CONFIGURE_OPTS=--with-readline-dir="$(abrew --prefix readline)" \

    rbenv install 2.7.1

Adicionar inicialização do rbenv no `.zshrc`:

    export PATH="$HOME/.rbenv/bin:$PATH"
    eval "$(rbenv init -)"

## Configurando o SSH do GitHub

Adicionando o SSH

    ssh-keygen -t ed25519 -C “seuemail@github.com”

Verificando a chave para colar no GitHub

    cat ~/.ssh/*.pub

Obs.: No comando acima trocar o `*.pub` pelo nome do arquivo.

Verificar se está conectado:

    ssh -T git@github.com

## Necessários para configurar o projeto

**Postgres:**

    postgresapp.com

**Evita seguinte problema no `rails db:create`: ExecJS::RuntimeUnavailable: Could not find a JavaScript runtime:**

    brew install v8

**Yarn:**

    brew install yarn

**Node:**

    brew install node

## Possíveis problemas durante a configuração do projeto

**Gem ffy:**

    gem install ffi -v '1.12.2' -- --with-cflags="-Wno-error=implicit-function-declaration"**

**Mimemagick:**

    brew install shared-mime-info
    brew install imagemagick

**Gem Qt5 / Qt5-webkit:**

    sudo port selfupdate
    sudo port install qt5 qt5-qtwebkit

E o seguinte comando para reconhecer o Qt5:

    sudo ln -s /opt/local/libexec/qt5/bin/qmake /opt/local/bin/qmake

Obs.: Para rodar os comandos acima, caso você não tenha o `port` instalado, instale direto com o tutorial do [site](https://guide.macports.org/chunked/installing.macports.html). Logo após acesse `/etc/paths` com o seguinte comando:

    sudo vim /etc/paths

E adicione as linhas abaixo:

    /opt/local/bin
    /opt/local/sbin
**Gem libpq:**

    brew install libpq
    brew link libpq --force
