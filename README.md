# Sistema de Controle de Versão com Git e GitHub: Guia Prático e Fluxo de Trabalho Profissional

## 1. Por que Git? O problema que ele resolve

O Git é um sistema de controle de versão distribuído criado por Linus Torvalds em 2005. Sua principal função é rastrear cada mudança realizada no código-fonte, o que permite reverter erros, colaborar em equipe e manter um histórico completo do desenvolvimento. A adoção do Git resolve problemas graves do fluxo de trabalho tradicional (onde desenvolvedores costumam duplicar arquivos manualmente, gerando nomes confusos como `projeto_v2_final_ESSE.js` ou `projeto_copia_backup.js`).

O valor do Git se apoia em quatro pilares fundamentais:

* **Viagem no tempo:** Cada commit funciona como um *snapshot* (fotografia) do estado do código. Isso permite retornar a qualquer momento anterior do projeto, inclusive para aquela versão de três semanas atrás que funcionava perfeitamente.
* **Colaboração segura:** Múltiplos desenvolvedores podem trabalhar simultaneamente em partes diferentes do mesmo projeto sem o risco de sobrescrever o trabalho alheio. O uso de branches isola o trabalho de cada um, eliminando a necessidade de compartilhar códigos por arquivos ZIP, o que frequentemente causava a perda de dados.
* **Branches e experimentos:** É possível criar uma ramificação (branch) para testar uma nova ideia. Se o experimento funcionar, é feito o *merge* (fusão) com o código principal; se não funcionar, a branch é descartada sem afetar a estabilidade do sistema. Isso elimina o hábito de comentar blocos de código apenas para "guardá-los" ou o medo de testar novas abordagens.
* **Rastreabilidade:** Através do comando `git log`, é possível identificar quem mudou o quê, quando e por qual motivo (por meio da mensagem de commit). Esse histórico detalhado é essencial para processos de *debugging* (correção de erros) e *code review* (revisão de código), evitando que bugs entrem em produção sem que se saiba quando ou por quem o código foi alterado.

## 2. Comandos Git Essenciais e o Fluxo Básico

O ciclo fundamental do Git consiste em modificar arquivos, adicioná-los à área de preparação e salvar o estado atual. Para entender esse fluxo, é necessário compreender as três áreas do Git:

1. **Working Directory:** O diretório de trabalho onde ficam os seus arquivos atuais.
2. **Staging Area:** A área de preparação onde as modificações são selecionadas.
3. **Repository (.git):** O repositório definitivo onde os *snapshots* são salvos.

O fluxo de comandos para manipular essas áreas e gerenciar o repositório local inclui:

* `git init`: Inicializa um repositório Git na pasta atual, criando a pasta oculta `.git`.  
    ![git init](/prints/git%20init.png)
* `git add arquivo.js`: Adiciona um arquivo específico à *staging area*.
    ![git add](/prints/git_add.png)
* `git status`: Mostra o estado atual dos arquivos, indicando quais foram modificados, quais estão na *staging area* e quais ainda não estão sendo rastreados.  
    ![git status](/prints/git_status.png)
* `git rm --cached <arquivo>`: remove o arquivo da **staging area** e retorna para **work area**.  
    ![git rm --cached](/prints/git_rm_--cached.png)
* `git add .`: Adiciona todos os arquivos modificados e novos da pasta atual à *staging area*.  
    ![git add .](/prints/git_add_dot.png)
* `git commit -m 'mensagem'`: Salva o *snapshot* do código no repositório com uma mensagem descritiva.  
    ![git commit -m "msg"](/prints/git_commit_-m.png)
* `git log`: é usado para visualizar o histórico de commits de um repositório. Por padrão, sem nenhum argumento, lista os commits em ordem cronológica inversa, exibindo o hash único (SHA-1), o autor, a data e a mensagem do commit  
    ![git log](/prints/git_log.png)
* `git log --oneline`: Lista os commits realizados em um formato compacto, exibindo apenas o hash e a mensagem descritiva.
* `git diff`: Mostra as diferenças que ainda não foram adicionadas à *staging area* em relação ao último commit.
* `git restore arquivo.js`: Desfaz as modificações que ainda não foram commitadas em um arquivo específico.
* `git restore --staged arquivo`: Remove um arquivo da *staging area*, desfazendo a ação do comando `git add`.
* ❗ Se houver algum arquivo com espações em branco no nome, usar barra invertida antes do espaço ou escrever o nome do arquivo dentro de aspas duplas.  
    `PS C:\Users\felip\Desktop\aula-git> git rm --cached "prints/git init.png"`  
    `PS C:\Users\felip\Desktop\aula-git> git rm --cached prints/git\ init.png`

