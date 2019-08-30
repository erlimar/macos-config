My macOS developer configuration
================================

É assim que configuro meu macOS para desenvolvimento.

## Meu hardware

![Meu hardware](my-macos.png)

## O que já temos pronto?

Como um desenvolvedore de software, no macOS já temos várias ferramentas prontas
sem precisar de nenhuma instalação adicional. É só começar a desenvolver:

- Ruby (https://www.ruby-lang.org)
- Perl 5 (https://www.perl.org)
- Python 2 (https://www.python.org)
- PHP 7 (https://www.php.net)
- cURL (https://curl.haxx.se)
- Emacs 22 (https://www.gnu.org/software/emacs)
- Vim 8 (https://www.vim.org)
- OpenSSL/LibreSSL (https://www.libressl.org, https://www.openssl.org)
- SQLite3 (https://www.sqlite.org)
- Swift (https://swift.org)
- Tcl/Tk 8.5 (https://www.tcl.tk)

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

- htop
- git
- java

TODO: Continua...
