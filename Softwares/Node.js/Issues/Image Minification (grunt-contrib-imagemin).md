# Image Minification ([grunt-contrib-imagemin](https://github.com/gruntjs/grunt-contrib-imagemin))

Caso tente executar um `grunt build`, subir servidor com `grunt server` ou até injetar dependências com `grunt wiredep` e for apresentado um erro como o abaixo:

```bash
Loading "imagemin.js" tasks...ERROR
>> Error: Cannot find module 'imagemin-gifsicle'
```

Não se preocupe, uma das dependências do modulo `grunt-contrib-imagemin` falhou ou foi mau instalada. Veja abaixo como proceder para corrigir isso.
 
Para corrigir a questão precisamos reinstalar o modulo `grunt-contrib-imagemin`. O Windows tem um limite de 260 caracteres no tamanho do endereço da pasta/arquivo, isso resulta em um erro ao tentar remover pacotes do Node.js, que normalmente tem o endereço superior a 260 caracteres. Para resolver isso instale o `rimraf`:

```bash
npm install rimraf -g
```

Este pacote habilita a deleção de arquivos e pastas recursivamente. Agora utilize o `rimraf` para remover o pacote `grunt-contrib-imagemin`:

```bash
rimraf node_modules/grunt-contrib-imagemin
```

Feita a remoção do pacote `grunt-contrib-imagemin`, iremos instalar novamente este pacote:

```bash
npm install grunt-contrib-imagemin
```

Para testar e verificar se tudo ocorreu bem, execute o comando `grunt wiredep` do [Grunt](http://gruntjs.com/). Essa tarefa tentará injetar todas as dependências do frontend e caso tudo ocorra bem ele não irá apresentar erro algum:

```bash
grunt wiredep
```
