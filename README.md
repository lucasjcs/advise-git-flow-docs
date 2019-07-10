
# Utilizando Git Flow para controle de versões.
No nosso modelo de fluxo usamos alguma branches específicas pra cada situação de desenvolvimento, sendo elas:

 - **Master**: Fica a versão de homologação, que geralmente será lançada para produção. A versão da master deve estar sempre testada;
 - **Hotfix**: Aqui são feitas as correções emergenciais de bugs encontrados em produção. Essa branch é criada a partir da master 
 - **Develop**: Fica a versão de desenvolvimento.
 - **Feature**: Aqui é onde criamos novas funcionalidades e melhorias no sistema. Essa branch é criada a partir da develop.

Na imagem abaixo é possível visualizar o fluxo de desenvolvimento utilizando o `git flow`:

![](https://miro.medium.com/max/700/1*8-zDz1s5Atux_yNW_mXmfg@2x.png)

## Como utilizar o Git Flow
É importante configurar o git flow antes mesmo de começar a desenvolver qualquer alteração no código.
pra iniciar o git flow no projeto basta rodar o comando: `git flow init` e setar o nome das branches conforme a imagem abaixo:
![](https://i.imgur.com/9huGc7v.png)


### Desenvolvendo melhorias
Para desenvolver novas features e melhorias precisamos criar uma nova branch a partir da **develop**, nesse caso, se necessário, execute o comando `git checkout develop` e depois `git flow feature start NumeroDaSprint#NumeroDaTask` exemplo: `15#131211` 

Após adicionar suas alterações e realizar o commit, é necessário finalizar a branch temporária que o git flow criou pra você, rodando comando `git flow feature finish`. Ao finalizar uma feature, todas as alterações sobem para a branch **develop**, agora é necessário somente subir para o TFS, executando o comando `git push`

#### Boas práticas:
- O commit sempre deve inicializar com o número da task, seguido por uma breve descrição da atividade desenvolvida, por exemplo: `#131211 - Criando documentação de uso do git flow`
- Sempre execute o comando `git pull` antes   do comando `git push`
- Teste a aplicação após finalizar a feature e realizar o pull (antes mesmo de realizar o push).


### Subindo correções diretamente em produção.
Eventualmente pode ocorrer de um bug chegar ao ambiente de produção, e o ambiente de desenvolvimento ainda não estar preparado para subir. Nesse caso, criamos uma branch de correção, a **Hotfix**. Conforme mostra na imagem do fluxo do git flow, a hotfix deriva da master, que é a nossa branch de produção.
Na hotfix é permitido realizar as alterações de **correção** de bugs **emergenciais** e subir diretamente para a master, basta criar a branch rodando o comando `git flow hotfix NumeroDaSprint#NumeroDaTask`.

Após realizar as correções, adicioná-las e commitá-las, finalize a branch com o comando `git flow hotfix finish`, esse comando subirá as alterações para a master,  sendo apenas necessário realizar o push para o TFS.

#### Boas práticas:
As boas práticas da criação de feature também se aplicam aqui, seguidas destas outras:
* Se necessário, replique as alterações também para o ambiente de desenvolvimento, para que ambos os ambientes estejam atualizados com a nova correção, para isso, após dar pull na master, basta executar os comandos: `git checkout develop` e `git merge master` 
* Acompanhe o build pra garantir que nada ocorra errado.
* Nunca realize o merge da develop com a master manualmente (subir as alterações da develop diretamente na master) .
