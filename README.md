# Comandos mais utilizados no git
Simples guia com os códigos git mais utilizados

	Working Directory => Staging Area => Git Directory
	              (git add)          (git commit)
	working directory, index e HEAD

## Configurações Iniciais
    Global
      git config --global user.name "Caio Andrade"
      git config --global user.email "caioandradedesousa@gmail.com"

    Local
      git config user.name "Caio Andrade"
      git config user.email "caioandradedesousa@gmail.com"

## Criar repositório local
    git init

## Criar repositório compartilhado
    git init --bare

## Consultar status do repositório
    git status

## Trackear arquivo
#### Único arquivo
    git add nome_arquivo.extensão
#### Todos arquivos
    git add .
#### Todos os arquivos com .txt
    git add *.txt
#### Trackear arquivo de forma interativa
    git add -i
#### Trackear arquivo declarado no .gitignore
    git add nome_do_arquivo -f
#### Separar mudanças em um mesmo arquivo para comitar separado
    git add -p

## Remover arquivo
    git rm arquivo.txt

## Realizar Commit
    git commit -m "Commit Inicial"

## Trackear e Commitar em conjunto(Só funciona para arquivos já conhecidos pelo GIT)
    git commit -a -m "Descrição do Commit"

## Consultar log de alterações
#### Arquivos do working directory
    git diff
#### Arquivos da staging area
    git diff --staged

## Consultar log de Commit's
#### Log Genérico de todos os commits
    git log
#### Log especifico de todos os commits, uma junção entre git log e git diff
    git log -p
#### Idem ao acima, porém com menos detalhes
    git log --stat
#### Parametro após o p indica a quantidade de log de commits, nesse caso será exibido o último commit
    git log -p -1
#### Abre uma interface com os relatórios de commits
    gitk
#### Mostra somente as mensagens dos logs com a sua chave
    git log --pretty=oneline
#### Git log customizado
    git log --pretty='%an realizou o commit %h: %s'
#### Mostra o log com a ramificação
    git log --graph
#### Visualizar quais arquivos que foram modificados em cada commit do nosso projeto
    git whatchanged -p
#### Visualizar quais as linhas que foram modificadas em cada commit do nosso projeto
    git whatchanged -p

## Alterar um commit sem gerar outro
    git add .
    git commit --amend -m "Commit Errado(CONSERTADO)"

## Reverter mudanças feitas no arquivo do Working Directory
	git checkout -- arquivo_teste.txt
		
## Reverter arquivo da forma como está em uma branch especificada, nesse caso está revertendo o arquivo para a forma como estava na branch master
    git checkout master -- arquivo.php

## Retirar arquivo do Staging Area após o add
    git reset HEAD arquivo_teste.txt

## Exclui o ultimo commit
    git reset HEAD~1 --hard

## Desfaz o último commit, porém deixa as modificações na Staging Area
    git reset HEAD~1 --soft

## Retorna os arquivos modificados para a Working Directory
    git reset HEAD

## Retira todos os arquivos da Working Directory (OBS: Que não sejam conhecidos pelo GIT)
    git clean -f

## Visualizar operações destrutivas realizadas
    git reflog

## Inserir novamente no branch um commit excluido
    git merge ("hash do commit")     

## Para corrigir arquivos com erros sem afetar o branch
  #### Primeiramente os arquivos precisam estar na Staging Area
    git stash	
  #### Logo após corrigidos realizar
    git stash apply
  #### Visualizar lista de stash
    git stash list
  #### Para Limpar o stash
    git stash clear
  #### Para aplicar uma versão específica de um stash
    git stash apply stash@{n}
  #### Para remover uma versão específica de um stash
    git stash drop stash@{n}
  #### Para salvar arquivos alterados no stash
    git stash save "Sua mensagem para o stash"

## Tornar o branch atual o ultimo da historia e atualizado de acordo com o que há de novo no master
    git rebase master

## Criar uma tag (Realease)
  #### Essa tag é referente ao ponto atual do branch master
    git tag -a v1.0 -m "Versao 1.0"
  #### Essa tag é referente ao commit passado por parametro após o v0.0
    git tag -a v0.0 fba4acec2ca9b4f642a013241f3afc7d387a343b -m "Versao 0.0"

## Mostrar todas as tag
    git tag

## Exibir detalhes de uma tag
    git show v0.0

## Ir para a tag(realease)
    git checkout v0.0

## Deletar uma tag
    git tag -t v0.0

## Ir para o branch master
    git checkout master

## Criar um branch
    git branch nomeDoBranch

## Ir para o branch 
    git checkout nomeDoBranch

## Listar branches
  #### Lista branches locais
    git branch
  #### Excluir branch
    git branch -d nomeDoBranch
  #### Lista branches remotas
    git branch -r
  #### Locais e remotas
    git branch -a
  #### Deletar branch remota
    git push origin :design

## Criar e ir para o branch
    git checkout -b nomeDoBranch

## Listar todos os branches
    git branch

## Realizar o merge
    git merge nomeDoBranch

## Criar endereço ssh na máquina local
    ssh-keygen

## Enviar do repositório local para o repositório nas nuvens
 		git push -u origin master
Após executar esse comando, nas próximas vezes que dar push na mesma branch, é só executar `git push`

## Traz atualizações de um repositório remoto
    git fetch nomeServidorRemoto

## Nome do servidor
    git remote (Por padrão é origin)

## Para dar um pull quando há conflitos
    git pull origin master --allow-unrelated-histories

## Criar alias git
    vim ~/.gitconfig
      [alias]
        st = status (git st fica igual git status)
        envia = !git pull && git push
        publica = !git checkout master && git pull && git checkout dev && git rebase master && git checkout master && git merge dev && git push
        git config --global alias.r reset
  
      Personalização
        [color] (Deixar visualização de branches colorida)
            branch = auto ou branch = true ou branch = on ou branch = 1

## Configurar aliases de forma global para ignorar arquivos localmente
    git config --global alias.ignore 'update-index --skip-worktree'
    git config --global alias.unignore 'update-index --no-skip-worktree'
    git config --global alias.ignored '!git ls-files -v | grep "^S"'
  #### Ignora arquivos localmente
    git ignore
  #### Desfaz o comando 'git ignore' e faz com o git volte a reconhecer as alterações do arquivo
    git unignore
  #### Retorna a lista de todos os arquivos ignorados localmente
    git ignored
