My macOS developer configuration
================================

É assim que configuro meu macOS para desenvolvimento.

## Meu hardware

![Meu hardware](my-macos.png)

## O que já temos pronto?

Como um desenvolvedore de software, no macOS já temos várias ferramentas prontas
sem precisar de nenhuma instalação adicional. É só começar a desenvolver:

- Git (https://git-scm.com)
- Ruby (https://www.ruby-lang.org)
- Perl 5 (https://www.perl.org)
- Python 2 (https://www.python.org)
- Tcl/Tk 8.5 (https://www.tcl.tk)
- Swift (https://swift.org)
- PHP 7 (https://www.php.net)
- Apache 2 (https://www.apache.org)
- cURL (https://curl.haxx.se)
- Vim 8 (https://www.vim.org)
- Emacs 22 (https://www.gnu.org/software/emacs)
- OpenSSL/LibreSSL (https://www.libressl.org, https://www.openssl.org)
- SQLite3 (https://www.sqlite.org)

Além, é claro, de ser um UNIX (http://www.unix.org), e por isso tem inúmeras outras
ferramentas que podemos usar no dia-a-dia, tais como (yacc, gnumake, tar, unzip, etc.).

## E o que precisamos mais?

Como desenvolvedor de múltiplas linguagens, mesmo já tendo toda essa lista
de linguagens apresentada lá em cima, ainda me falta as ferramentas para desenvolvimento
nativo. Além é claro de algumas dessas ferramentas estarem com versões antigas.

Assim, precisamos instalar os compiladores para código nativo, e isso pode ser
feito com o comando `xcode-select --install`. Porém, nós também precisaremos atualizar
as versões dos softwares já instalados e instalar outros, e para isso eu utilizo o
Homebrew (https://brew.sh). Ao instalar o Homebrew, ele já instala as ferramentas
nativas que seriam instaladas com o comando `xcode-select --install`, portanto não
precisaremos executá-lo separadamente.

Então instale o Homebrew seguindo as instruções de https://brew.sh.
Quando a instalação terminar, nós teremos além do próprio comando `brew`,
também os compiladores nativos:

- Compiladores **C**: clang, gcc, cc, c89, c99
- Compiladores **C++**: clang++, g++, c++, cpp

Já não temos porque reclamar, como desenvolvedor, temos agora um arsenal de ferramentas
de desenvolvimento das mais variadas tecnologias e plataformas disponíveis só aguardando
nossa codificação.

Mas ainda precisamos de mais algumas ferramentas, e utilizaremos o Homebrew para
instalá-las:

## Primeiramente vamos atualizar nossas ferramentas já instaladas

### Git

O Git talvez seja a ferramenta que mais utilizo no desenvolvimento de software.
Aqui já temos a versão `2.17` instalada, mas vamos atualizá-la:
```
$ brew install git
```

Pronto, agora temos a última versão disponível.

### Ruby

Já temos o Ruby `v2.3` que vem com o `gem 2.5`, e queremos usar a última versão
disponível:
```
$ brew install ruby
```

Trabalhar com duas versões do Ruby pode causar alguns probleminhas, por isso
o `brew` não atualiza os links e se você tentar executar `ruby` em seu
terminal, verá que lá ainda está a versão `2.3`. Mas basta você atualizar
sua variável de ambiente `$PATH` para resolver o problema:
```
$ echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.bashrc
```

Agora temos o Ruby `v2.6` com o `gem 3.0` disponível.

### ~/.bashrc e ~/.bash_profile

Não quero aqui entrar na discussão das diferenças entre os arquivos de
configuração `~/.bash_profile` e `~/.bashrc`, então deixo esse link para você
saber mais sobre o assunto:
https://medium.com/@kingnand.90/what-is-the-difference-between-bash-profile-and-bashrc-d4c902ac7308

Mas eu uso a seguinte configuração na minha máquina:

Tenho o arquivo `~/.bashrc` e uso somente ele para configurar minhas variáveis
de ambiente e personalizações.

Mas também tenho o arquivo `~/.bash_profile` para as configurações iniciais de logon,
esse por sua vez inclui `~/.bashrc` para as configurações de variáveis de ambiente
e personalizações.
```sh
$ ~./bash_profile << EOF
# Include ~/.bashrc if exists
if [ -f ~/.bashrc ]; then
    source ~/.bashrc
fi
EOF
```

### Perl

O Perl que vem instalado é o `v5.18` com `cpan 1.61`. Vamos atualizá-los:
```sh
$ brew install perl
```

Agora temos o Perl `v5.30` com `cpan 1.64`.

Mas existe um pequeno problema, sempre que você instalar um módulo com a nova
versão do Perl, ele será instalado nos diretórios _Cellar_, isso tem o
inconveniente de que quando você atualizar sua versão via `brew`, seus pacotes
serão perdidos e terão que ser instalados novamente.

Então vamos seguir as dicas que são exibidas logo que você termina a instalação
via `brew install perl`:
```sh
$ PERL_MM_OPT="INSTALL_BASE=$HOME/perl5" cpan local::lib
echo 'eval "$(perl -I$HOME/perl5/lib/perl5 -Mlocal::lib=$HOME/perl5)"' >> ~/.bashrs
```

Agora seus pacotes são persistidos entre as atualizações futuras. Vamos aproveitar
e atualizar todos os pacotes Perl que já estão instalados?
```sh
$ cpan -u
```

Demora um pouco, mas vale à pena!

Para uma experiência mais moderna, sugiro também experimentar o **Perl6**
(https://www.perl6.org/), por isso vamos instalá-lo também:
```sh
$ brew install perl6
```

### Python

Já temos o Python `v2.7` instalado, e ele vem com o `easy_install` e o `wheel`.
Só não temos o `pip`, então primeiramente vamos completar a instalação do Python `v2`
também com o `pip`:
```
$ sudo easy_install pip
```

Também vamos instalar o Python `v3` que já vem com o `pip`, e de quebra traz o
`virtualenv` pra nós:
```
$ brew install python@3
```

### Tcl/Tk

Já temos o Tcl/Tk 8.5, mas podemos usar também a última versão `8.6`:
```
$ brew install tcl-tk
```

Em seguida você precisará atualizar sua variável de ambiente $PATH:
```sh
$ echo 'export PATH="/usr/local/opt/tcl-tk/bin:$PATH"' >> ~/.bashrc
$ . ~/.bashrc
```

### Swift

> TODO

### PHP 7

Também queremos a última versão do PHP disponível:
```sh
$ brew install php
```

### Apache

O Apache 2 já está instalado em nossa máquina, mas se você tentar acessar o endereço
`http://localhost`, não vai ver nada. Isso porque o apache vem parado por padrão,
então vamos iniciá-lo:
```
$ sudo apachectl start
```

Pronto! Agora ao acessar `http://localhost`, você verá uma página dizendo **It work!**.
Isso quer dizer que o apache está rodando na nossa máquina.

### cURL

Agora a última versão do cURL:
```sh
$ brew install curl
```

Para esse também precisamos atualizar nossa variável de ambiente `$PATH`:
```sh
$ echo 'export PATH="/usr/local/opt/curl/bin:$PATH"' >> ~/.bashrc
$ . ~/.bashrc
```

### Vim 8

Quanto ao Vim, eu particularmente prefiro usar o Neovim (https://neovim.io), mas como já temos
o Vim 8 instalado, vamos primeiro atualizar para a última versão:
```sh
$ brew install vim
```

> PS: Agora de quebra ganhamos mais uma linguagem na nossa lista, **lua** na versão `5.3`

Agora sim, vamos instalar o **Neovim**. A última versão é a `v0.3`:
```sh
$ brew install neovim
```

Quanto a configuração vom **Vim/Neovim**, isso é um capítulo à parte, por isso
eu deixei um repositório com minha configuração toda documentada para você usá-la também.

Acesse https://github.com/erlimar/vim-config, lá você encontra tanto minha configuração
**Vim** quanto **Neovim**, e não só para macOS, mas também para Windows e Linux.
De quebra tem um pequeno quadro com os comando mais usados, você pode usá-lo para
aprender caso seja um iniciante em **Vim** (como eu).

No caso do **macOS** eu recomendo atualizar o mapeamento da tecla **Lead** de `\\`
para `\<Space` devido ao layout do teclado.

### Emacs

Já temos o Emacs 22, mas se você quer utilizar os recursos modernos eo **Emacs**
(como eu), precisamos atualizar para a versão `v26`:
```sh
$ brew install emacs
```

Se você não se sentir confortável com utilizar a tecla `ESC+m` como tecla de meta,
pode encontrar uma ajuda em https://www.emacswiki.org/emacs/MetaKeyProblems.

### OpenSSL/LibreSSL

Já temos o LibreSSL `2.2.7` instalado mas eu prefiro a última versão disponível:
```sh
$ brew install openssl
```

Só que também vamos precisar atualizar nossa variável de ambiente `$PATH`:
```sh
$ echo 'export PATH="/usr/local/opt/openssl/bin:$PATH"' >> ~/.bashrc
$ . ~/.bashrc
```

### SQLite3

O SQLite3 é uma mão na roda para o desenvolvimento com banco de dados local,
por isso vamos atualizá-lo também:
```sh
$ brew install sqlite3
```

Para esse também precisamos atualizar nossa variável de ambiente `$PATH`:
```sh
$ echo 'export PATH="/usr/local/opt/sqlite/bin:$PATH"' >> ~/.bashrc
$ . ~/.bashrc
```

## E ainda precisamos de mais alguma coisa?

Ainda vamos precisar de mais umas ferramentas para completar nosso quadro
de linguagens modernas:

### Java/JDK

Não podemos ter um set completo de linguagens sem incluir **Java**, por isso
vamos instalar tanto o tempo de execução quanto o kit de desenvolvimento Java:
```sh
$ brew cask install oracle-jdk
```

Com isso temos o Java 12 pronto para desenvolver.

Se preferir OpenJDK ao invés do Oracle JDK:
```sh
$ brew cask install java
```

### htop
```sh
$ brew install htop
```

### NodeJS

Não dá pra falar de desenvolvimento de software moderno sem mencionar **NodeJS**:
```sh
$ brew install node
```

### Rust

Eu particularmente considero o uso da linguagem Rust (https://rust-lang.org) para
o desenvolvimento moderno de aplicativos de alto desempenho além da construção
de sistemas nativos.

O sistema de instalação é tão completo e eficiente, que nesse caso não vamos usar
o `brew`, mas o próprio instalador (https://rustup.rs/):
```sh
$ curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
$ cat ~/.cargo/env >> ~/.bashrc
```

### Visual Studio Code

Esse é um editor inteligente moderno que acredito não poder faltar no seu set
de ferramentas:
```sh
$ brew cask install visual-studio-code
```

### Docker

Além das linguagens e editores que instalamos para utilizar no nosso dia-a-dia no
desenvolvimento de softwares, ainda faltam coisas como banco de dados, serviços
de mensageria, etc. Mas todos esses recursos tem mais a ver com o propósito
específico de cada projeto.

Eu particularmente no dia-a-dia, como preciso lidar com várias versões da mesma
ferramenta, aprendi que as vezes isso fica difícil, porque muitas vezes precisamos
desinstalar uma versão e depois instalar outra e ficar chaveando entre elas.
É certo que as linguagens mais modernas já resolvem isso com os seus gerenciadores
de versões, como o `rustup` que instalamos para **Rust**, com ela podemos gerenciar
as várias versões de Rust em nossa máquina. Mas outras linguagens já antes mesmo
usavam recursos parecidos, como **rvm** para Ruby, ou **nvm** para NodeJS, ou
**virtualenv** para Python.

Na verdade não precisávamos nem ao menos ter instalado todas essas ferramentas
e linguagens na nossa máquina. Poderíamos simplesmente usá-las via **Docker**.

Mas como isso depende de uma máquina com boa memória (8GB já resolvem, mas recomendo
pelo menos 16GB), além de um bom processador.

Eu já experimentei não ter nenhuma linguagem instalada diretamente em minha máquina,
ao invés disso usava somente o Docker, assim não sujava minha máquina com
instalações diversas. Mas no dia-a-dia ter a ferramenta rodando na máquina real
é a melhor opção.

Mas para todos os outros recursos (banco, cache, mensageria, etc.), uso o Docker,
por isso vamos instalá-lo:
```sh
$ brew install docker
```

TODO
* Configurar
  - Oh My Zsh com fontes Powerline
  - Terminal
