---
title: Extensão do SQL Server 2019 (versão prévia)
titleSuffix: Azure Data Studio
description: Extensão da Versão Prévia do SQL Server 2019 para Azure Data Studio
ms.custom: seodec18
ms.date: 06/25/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 9b25fd044b94e21151b687d428c469a12d8c8a5d
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959212"
---
# <a name="sql-server-2019-extension-preview"></a>Extensão do SQL Server 2019 (versão prévia)

A extensão do SQL Server 2019 (versão prévia) dá suporte em versão prévia a novos recursos e ferramentas fornecidos em suporte do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. Isso inclui suporte em versão prévia a [clusters de Big Data do SQL Server 2019](../big-data-cluster/big-data-cluster-overview.md), uma [experiência de notebook](../big-data-cluster/notebooks-guidance.md) integrada e um assistente [Criar Tabela Externa](../relational-databases/polybase/data-virtualization.md?toc=/sql/toc/toc.json) do PolyBase.

## <a name="install-the-sql-server-2019-extension-preview"></a>Instalar a extensão do SQL Server 2019 (versão prévia)

Para instalar a extensão do SQL Server 2019 (versão prévia), baixe e instale o arquivo .vsix associado.

1. Baixe o arquivo .vsix da extensão do SQL Server 2019 (versão prévia) para um diretório local:

   |Plataforma|Download|Data de liberação|Versão
   |:---|:---|:---|:---|
   |Windows|[.vsix](https://go.microsoft.com/fwlink/?linkid=2097803)|25 de junho de 2019 |0.14.1
   |macOS|[.vsix](https://go.microsoft.com/fwlink/?linkid=2097802)|25 de junho de 2019 |0.14.1
   |Linux|[.vsix](https://go.microsoft.com/fwlink/?linkid=2097801)|25 de junho de 2019 |0.14.1

1. No Azure Data Studio, escolha **Instalar extensão do pacote VSIX** no menu **Arquivo** e selecione o arquivo .vsix baixado.

1. Escolha **Sim** quando for solicitado que você confirme a instalação e aguarde a notificação de que a instalação foi bem-sucedida.

1. Selecione **Recarregar** para habilitar a extensão (necessário apenas na primeira vez que você instala uma extensão).

1. Após o recarregamento, a extensão instalará as dependências. Você pode ver o andamento na janela de Saída. O processo pode levar vários minutos.

1. Após as dependências serem instaladas, feche e reabra Azure Data Studio. O tipo de conexão **Cluster de Big Data do SQL Server** ficará disponível somente após você reiniciar o Azure Data Studio.

## <a name="changes-in-release-0141"></a>Alterações na versão 0.14.1
* Suporte para a fonte de dados CTP 3.1

## <a name="changes-in-release-0121"></a>Alterações na versão 0.12.1

* O tipo de conexão de **Cluster de Big Data do SQL Server** foi removido desta versão. Agora, toda a funcionalidade disponível anteriormente na conexão do cluster de Big Data do SQL Server está disponível na conexão do SQL Server.
* A navegação do HDFS pode ser encontrada na pasta **Serviços de Dados**
* Para notebooks, o PySpark e outros kernels de Big Data funcionam quando conectados à instância mestre do SQL Server em seu cluster de Big Data do SQL Server.
* Assistente Criar Tabela Externa:
  * Suporte para criação de Tabela Externa usando a Fonte de Dados Externa existente.
  * Melhorias de desempenho no assistente.
  * Tratamento aprimorado de nomes de objetos com caracteres especiais. Em alguns casos, eles causavam falhas do assistente
  * Melhorias de confiabilidade na página Mapeamento de Objeto.
  * Remoção dos bancos de dados do sistema – 'DWConfiguration', 'DWDiagnostics', 'DWQueue' – da lista suspensa de bancos de dados.
  * Suporte para definir o nome do objeto de Formato de Arquivo Externo no assistente **Criar Tabela Externa de Arquivos CSV**.
  * Adição de um botão de atualização à primeira página do assistente **Criar Tabela Externa de Arquivos CSV**.

## <a name="release-notes-v0110"></a>Notas sobre a versão (v0.11.0)

* O suporte para Jupyter Notebook, especificamente o suporte para kernels do Python3 e do Spark, foi movido para o Azure Data Studio. Deixou de ser necessário ter essa extensão para usar Notebooks.
* Várias correções de bugs nos assistentes de Dados Externos:
  * Os mapeamentos de tipo do Oracle foram atualizados para corresponder às alterações fornecidas no SQL Server 2019 CTP 2.3.
  * Corrigido um problema em que novos esquemas digitados nos controles de mapeamento da tabela eram perdidos.
  * Corrigido um problema em que a verificação de um nó de Banco de dados nos mapeamentos de tabela não resultava na verificação de todas as tabelas e exibições.


## <a name="release-notes-v0102"></a>Notas sobre a versão (v0.10.2)
### <a name="sql-server-2019-support"></a>Suporte ao SQL Server 2019
O suporte para o SQL Server 2019 foi atualizado. Ao se conectar a uma instância do Cluster de Big Data do SQL Server, uma nova pasta _Serviços de Dados_ será exibida na árvore do Explorer. Ela tem pontos de inicialização para ações como abrir um novo Notebook para a conexão, enviar trabalhos do Spark e trabalhar com o HDFS. Observe que, para algumas ações como _Criar Dados Externos_ em um arquivo/pasta do HDFS, a extensão de _Versão Prévia do SQL Server 2019_ precisa estar instalada.

### <a name="notebook-support"></a>Suporte para Notebook
Fizemos atualizações significativas na interface do usuário do Notebook nesta versão. Nosso foco foi facilitar a leitura de Notebooks compartilhados com você. Isso significava remover todas as caixas de contorno em torno das células, a menos que estivessem selecionadas ou focalizadas, adicionar suporte de foco para facilitar ações no nível da célula sem precisar selecionar a célula e esclarecer o estado da execução adicionando uma contagem de execução, um botão animado _parar execução_ , entre outros. Também adicionamos atalhos de teclado para _Novo Notebook_ (`Ctrl+Shift+N`), _Executar Célula_ (`F5`), _Nova Célula de Código_ (`Ctrl+Shift+C`), _Nova Célula de Texto_ (`Ctrl+Shift+T`). Futuramente, faremos com que todas as ações importantes sejam iniciadas por atalho, sendo assim, diga-nos de quais ações você sente falta!

Outras melhorias e correções incluem:
* Agora, a extensão de _Versão Prévia do SQL Server 2019_ solicita que os usuários escolham um diretório de instalação para as dependências de Python. Além disso, ela não inclui mais o Python no `.vsix file`, reduzindo o tamanho geral da extensão. As dependências do Python são necessárias para dar suporte a kernels do Spark e do Python3, portanto, é necessário instalar essa extensão para usá-las.
* Foi adicionado suporte para iniciar um novo notebook na linha de comando. A inicialização com os argumentos `--command=notebook.command.new --server=myservername` deve abrir um novo notebook e conectar a este servidor.
* Correções de desempenho para notebooks com código de tamanho grande nas células. Se tiverem mais de 250 linhas, as células de código terão uma barra de rolagem adicionada.
* Melhoria do suporte para arquivos .ipynb. Agora, a versão 3 ou superior tem suporte. Observe que, ao salvar os arquivos, será feita a atualização para a versão 4 ou superior.
* A configuração do usuário `notebook.enabled` foi removida agora que o visualizador interno do Notebook é estável
* Agora, o tema Alto Contraste tem suporte, com diversas correções no layout do objeto neste caso.
* Correção de 3680, em que as saídas às vezes mostravam um número de caracteres `,,,` incorretamente
* Correção de 3602, em que o Editor desaparece para as células depois de navegar para fora do Azure Data Studio
* Adicionado suporte para usar exibições de Grade para o tipo MIME da saída `application/vnd.dataresource+json`. Isso significa que muitos Notebooks que o usam (por exemplo, definindo `pd.options.display.html.table_schema` em um notebook Python) terão saídas de tabela melhores da Correção de 3959, em que o Azure Data Studio tentar desligar o servidor do notebook duas vezes após fechar o notebook

#### <a name="known-issues"></a>Problemas conhecidos
* Ao abrir um Notebook, a caixa de diálogo Instalar Python será exibida. Cancelar essa instalação fará com que as listas suspensas Kernels e Anexar ao não exibam os valores esperados. A solução alternativa é concluir a instalação do Python.
* Quando um notebook é aberto com um kernel sem suporte, as listas suspensas Kernels e _Anexar ao_ farão com que o Azure Data Studio trave. Você precisará fechar o Azure Data Studio e usar um kernel com suporte (Python3, Spark | R, Spark | Scala, PySpark, PySpark3)
* O link da interface do usuário do Spark falha ao usar o PySpark3 ou outros kernels do Spark no ponto de extremidade do SQL Server. Como solução alternativa, clique na interface do usuário do Spark no painel ou conecte-se usando o tipo de conexão de cluster de Big Data do SQL Server, pois ele terá o hiperlink correto da interface do usuário do Spark

### <a name="extensibility-improvements"></a>Melhorias de extensibilidade
Nesta versão, foram adicionadas várias melhorias que ajudam os extensores
* Uma nova API do `ObjectExplorerNodeProvider` permite que as extensões contribuam com pastas no SQL Server ou em outros nós de Conexão. É assim que o nó `Data Services` é adicionado em instâncias SQL Server 2019, mas poderia ser usado para adicionar Monitoramento ou outras pastas facilmente à interface do usuário.
* Dois novos valores de chave de contexto estão disponíveis para ajudar a mostrar/ocultar contribuições para o painel.
  * `mssql:iscluster` indica se este é um Cluster de Big Data do SQL Server 2019
  * `mssql:servermajorversion` tem a versão do servidor (15 para o SQL Server 2019, 14 para o SQL Server 2017 e assim por diante). Isso pode ajudar caso os recursos só devam ser mostrados para o SQL Server 2017 ou superior, por exemplo.


## <a name="release-notes-v080"></a>Notas sobre a versão (v0.8.0)
*Notebooks*:
* Agora, há suporte para adição de células antes/depois das células existentes clicando no botão "Mais Ações" da célula
* A opção **Adicionar Nova Conexão** foi adicionada às conexões na lista suspensa "Anexar ao"
* Foi adicionado um comando **Reinstalar Dependências do Notebook** para auxiliar nas atualizações de pacote do Python e resolver casos em que a instalação é interrompida ao fechar o aplicativo. Ele pode ser executado na paleta de comandos (use `Ctrl/Cmd+Shift+P` e digite `Reinstall Notebook Dependencies`)
* O pacote PROSE do Python foi atualizado para 1.1.0 e inclui várias correções de bugs. Use o comando **Reinstalar Dependências do Notebook** para atualizar este pacote
* Agora, há suporte para um comando **Limpar Saída** clicando no botão **Mais Ações** da célula
* Corrigidos os seguintes problemas relatados pelos clientes:
  * Não era possível iniciar a sessão do Notebook no Windows devido a problemas de caminho
  * Não era possível iniciar o Notebook na pasta raiz de uma unidade, como C:\ ou D:\
  * [#2820](https://github.com/Microsoft/azuredatastudio/issues/2820) Não é possível editar notebooks criados usando o ADS no VS Code
  * Agora, o link da interface do usuário do Spark funciona ao executar um kernel do Spark
  * "Pacotes Gerenciados" foi renomeado para "Instalar Pacotes"

*Criar Dados Externos*:

* As mensagens de erro podem ser copiadas e foram separadas em um resumo e uma exibição detalhada para facilitar
* Melhoria do layout da interface do usuário e melhoria significativa da confiabilidade e do tratamento de erro
* Corrigidos os seguintes problemas relatados pelos clientes:
  * Tabelas com mapeamentos de coluna inválidos são mostradas como desabilitadas e um aviso explica o erro

## <a name="release-notes-v072"></a>Notas sobre a versão (v0.7.2)
* Agora, o Azure Resource Explorer foi incorporado ao Azure Data Studio e foi removido desta extensão. Agradecemos por seus comentários sobre isto!
* Melhoria no desempenho de notebooks com muitas células de Markdown.
* Dimensionamento automático de células de código no Notebook. Isso ainda tem um tamanho mínimo baseado na barra de ferramentas da célula.
* Notificar o usuário ao instalar dependências do Notebook. No Windows em particular, isso pode levar muito tempo, de modo que agora as notificações são mostradas no modo de exibição de Tarefas.
* Suporte à reinstalação de dependências do Notebook. Isso é útil se o usuário fechou o Azure Data Studio anteriormente durante a instalação.
* Suporte para cancelamento da execução da célula no Notebook.
* Melhoria na confiabilidade ao usar o assistente Criar Dados Externos, especificamente quando erros de conexão ocorrem.
* Bloquear o uso do assistente Criar Dados Externos se o PolyBase não estiver habilitado ou em execução no servidor de destino.
* Correção de ortografia e nomenclatura relacionadas ao SQL Server 2019 e ao assistente Criar Dados Externos.
* Remoção de um grande número de erros do console de depuração do Azure Data Studio.

##  <a name="sql-server-2019-big-data-cluster-support"></a>Suporte para Cluster de Big Data do SQL Server 2019

* Clique em **Adicionar Conexão** no *Pesquisador de Objetos* e escolha **Cluster de Big Data do SQL Server** como tipo de conexão.

   > [!TIP]
   > Se não vir o tipo de conexão **Cluster de Big Data do SQL Server**, reinicie o Azure Data Studio.

* Insira o nome do host ou o endereço IP do ponto de extremidade do cluster mais o nome de usuário e a senha usados para se conectar.
* Opcionalmente, inclua um nome de exibição amigável no campo **Nome**.
* Clique em **Conectar** e você poderá iniciar tarefas comuns no painel, navegar no **HDFS** no Pesquisador de Objetos e executar tarefas em contexto nele.
* Para enviar um trabalho do Spark ao cluster, clique com o botão direito do mouse no nó de servidor no *Pesquisador de Objetos* e escolha **Enviar Trabalho do Spark** para abrir a caixa de diálogo de envio.
* Para abrir um Notebook, confira a próxima seção.

Para obter detalhes, confira [Clusters de Big Data](../big-data-cluster/big-data-cluster-overview.md).


## <a name="azure-data-studio-notebooks"></a>Notebooks do Azure Data Studio

* Abra um notebook de um dos seguintes modos:
  * Abra um novo notebook na *Paleta de Comandos*.
  * Abra a árvore do Pesquisador de Objetos do HDFS para um cluster de Big Data do SQL Server 2019 e:
    * Clique com o botão direito do mouse no nó de servidor e escolha **Novo Jupyter Notebook**.
    * Clique com o botão direito do mouse em um arquivo CSV e escolha **Analisar no Notebook**.
  * Abra um arquivo .ipynb existente no menu **Arquivo** ou no Explorador de Arquivos *(arquivos .ipynb devem ser atualizados para a versão 4 ou superior para serem carregados corretamente)*
* Escolha um kernel. Para execução local do notebook, escolha Python 3. Para execução remota, escolha PySpark ou Spark | Scala.
* Escolha um ponto de extremidade do cluster de Big Data do SQL Server para se conectar se estiver executando remotamente (isso não é necessário para o desenvolvimento local com Python 3).
* Adicione células de código ou de Markdown usando os botões no cabeçalho do notebook. Remova as células com o ícone de lixeira à esquerda de cada célula.
* Execute as células usando o botão reproduzir para células de código e alterne entre a exibição de edição e de versão prévia de Markdown usando o ícone de olho

## <a name="polybase-create-external-table-wizard"></a>Assistente Criar Tabela Externa do PolyBase

* Em uma instância do SQL Server 2019, o *Assistente Criar Tabela Externa* pode ser aberto de três maneiras:
  * Clique com o botão direito do mouse em um servidor, escolha **Gerenciar**, clique na guia do SQL Server 2019 (versão prévia) e escolha **Criar Tabela Externa**.
  * Com uma instância do SQL Server 2019 selecionada no *Pesquisador de Objetos*, exiba o *Assistente Criar Externo* usando a *Paleta de Comandos*.
  * Clique com o botão direito do mouse em um banco de dados do SQL Server 2019 no *Pesquisador de Objetos* e escolha **Criar Tabela Externa**.
* Nesta versão da extensão, tabelas externas podem ser criadas para acessar tabelas remotas do SQL Server e do Oracle.

  > [!NOTE]
  > Embora a funcionalidade de Tabela Externa seja um recurso do SQL 2019, o SQL Server remoto pode estar executando uma versão anterior do SQL Server.

* Escolha se você está acessando o SQL Server ou o Oracle na primeira página do assistente e continue.
* Será solicitado que você crie uma Chave Mestra do Banco de Dados se uma ainda não tiver sido criada (senhas com complexidade insuficiente serão bloqueadas).
* Crie uma conexão de fonte de dados e uma credencial nomeada para o servidor remoto.
* Escolha quais objetos você deseja mapear para sua nova tabela externa.
* Escolha **Gerar Script** ou **Criar** para concluir o assistente.
* Após a criação da tabela externa, ela aparecerá imediatamente na árvore de objetos do banco de dados em que foi criada.


## <a name="known-issues"></a>Problemas conhecidos

* Se a senha não for salva durante a criação de uma conexão, algumas ações, como enviar o trabalho do Spark, poderão não ter sucesso.
* Notebooks .ipynb existentes devem ser atualizados para a versão 4 ou superior para carregar conteúdo no visualizador.
* Executar o comando **Reinstalar Dependências do Notebook** pode mostrar duas tarefas no modo de exibição de tarefas, uma das quais falha. Isso não causa a falha da instalação
* Escolher **Adicionar Nova Conexão** em um Notebook e clicar em cancelar fará com que **Selecionar Conexão** seja exibido, mesmo que você já esteja conectado.
