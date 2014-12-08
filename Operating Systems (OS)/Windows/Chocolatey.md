# Chocolatey

Imagine poder instalar programas utilizando uma simples linha de comando no [Windows](http://pt.wikipedia.org/wiki/Microsoft_Windows) e ter a mesma experiencia que usuários Linux tem com seus gerenciadores de pacote como [Aptitude](http://pt.wikipedia.org/wiki/Aptitude), [Yum](http://pt.wikipedia.org/wiki/Yum), entre diversos outros. Usuários do [OS X](http://pt.wikipedia.org/wiki/OS_X) também convivem com essas facilidades através de gerenciadores de pacote como [Homebrew](http://brew.sh/) e [MacPorts](http://pt.wikipedia.org/wiki/MacPorts).

O fato é que até o momento (Windows 8.1), gerenciadores de pacotes não são nativos e é necessário instalar uma ferramenta de terceiro como o [Chocolatey](https://chocolatey.org/) para obter acesso a esse recurso.

A instalação do [Chocolatey](https://chocolatey.org/) é simples, abra um terminal como administrador e execute o seguinte comando:

```bash
@powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
```

Apos o termino da instalação uma mensagem de sucesso será apresentada e você estará apto a baixar e instalar programas através do terminal.

Caso queira procurar por algum pacote, dite o seguinte comando:

```bash
choco search atom
```

Uma lista contendo todos os resultados será apresentada. A instalação é simples, copie o nome do software que deseja instalar e faça sua instalação:

```bash
choco install Atom
```

Se precisar desinstalar algum programa utilize o seguinte comando:

```bash
choco uninstall Atom
```

Se quiser saber mais sobre comandos do [Chocolatey](https://chocolatey.org/) digite o seguinte comando:

```bash
choco /?
```

Disponibilizei uma [lista de programas](https://gist.github.com/brunobatista/2d04079ae233de1e7b80) que utilizo, são programas comuns entre desenvolvedores.
