# Modelo LaTeX UPE-PPGEC

Modelo LaTeX para projetos de dissertação e tese do Programa de Pós-graduação em Engenharia da Computação (PPGEC) da Universidade de Pernambuco (UPE).

Elaborado a partir dos originais disponíveis no site do programa PPGEX:
[https://w2.solucaoatrio.net.br/somos/upe-ppgec/index.php/pt/downloads/viewcategory/4-templates](https://w2.solucaoatrio.net.br/somos/upe-ppgec/index.php/pt/downloads/viewcategory/4-templates)

## Começando

Estas instruções lhe darão uma cópia do projeto em sua máquina local, ou serviços de edição LaTeX online, para fins de teste e compilação final.

### Pré-requisitos

Requisitos do modelo LaTeX e outras ferramentas para editar e compilar:
- Se for editar e compilar localmente você irá precisar de:
    - Distribuição LaTeX, recomendo o TexLive, disponível em [https://www.tug.org/texlive/](https://www.tug.org/texlive/)
    - Algum editor de textos habilitado para trabalhar com LaTeX, recomendo TexStudio, VSCode ou Sublime Text:
        - TexStudio (https://www.texstudio.org/)[https://www.texstudio.org/]
        - Visual Studio Code com extensão para trabalhar com LaTeX, gosto muito da extensão LaTeX Workshop, mas ela precisa do Docker com imagem texlive/texlive. Links:
            - Visual Studio Code: (https://code.visualstudio.com)[https://code.visualstudio.com]
            - Extensão LaTeX Workshop: (https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop)[https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop]
            - Docker: (https://docs.docker.com/engine/install/)[https://docs.docker.com/engine/install/]
            - Imagem Docker texlive/texlive: (https://hub.docker.com/r/texlive/texlive)[https://hub.docker.com/r/texlive/texlive]
        - Sublime Text com Package Control e pacote
            - Sublime Text: (https://www.sublimetext.com/)[https://www.sublimetext.com/]
            - Package Control: (https://packagecontrol.io/installation)[https://packagecontrol.io/installation]
            - Pacote LaTeX Tools: (https://packagecontrol.io/packages/LaTeXTools)[https://packagecontrol.io/packages/LaTeXTools]
- Se for editar e compilar online há várias opções:
    - OverLeaf: (https://pt.overleaf.com/)[https://pt.overleaf.com/]
    - Paperia: (https://papeeria.com/)[https://papeeria.com/]
    - CoCalc: (https://cocalc.com/features/latex-editor)[https://cocalc.com/features/latex-editor]

## Edição local

Clone o repositório em sua máquina e edite o código com seu editor LaTeX de preferência:

```bash
git clone https://github.com/joaoferreirape/upe_ppgec_template_latex.git
```

## Macros do documento

No preâmbulo do documento, no arquivo principal, há as *macros do documento* onde **deve-se** editar o conteúdo das variáveis:

<pre>
\titulo{EDITAR}
\autor{O grande mestre do universo}
\local{Recife}
\def\diadefesa{EDITAR}
\def\mesdefesa{EDITAR}
\def\anodefesa{EDITAR}
\data{\diadefesa~de~\mesdefesa~de~\anodefesa}
\orientador{O supremo senhor das galáxias}
\coorientador{O sábio senhor das estrelas}
\def\universidade{Universidade Pernambuco}
\def\centro{Escola Politécnica de Pernambuco}
\def\programa{Programa de Pós-Graduação em Engenharia da Computação}
\instituicao{%
  \universidade{}
  \par
  \centro{}
  \par
  \programa{}
  }
\tipotrabalho{Disertação (Mestrado) ou Projeto de Tese (Doutorado) ou Tese (Doutorado)}
\grau{Mestre ou Doutor}
\preambulo{\tipotrabalho submetido à avaliação pelo Programa de Pós-Graduação em Engenharia da Computação da Universidade Pernambuco como parte dos requisitos para obtenção do grau de \grau em Engenharia da Computação.}
%
\author{\imprimirautor}
\title{\imprimirtitulo}
% \logo{}
% \institute{UPE}  % exclusiva do beamer
\date{\imprimirdata}
% \subject{}
</pre>

## Convenção de nomes

Conjunto de regras para nomeação de arquivos.

### Nome do arquivo principal

Os nomes de arquivos em LaTeX não devem ter acentos, caracteres especiais ou espaços.

Formato: ANO-AUTOR-TIPO.tex

Exemplo: `2024-JOAO-FERREIRA-TESE.tex`

Nota 1: O arquivo final em pdf será gerado com o nome sob o formato do arquivo principal.

Nota 2: Ao mudar o nome do arquivo principal, deverá ser atualizado a *magic quote* no início de cada arquivo `.tex` do projeto.

### Nome dos arquivos de capítulos

Formato: ANO-AUTOR-TIPO-CH0X-TEMA.tex

Exemplo: `2024-JOAO-FERREIRA-TESE-CH01-INTRODUCAO.tex`

### Nome do arquivo de biblioteca

O arquivo contendo a relação de fontes para citação, deverá ser salvo na raiz do projeto com o nome: `library.bib`

## Magic quotes

Ao mudar o nome do arquivo principal, deverá ser atualizada a *magic quote* no início de cada arquivo `.tex` do projeto.

<pre>
% !TeX encoding = UTF-8
% !TeX spellcheck = pt_BR
% !TeX root = 2024-JOAO-FERREIRA-TESE.tex
% ------------------------------------------------------------------------------
</pre>

A linha `% !TeX encoding = UTF-8` informa ao compilador que esse arquivo foi escrito utilizando a codificação de caracteres UTF-8

A linha `% !TeX spellcheck = pt_BR` informa ao compilador que ele poderá fazer verificação ortográfica no idioma especificado, mas sem fazer a correção dos erros.

A linha `% !TeX root = 2024-JOAO-FERREIRA-TESE.tex` informa ao comilador qual será o arquivo principal a partir do qual o projeto será compilado, o nome desse arquivo será o padrão para determinar o nome do arquivo final compilado para `pdf`.

### Buscar recursivamente e modificar nome de arquivos

Nota: Este comando funcionará apenas em sistemas Linux ou MacOS.

Exemplo para modificar recursivamente o padrão `2024-JOAO-FERREIRA` no prefixo do nome dos arquivos para `2024-ZEUS`:

`find . -name '*.*' -print0 | xargs -0 -n1 bash -c 'mv "$0" "${0/2024-JOAO-FERREIRA/2024-ZEUS}"'`

### Buscar recursivamente e modificar texto em arquivos

Exemplo para modificar a *magic quote* de referência ao arquivo principal:

`find . -type f -name "*.tex" -exec sed -i 's/root = 2024-JOAO-FERREIRA/2024-JOAO-ZEUS/g' {} +`

## Contribuindo

Por favor leia [CONTRIBUTING.md](CONTRIBUTING.md) para detalhes sobre os processos de submissão das suas contribuições via `pull request`.

## Autores

  - **João Ferreira** [https://github.com/joaoferreirape](https://github.com/joaoferreirape)

Veja a lista de pessoas que eventualmente tenha contribuído com este projeto:
[https://github.com/joaoferreirape/upe_ppgec_template_latex/graphs/contributors](https://github.com/joaoferreirape/upe_ppgec_template_latex/graphs/contributors)

## Licença

Este projeto está licenciado sob [CC0 1.0 Universal](LICENSE)
Creative Commons License - veja o arquivo [LICENSE](LICENSE) para mais detalhes.
