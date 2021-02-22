# CRIANDO E CONFIGURANDO PROJETO
git init
git remote add origin git@github.com:ThiagoBarradas/my-project.git

# Faz modificações no projeto e faz commits etc

# Agora, vamos adicionar a primeira tag, fazer o merge para develop e sincronizar com o remote
# Assim teremos a estrutura das branches fixas
git tag 0.0.1
git checkout -b develop

git push origin master
git push origin master --tags
git push origin develop

# CRIANDO FEATURE 
# Fluxo idêntico para bugfix e requirement, mudando somente o prefixo do nome da branch
# Vamos iniciar uma nova feature a partir da develop
git pull origin develop
git checkout -b feature/something develop

# Faz modificações no projeto e faz commits etc
# Eventualmente pode pegar atualizações (merge) da develop para ficar atualizado

# FINALIZANDO FEATURE (OU BUGFIX, REQUIREMENT)
# A feature está pronta para entrar para a próxima release? 
# Vamos fazer o merge para a develop, deletar a branch e sincronizar com o remote
git checkout develop
git merge --no-ff feature/something 
git branch -D feature/something

git push develop 
git push feature/something

# CRIANDO RELEASE
git pull origin develop
git checkout -b release/1.0.0 develop

# Se necessário algum 'micro ajuste' faça direto na branch
# Se necessário pegar mais coisas que chegaram deppois na develop, faça o merge da develop para a sua release

# FINALIZANDO RELEASE
git checkout master 
git merge --no-ff release/1.0.0
git tag -a 1.0.0

git checkout develop
git merge --no-ff release/1.0.0 

git branch -D release/1.0.0

git push origin master
git push origin master --tags
git push origin develop
git push origin release/1.0.0

# APARECEU UM BUG CRITICO! PRECISAMOS CRIAR UM HOTFIX!
# CRIANDO HOTFIX
git pull origin master
git checkout -b hotfix/1.0.1 master

# Ache o bug, corrija e faça os commits

# FINALIZANDO HOTFIX
git checkout master 
git merge --no-ff hotfix/1.0.1
git tag -a 1.0.1

git checkout develop
git merge --no-ff hotfix/1.0.1

git branch -D hotfix/1.0.1

git push origin master
git push origin master --tags
git push origin develop
git push origin hotfix/1.0.1


## COM COMANDOS GIT FLOW

# CRIANDO E CONFIGURANDO PROJETO
git init
git remote add origin git@github.com:ThiagoBarradas/my-project.git

# Faz modificações no projeto e faz commits etc

# Agora, vamos adicionar a primeira tag, fazer o merge para develop e sincronizar com o remote
# Assim teremos a estrutura das branches fixas
git tag 0.0.1
git checkout -b develop

git push origin master
git push origin master --tags
git push origin develop

# INICIANDO GIT FLOW NO PROJETO 
git flow init

# No meu caso, não faço 'customizações' e apenas dou <enter> até o fim do setup

# CRIANDO FEATURE
git flow feature start add-something

# Faz modificações no projeto e faz commits etc
# Eventualmente pode pegar atualizações (merge) da develop para ficar atualizado

# FINALIZANDO FEATURE (OU BUGFIX, REQUIREMENT)
# A feature está pronta para entrar para a próxima release? 
git flow feature finish add-something --push

# CRIANDO RELEASE
git flow release start 1.0.0

# Se necessário algum 'micro ajuste' faça direto na branch
# Se necessário pegar mais coisas que chegaram deppois na develop, faça o merge da develop para a sua release

# FINALIZANDO RELEASE
git flow release finish 1.0.0 --push

# APARECEU UM BUG CRITICO! PRECISAMOS CRIAR UM HOTFIX!
# CRIANDO HOTFIX
git flow hotfix start 1.0.1

# Ache o bug, corrija e faça os commits

# FINALIZANDO HOTFIX
git flow hotfix finish 1.0.1 --push
