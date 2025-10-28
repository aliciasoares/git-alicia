# 🧩 Aula Prática – Git Local (sem GitHub)

## 🎯 Objetivo
Aprender a utilizar o **Git** localmente para versionar projetos, criando commits, branches e manipulando o histórico de forma segura.

---

## 🧱 1. Configuração inicial
Para realizar qualquer ação em um repositório, seja configurar ou gerenciar, é preciso abrir o **CMD (Prompt de Comando) ou o GitBash**,, pois são neles que todas as instruções do Git são executadas.

Primeiramente, é importante que esses comandos sejam **adicionados**. Esses comandos configuram o nome e o e-mail do usuário (necessário para registrar os commits).

```bash
git config --global user.name "Seu Nome" 
git config --global user.email "seuemail@exemplo.com"
git config --global core.editor "code --wait"   # Define o VS Code como editor padrão (opcional)
git config --list                                # Verifica as configurações atuais
```

Exemplo com outro repositório:
```bash
git config --global user.name "Alicia Oliveira"
git config --global user.email "aliciaoliveirasoaress@gmail.com"
git config --global core.editor "code --wait"   
git config --list
```
> git config --global user.name "Alicia Oliveira"
- Esse comando define o **nome** que aparecerá nos commits. Esse nome serve para identificar **quem fez cada alteração** no projeto (nesse caso, *“Alicia Oliveira”* é apenas um exemplo, cada pessoa pode colocar o seu.).

- Já o comando **git config --global user.email** "aliciaoliveirasoaress@gmail.com" determina o **e-mail** que será exibido junto ao nome nos commits, o que ajuda a rastrear as contribuições de cada pessoa.

- Para conferir se essas informações foram registradas corretamente, existe o comando **git config --list**, que mostra todas as configurações feitas até o momento.

---

## 📂 2. Criar e iniciar um repositório

```bash
mkdir meu_projeto
cd meu_projeto
git init
```
### Explicações;
- O comando **mkdir** meu_projeto cria uma nova pasta chamada *meu_projeto*. O nome pode ser qualquer um, pois o comando serve para **criar o local onde o projeto vai ficar armazenado**
- Em seguida, o comando **cd meu_projeto** é usado para entrar dentro da pasta recém-criada. Ele muda o diretório atual do CMD para **dentro** de *meu_projeto.*
- Depois, com o comando **git init**, o Git cria um *repositório* dentro dessa pasta. Isso significa que, a partir desse momento, o Git começa a **monitorar as alterações feitas nos arquivos desse diretório**.

> O comando `git init` cria um repositório local, gerando a pasta oculta `.git`.

---

## 🏷️ 3. Alterar a branch padrão de `master` para `main`

Por padrão, o Git pode criar a branch inicial como master. 
Para padronizar e seguir boas práticas, altere para **main**:

```bash
git branch -m master main
```

Se quiser definir **main** como padrão para novos repositórios:

```bash
git config --global init.defaultBranch main
```
- Como  hoje em dia é mais comum usar o nome **main** para branchs iniciais, o comando **git branch -M main** serve justamente para renomear a branch principal para main, deixando o projeto *atualizado com o padrão usado por plataformas como o *GitHub.*

---

## 📄 4. Criar arquivos e verificar status

```bash
echo "Meu primeiro arquivo" > readme.txt
git status
```
- O comando **echo "Meu primeiro arquivo" > readme.txt** cria um novo arquivo chamado **readme.txt** e já coloca dentro dele o texto *“Meu primeiro arquivo”*.O echo normalmente serve para **mostrar mensagens na tela**, mas quando é combinado com o símbolo *">"*, o texto é redirecionado para *dentro de um arquivo.* Se esse arquivo ainda não existir, ele será **criado automaticamente.**

> `git status` mostra arquivos novos, modificados ou prontos para commit. 
- Ele indica se há **arquivos novos, modificados ou excluídos** desde o último commit. Por exemplo, logo após criar o **readme.txt**, o Git vai avisar que há um “untracked file”, ou seja, um arquivo novo que ainda não está sendo monitorado. Esse arquivo só vai passar a ser monitorado após o comando **ADD.**


---

## 🧺 5. Adicionar arquivos à área de staging