A VSCode possui uma interface gráfica de controle de código-fonte. Nela também é possível realizar controlar o versionamento de forma mais intuitiva, sem usar o terminal.  
![versionamento-vscode](/prints/interface-versionamento.png)  

## 3. GitHub: Publicar seu Repositório na Nuvem

O GitHub é uma plataforma de hospedagem para repositórios Git que expande as capacidades locais, permitindo colaboração, revisão de código (*code review*), gerenciamento de problemas (*issues*) e automação de testes e deploys (CI/CD). Ele atua como o portfólio do desenvolvedor e é o padrão da indústria para o trabalho em equipe.

O processo de integração com o GitHub envolve as seguintes etapas:

### Criar o repositório no GitHub

O processo se inicia na plataforma através do caminho `github.com -> New repository`. Deve-se definir um nome (por exemplo, `aulla-git-github`) e configurá-lo como **Público**. Como o projeto já foi iniciado localmente, deve-se criá-lo **sem README**.

### Chave SSH (Autenticação)

Para realizar a autenticação segura entre a máquina local e o GitHub, utiliza-se chaves SSH através dos comandos:

```bash
ssh-keygen -t ed25519 -C 'email@vc.com'

```

Após gerar a chave, deve-se copiar o conteúdo do arquivo público localizado em `~/.ssh/id_ed25519.pub`, acessar as configurações do GitHub (`Settings -> SSH Keys -> New`) e colá-lo lá. Para testar a conexão, utiliza-se o comando:

```bash
ssh -T git@github.com

```

### Configurar Remote e Push

Para vincular o repositório local ao servidor remoto e enviar os arquivos, utilizam-se os comandos:

* `git remote add origin URL`: Vincula o repositório local à URL do GitHub.
* `git branch -M main`: Define o nome da branch principal como `main`.
* `git push -u origin main`: Envia os commits locais para a branch `main` do servidor remoto. O parâmetro `-u` configura a origem padrão; após a primeira execução, basta digitar apenas `git push`.
* `git remote -v`: Permite verificar se os endereços remotos foram configurados corretamente.

![atualizando repositorio remoto](/prints/git_remote_branch_push.png)

### Clone e Pull

Para trabalhar com repositórios já existentes na nuvem, utilizam-se:

* `git clone URL`: Baixa um repositório remoto completo para a máquina local.
* `git pull`: Atualiza o repositório local trazendo e mesclando as alterações do servidor remoto.
* `git fetch`: Baixa as novidades do repositório remoto, mas sem mesclá-las com o código local imediatamente.
* `git pull origin main`: Executa a atualização local apontando explicitamente para a branch `main` remota.

## 4. GitFlow: Branches e Workflow Profissional

O GitFlow é um modelo de gerenciamento de ramificações (*branching*) profissional projetado para organizar o trabalho em equipe. Criado por Vincent Driessen em 2010, ele define regras estritas sobre o papel de cada branch em projetos que possuem ciclos de lançamento (*releases*) bem definidos.

### Funcionamento das Branches e Resolução de Conflitos

Uma branch no Git funciona de forma leve, agindo apenas como um ponteiro para um commit. Criá-las é um processo instantâneo e sem custo de desempenho, permitindo alternar entre múltiplos contextos em segundos.

No terminal, a interação com as branches ocorre da seguinte forma:

* Para listar as branches existentes e identificar em qual você está (marcada com um asterisco), utiliza-se o comando `git branch`.

![git branch](/prints/git_branch.png)

* Para criar uma ramificação para o desenvolvimento de uma funcionalidade, usa-se `git branch feature/login`.
* Para alternar para a branch criada, utiliza-se `git checkout feature/login`. Existe um comando de atalho que cria e alterna para a nova branch simultaneamente: `git checkout -b feature/login`.

![git checkout -b](/prints/git_checkout_-b.png)

