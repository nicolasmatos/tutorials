# Assemble

Assemble é um gerador de site estático (parecido com [Jekyll](http://jekyllrb.com/)), junto ao [Handlebars.js](http://handlebarsjs.com/) que é um motor de template, podemos trabalhar com inclusão de partials e templates em nosso projeto. Iremos utilizar essas ferramentas com o gerador [webapp](https://github.com/yeoman/generator-webapp), porem você pode utilizar este mesmo tutorial com outros geradores do [Yeoman](http://yeoman.io/).

## Estrutura

Partindo do pressuposto que você já tenha uma instalação do [webapp](https://github.com/yeoman/generator-webapp) instalada, agora precisamos adequá-la ao Assemble. Acesse o diretório `app` e crie a seguinte estrutura de diretórios e arquivos:

	app/
		templates/
			data/
				data.json
			layouts/
				master.hbs
				page.hbs
			pages/
				index.hbs
				about.hbs
				contact.hbs
			partials/
				header.hbs
				navigation.hbs
				footer.hbs

Copie o conteúdo do arquivo `app\index.html` e cole dentro do arquivo `app\templates\layouts\master.hbs`. Remova o arquivo `app\index.html`, não será mais necessário. Volte ao arquivo `app\templates\layouts\master.hbs` e remova todo HTML dentro da classe `.container` e adicione o código `{{> body}}`:

```html
[...]
<div class="container">
  {{> body}}
</div>
[...]
```

```html
---
layout: master.hbs
---
{{> header}}
{{> body}}
{{> footer}}
```

```html
<header role="banner">
	<h1>{{title}}</h1>
	{{> navigation}}
</header>
```

```html
<nav role="navigation">
	<ul class="list-inline">
		<li><a href="index.html">Home</a></li>
		<li><a href="about.html">About</a></li>
		<li><a href="contact.html">About</a></li>
	</ul>
</nav>
```

```html
<hr>
<footer role="contentinfo">
	&copy; 2014 Codexplain - Making the code be easy.
</footer>
```

```html
---
title: Home
---
<main role="main">
	Home content here.
</main>
```

```html
---
title: About
---
<main role="main">
	About content here.
</main>

```

```html
---
title: Contact
---
<main role="main">
	Contact content here.
</main>
```

### Suporte ao Assemble

```bash
npm install assemble
```

1. 

	```js
		grunt.initConfig({
		[...]
		livereload: {
			[...]
			files: [
				'<%= config.app %>/templates/{,*/}*.hbs',
				[...]
			]
		},
		[...]
	});
	```

2. 

		```js
		grunt.initConfig({
			watch: {
				[...]
				assemble: {
					files: [
						'<%= config.app %>/templates/data/{,*/}*.json',
						'<%= config.app %>/templates/layouts/{,*/}*.hbs',
						'<%= config.app %>/templates/pages/{,*/}*.hbs',
						'<%= config.app %>/templates/partials/{,*/}*.hbs'
					],
					tasks: ['assemble:server']
				}
			},
			[...]
		});
		```

3. 

		```js
		grunt.initConfig({
			[...]
			wiredep: {
				app: {
					[...]
					src: ['<%= config.app %>/templates/layouts/master.hbs'],
					[...]
				},
				[...]
			},
		});
		```

4. 

		```js
		grunt.initConfig({
			[...]
			useminPrepare: {
				[...]
				html: '<%= config.app %>/templates/layouts/master.hbs'
			},
			[...]
		});
		```

5. 

		```js
		grunt.initConfig({
			[...]
			// Convert .hbs files to .html
			assemble: {
				options: {
					data: [
						'<%= config.app %>/templates/data/*.json',
						'package.json'
					],
					layoutdir: '<%= config.app %>/templates/layouts',
					layout: 'page.hbs',
					partials: ['<%= config.app %>/templates/partials/{,*/}*.hbs'],
					flatten: true
				},
				server: {
					files: [{
						expand: true,
						cwd: '<%= config.app %>/templates/pages/',
						src: ['{,*/}*.hbs'],
						dest: '.tmp',
						ext: '.html'
					}]
				}
			}
		});
		```

6. 

		```js
		grunt.loadNpmTasks('assemble');
		```

7. 

		```js
		grunt.registerTask('serve', [...], function (target) {
			grunt.task.run([
				[...]
				'wiredep',
				'assemble',
				'concurrent:server',
				[...]
			]);
		});
		```

8. 

		```js
		grunt.registerTask('build', [
			[...]
			'wiredep',
			'assemble',
			'useminPrepare',
			[...]
		]);
		```

### Correções