```bash
git add readme.txt       # adiciona um arquivo específico
git add .                # adiciona todos os arquivos do diretório
git status
```

> A área de staging é onde os arquivos ficam “preparados” antes do commit.
- Com o comando **git add readme.txt**,o arquivo *readme.txt* passa a ser incluído na chamada *staging area (ou área de preparação)*. Isso significa que ele está pronto para ser salvo oficialmente no **histórico do repositório.**
- Se o comando *git status for usado novamente*, o Git mostrará que o arquivo deixou de ser **“untracked”** (não rastreado) e agora está **“staged”** (preparado), ou seja,  ou seja, o Git agora reconhece o arquivo como sendo um **novo arquivo dentro do repositório.**

---

## 💾 6. Fazer o primeiro commit

```bash
git commit -m "Primeiro commit - adiciona readme.txt"
```

> Um commit é o “salvamento” oficial no histórico do repositório.

- O comando **git commit -m "Primeiro commit - adiciona readme.txt"**
 cria um **commit**. Ele registra **todas as mudanças** feitas nos arquivos que estavam na *área de preparação*, junto com uma mensagem que explica o que foi alterado. O commit é muito importante porque permite **voltar no tempo se algo der errado**, além de ajudar a acompanhar a *evolução do projeto.*


---

## 🔍 7. Ver histórico e detalhes
- Se quiser visualizar o **histórico de commits do seu repositório**, use o comando **“git log”**, que  mostra quem fez as alterações, quando e a mensagem associada a cada commit. 

```bash
git log
git log --oneline
git show
```

> Use `--oneline` para visualizar um resumo simplificado.
- Nesse comando, há algumas variações, como o **git log --oneline,** que mostra o **histórico de commits do repositório,** mas de forma resumida e organizada em uma *única linha por commit*, e o git show, que exibe informações detalhadas sobre um commit específico. Por padrão, ele mostra o **commit mais recente.**

---

## ✏️ 8. Editar arquivos e registrar mudanças
- Se quiser modificar o **readme.txt**, é possível usar novamente o comando echo para **adicionar novas linhas de texto**.  Depois de editá-lo,  basta usar novamente o git add readme.txt para preparar as novas mudanças e, em seguida, o *git commit -m* para registrar essas alterações no **histórico do repositório.**


```bash
echo "Adicionando nova linha" >> readme.txt
git status
git diff
git add readme.txt
git commit -m "Atualiza readme.txt com nova linha"
```

> `git diff` mostra as diferenças entre a versão atual e a anterior.Assim, dá para ver exatamente **o que foi alterado**, por exemplo, uma nova linha adicionada abaixo de *“Meu primeiro arquivo”.*

---

## ♻️ 9. Desfazer mudanças
- Caso queira **desfazer mudanças**, você pode utilizar os comandos **“git restore”**, que descarta mudanças não adicionadas ou o, *“git restore --staged”* que é usado para remover arquivos da área de staging sem apagar as mudanças feitas nele.  Os dois, são ideais para **corrigirem erros antes de realizar outro Commit.**

```bash
git restore readme.txt              # descarta mudanças não adicionadas
git restore --staged readme.txt     # remove da área de staging
```

> Ideal para corrigir erros antes de um commit.

---

## 🌿 10. Criar e alternar entre branches
- Para criar uma branch, utilize o comando **git branch nome-da-branch** uma branch (ou ramo) no Git é uma versão *independente* do seu projeto, onde você pode fazer alterações **sem afetar a versão principal.**
Para mudar do diretório atual para sua branch, utilize o **git switch <nome-da-branch>** que é usado para mudar de uma branch para outra no Git. Quando você trabalha com várias branches em um repositório, você pode usar esse comando para **alternar entre elas** de maneira rápida e fácil.
Obs: O comando **Git branch sozinho**, sem nenhum argumento, mostra *todas as branches existentes no projeto e indica em qual delas você está trabalhando no momento.*


```bash
git branch                         # lista branches
git branch nova_funcionalidade     # cria nova branch
git switch nova_funcionalidade     # muda para ela
```

> Cada branch é uma linha independente de desenvolvimento.

---