* Para retornar à ramificação principal, usa-se `git checkout main`.
* Para unir as mudanças de uma funcionalidade concluída à branch principal, utiliza-se o comando `git merge feature/login` a partir da branch de destino. O Git pode realizar um merge do tipo *Fast-forward* (quando não há divergências no histórico, exibindo mensagens como `Updating abc123..def456`) ou um merge do tipo *ort* (quando há ramificações paralelas).
* Para deletar uma branch local que já foi integrada, utiliza-se `git branch -d feature/login`.

Caso duas pessoas alterem as mesmas linhas do mesmo arquivo, ocorrerá um **conflito**. Para resolvê-lo no terminal, o desenvolvedor deve:

1. Editar manualmente o arquivo que apresenta o conflito, escolhendo o código correto.
2. Adicionar o arquivo corrigido com o comando `git add arquivo`.
3. Concluir o processo com um novo commit através de `git commit`.

### Estrutura de Branches no GitFlow

O modelo profissional do GitFlow é composto por cinco tipos de branches principais:

* **main:** Armazena o código que está rodando em **produção**. É uma branch altamente protegida que só recebe merges vindos das branches de `hotfix` e `release`. Cada merge realizado na `main` representa uma nova versão estável do software entregue ao cliente.
* **develop:** Centraliza a **integração contínua** do projeto. Todas as funcionalidades concluídas e testadas convergem para cá. Ela serve como base de preparação para as próximas versões de lançamento.
* **feature/*:** Ramificações criadas especificamente para o desenvolvimento de uma funcionalidade isolada (ex: `feature/login`, `feature/carrinho`). Elas são criadas sempre a partir da branch `develop` e retornam para ela quando concluídas.
* **release/*:** Branches dedicadas à preparação de um novo deploy no ambiente de produção, onde são realizados os ajustes de bugs finais. Quando a versão está homologada e pronta, a branch de release sofre um merge tanto na `main` quanto na `develop`.
* **hotfix/*:** Ramificações destinadas a correções urgentes diretamente no código que está em produção. Elas são criadas a partir da branch `main` e, assim que o erro é solucionado, o código corrigido é integrado tanto na `main` quanto na `develop`.

## 5. Pull Request e Ferramentas no VS Code

O Pull Request (PR) é o mecanismo utilizado em plataformas como o GitHub para gerenciar a revisão e a integração de novos códigos de forma segura e auditável.

### Fluxo de Trabalho com Pull Request

O ciclo de desenvolvimento colaborativo segue os passos listados abaixo:

1. Cria-se uma nova branch para a funcionalidade: `git checkout -b feature/minha-feature`
2. O desenvolvedor realiza as modificações e faz os commits necessários na branch de feature.
3. A branch local é enviada para o servidor remoto: `git push origin feature/minha-feature`
4. Na interface do GitHub, abre-se um **Pull Request**.
5. Um revisor avalia o código enviado, faz comentários e, estando tudo correto, faz a aprovação.
6. É realizado o **Merge** do PR diretamente para a branch `main` no GitHub.
7. Localmente, o desenvolvedor retorna à branch principal e puxa as atualizações integradas: `git pull origin main`
8. A branch local de feature, já obsoleta, é excluída: `git branch -d feature/minha-feature`

### Extensões Recomendadas para o VS Code

Para facilitar a gestão do Git diretamente no ambiente de desenvolvimento, destacam-se duas ferramentas:

* **GitLens:** Exibe o recurso de *blame* linha por linha no editor de código, mostrando instantaneamente quem editou aquela linha e quando o fez. Também disponibiliza o histórico completo do arquivo, ferramentas de comparação visual (*diff*) e um explorador de branches.
* **Git Graph:** Apresenta uma visualização gráfica e interativa do histórico de commits do projeto. Permite criar, deletar, alternar (*checkout*) e unir (*merge*) branches de forma inteiramente visual.

### Arquivos Ignorados: O arquivo `.gitignore`

Para evitar que arquivos desnecessários, pesados ou contendo dados sensíveis sejam enviados para o repositório na nuvem, utiliza-se um arquivo especial chamado `.gitignore`. Itens essenciais que devem constar nessa lista incluem:

* `node_modules/`: Pastas que contêm as dependências do projeto (visto que podem ser recriadas localmente rodando o comando `npm install`).
* `.env`: Arquivos que guardam variáveis de ambiente, configurações locais e senhas confidenciais.
* `DS_Store`: Arquivos de sistema gerados automaticamente pelo macOS.
* `dist/`: Diretórios que contêm os arquivos resultantes do processo de compilação ou do build final de produção.