## 🧬 11. Fazer commits em outra branch
- Para adicionar mudanças em uma branch **diferente da principal**, você primeiro precisa estar nessa branch (usando git switch nome-da-branch). Depois, o fluxo de commits funciona *normalmente*, como se estivesse na branch principal, e você pode usar os comandos **echo**, **git add** e **git commit** normalmente.


```bash
echo "Nova feature" > feature.txt 
git add feature.txt
git commit -m "Adiciona nova feature"
```

-  **echo** > Cria um arquivo chamado feature.txt com o texto **"Nova feature"**. Esse arquivo existirá apenas na branch em que você está, até que seja **mesclado** com outra branch
- **git add feature.txt** > Adiciona o arquivo à *staging area*, preparando-o para ser **incluído** na proxima vez que você fizer um commit.
- **git commit -m "Adiciona nova feature"**> Cria um commit **registrando que o arquivo foi adicionado na branch atual.**

---

## 🔀 12. Voltar e mesclar mudanças
- Caso queira **mesclar** as mudanças feitas em uma branch na outra, utilize o comando **“git merge”**, que é um comando do Git usado para **integrar alterações** de uma branch em outra.

```bash
git switch main
git merge nova_funcionalidade
```
> Junta as alterações da branch `nova_funcionalidade` na `main`.
- No exemplo, a branch atual foi mudada para a branch principal com o  **“git switch main”**, e com o git merge nova_funcionalidade,as mudanças feitas na branch chamada **nova_funcionalidade** foram incorporadas na branch main. Ou seja, tudo o que foi alterado na branch nova_funcionalidade foi **unido à branch principal.**


---

## 🗑️ 13. Excluir branches locais
- Caso queira **deletar uma branch**, utilize o comando git branch -d. O -d significa **“delete”**, mas com uma verificação: ele só apaga a branch se ela já foi mesclada. Se você quiser forçar a exclusão sem essa verificação, utilize **git branch -D nome_da_branch.**

```bash
git branch -d nova_funcionalidade
```

---

## 🧹 14. Ignorar arquivos com `.gitignore`
- Para ignorar arquivos, abra seu repositório em algum editor de código como o VSCODE.

- Crie um arquivo chamado `.gitignore` e adicione:

```bash
*.log #ignora todos os arquivos que terminam com .log
*.tmp #ignora todos os arquivos temporários, que não têm relevância para o projeto.
node_modules/ #ignora a pasta node_modules, (ela contém milhares de arquivos que podem ser facilmente recriados com npm install.)
```
- Depois de criar o arquivo **.gitignore**, você precisa voltar ao CMD, adicioná-lo e fazer um **commit** para registrar no repositório:

Depois:

```bash
git add .gitignore
git commit -m "Adiciona arquivo .gitignore"
```

---

## 🧠 15. Visualizar informações úteis
- Para visualizar **informações úteis sobre os seus commits**, comandos anteriores como o *git status* e o *diff* podem ser utilizados, porém há também outros que **auxiliam** nessa verificação, vistos abaixo:

```bash
git status
git log --oneline --graph --decorate
git diff
git show HEAD
```

> `--graph` mostra o histórico de commits com ramificações visualmente, de forma resumida, pois **desenha as branches** e **merges**, facilitando a visualização da estrutura do projeto, enquanto o **--decorate adiciona informações extras**, como os nomes das branches e tags associadas a cada commit.
- Além disso, há também o **git show HEAD** que exibe detalhes do último commit feito, incluindo o *autor*, a *mensagem8 e as *mudanças realizadas*.


---

## 💡 16. Exemplo de fluxo completo

```bash
git init
echo "Aula prática Git local" > readme.txt
git add .
git commit -m "Primeiro commit"
git branch dev
git switch dev
echo "Nova versão em desenvolvimento" >> readme.txt
git add .
git commit -m "Atualiza versão dev"
git switch main
git merge dev
git log --oneline --graph
```

## Como integrar o Git local ao GitHub;
---

## 📘 Créditos

Material criado para fins educacionais na aula prática de **Git Local**,  
ministrada por *Anderson R. M. Gomes* 🧑‍🏫

---

**🚀 Próximos passos:**  
Na próxima aula, você aprenderá a conectar este repositório local ao GitHub com os comandos `git remote`, `git push` e `git pull`.
