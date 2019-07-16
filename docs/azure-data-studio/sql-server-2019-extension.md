---
title: Extensão do SQL Server 2019 (visualização)
titleSuffix: Azure Data Studio
description: Extensão de 2019 Preview do SQL Server para o Studio de dados do Azure
ms.custom: seodec18
ms.date: 06/25/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 9b25fd044b94e21151b687d428c469a12d8c8a5d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959212"
---
# <a name="sql-server-2019-extension-preview"></a>Extensão do SQL Server 2019 (visualização)

A extensão de 2019 do SQL Server (versão prévia) fornece suporte de visualização para novos recursos e ferramentas de envio suportados [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. Isso inclui suporte para visualização [clusters do SQL Server 2019 big data](../big-data-cluster/big-data-cluster-overview.md), um integrada [experiência de notebook](../big-data-cluster/notebooks-guidance.md)e um PolyBase [assistente Create External Table](../relational-databases/polybase/data-virtualization.md?toc=/sql/toc/toc.json).

## <a name="install-the-sql-server-2019-extension-preview"></a>Instalar a extensão do SQL Server 2019 (visualização)

Para instalar a extensão de 2019 do SQL Server (versão prévia), baixe e instale o arquivo. VSIX associado.

1. Baixe o arquivo. VSIX de extensão (visualização) do SQL Server 2019 para um diretório local:

   |Plataforma|Download|Data de liberação|Versão
   |:---|:---|:---|:---|
   |Windows|[.vsix](https://go.microsoft.com/fwlink/?linkid=2097803)|25 de junho de 2019 |0.14.1
   |macOS|[.vsix](https://go.microsoft.com/fwlink/?linkid=2097802)|25 de junho de 2019 |0.14.1
   |Linux|[.vsix](https://go.microsoft.com/fwlink/?linkid=2097801)|25 de junho de 2019 |0.14.1

1. No estúdio de dados do Azure, escolha **instalar a extensão do pacote VSIX** da **arquivo** menu e selecione o arquivo. VSIX baixado.

1. Escolher **Sim** quando for solicitado a confirmar a instalação e aguarde a notificação de que a instalação foi bem-sucedida.

1. Selecione **Recarregar** para habilitar a extensão (necessário somente na primeira vez que você instalar uma extensão).

1. Após o recarregamento, a extensão instalará as dependências. Você pode ver o progresso na janela de saída, e pode levar vários minutos.

1. Após as dependências de concluir a instalação, feche e reabra o estúdio de dados do Azure. O **cluster de big data do SQL Server** tipo de conexão não está disponível até que você reinicie o estúdio de dados do Azure.

## <a name="changes-in-release-0141"></a>Alterações na versão 0.14.1
* Suporte para o suporte de fonte de dados CTP 3.1

## <a name="changes-in-release-0121"></a>Alterações na versão 0.12.1

* O **cluster de big data do SQL Server** tipo de conexão foi removido nesta versão. Todas as funcionalidades disponíveis anteriormente a conexão de cluster de big data do SQL Server agora está disponível na conexão do SQL Server.
* HDFS navegação pode ser encontrado sob o **serviços de dados** pasta
* Para notebooks do PySpark e outros kernels de grandes dados funcionam quando conectado a instância mestre do SQL Server no seu cluster de big data do SQL Server.
* Crie Assistente de tabela externa:
  * Suporte para a criação de tabela externa usando a fonte de dados externa existente.
  * Melhorias de desempenho entre o assistente.
  * Melhoria no tratamento de nomes de objeto com caracteres especiais. Em alguns casos, esses causou o falha do Assistente
  * Melhorias de confiabilidade para a página mapeamento de objeto.
  * Sistema removidos bancos de dados - ': DWConfiguration', 'DWDiagnostics', 'DWQueue' - na lista suspensa de bancos de dados.
  * Suporte para definir o nome do objeto de formato de arquivo externo na **criar tabela externa de arquivos CSV** assistente.
  * Adicionado um botão de atualização para a primeira página do **criar tabela externa de arquivos CSV** assistente.

## <a name="release-notes-v0110"></a>Notas de versão (v0.11.0)

* Suporte de Jupyter Notebook, oferecem suporte especificamente para os kernels Spark e Python3, foi movido no estúdio de dados do Azure. Esta extensão não é mais necessária para usar os blocos de anotações.
* Várias correções de bugs nos assistentes de dados externos:
  * Mapeamentos de tipo Oracle foram atualizados para corresponder as alterações enviadas no SQL Server de 2019 CTP 2.3.
  * Corrigido um problema em que novos esquemas digitadas no controle de mapeamento de tabela foram perdidas.
  * Corrigido um problema em que a verificação de um nó de banco de dados nos mapeamentos de tabela não resultou em todas as tabelas e modos de exibição que está sendo verificados.


## <a name="release-notes-v0102"></a>Notas de versão (v0.10.2)
### <a name="sql-server-2019-support"></a>Suporte do SQL Server de 2019
Suporte para SQL Server 2019 foi atualizado. Sobre como se conectar a um Cluster grande de dados do SQL Server da instância uma nova _serviços de dados_ pasta será exibido na árvore do Gerenciador. Isso tem pontos de partida para ações como abrir um novo Notebook em relação a conexão, enviando trabalhos do Spark e trabalhar com o HDFS. Observe que para algumas ações, como _criar dados externos_ ao longo de um arquivo/pasta do HDFS, o _visualização do SQL Server de 2019_ extensão deve ser instalada.

### <a name="notebook-support"></a>Suporte do bloco de anotações
Fizemos atualizações importantes para a interface do usuário do bloco de anotações nesta versão. Nosso foco foi tornando mais fácil de ler blocos de anotações que são compartilhados com você. Isso significava a remoção de todas as caixas em torno de células de descrever, a menos que selecionado ou colocado em cima, adição de suporte de focalização fácil ações de nível de célula sem a necessidade selecionar uma célula e esclarecer o estado de execução, adicionando a contagem de execução, um animada _Parar execução_ botão e muito mais. Também adicionamos atalhos de teclado para _novo Notebook_ (`Ctrl+Shift+N`), _executar célula_ (`F5`), _nova célula de código_ (`Ctrl+Shift+C`),  _Nova célula de texto_ (`Ctrl+Shift+T`). Futuramente que serão nosso objetivo é ter todas as ações de chave possam ser iniciadas pelo atalho então informe-nos saber o que está perdendo!

Outras melhorias e correções incluem:
* O _versão prévia do SQL Server de 2019_ extensão agora usa de prompts para escolher um diretório de instalação de dependências do Python. Ele também não inclui mais Python no `.vsix file`, reduzindo o tamanho geral da extensão. As dependências de Python são necessários para suportar os kernels Spark e Python3, para que instalar essa extensão é necessária para usá-los.
* Foi adicionado suporte para iniciar um novo bloco de anotações na linha de comando. Inicie com os argumentos `--command=notebook.command.new --server=myservername` deve abrir um novo bloco de anotações e conectar a esse servidor.
* Correções de desempenho para os blocos de anotações com um comprimento de código grande em células. Se as células de código são mais de 250 linhas tiverem uma barra de rolagem adicionada.
* Maior suporte a arquivo ipynb. Agora há suporte para a versão 3 ou posterior. Observe que ao salvar arquivos será atualizada para a versão 4 ou superior.
* O `notebook.enabled` configuração de usuário tiver sido removido agora que internos no bloco de anotações do Visualizador é estável
* Tema de alto contraste agora é compatível com um número de correções para o layout do objeto nesse caso.
* Corrigido 3680 # onde saídas mostraram, às vezes, um número de `,,,` caracteres incorretamente
* Editor de #3602 fixa desaparece para células depois de sair do studio de dados do azure
* Foi adicionado suporte para usar os modos de exibição de grade para o `application/vnd.dataresource+json` tipo MIME de saída. Isso significa que muitos blocos de anotações que usam esse (por exemplo, definindo `pd.options.display.html.table_schema` em um bloco de anotações do Python) terão mais agradável saídas tabulares fixa #3959 Azure dados Studio tenta desligue o servidor de notebook duas vezes depois de fechar o bloco de anotações

#### <a name="known-issues"></a>Problemas conhecidos
* Como abrir um bloco de anotações aparecerá a caixa de diálogo Instalação do python. Cancelando a instalação resultará nos Kernels e anexar para listas suspensas mostrando não esperado de valores. A solução alternativa é concluir a instalação do Python.
* Quando um bloco de anotações é aberto com um kernel sem suporte, os kernels e _anexar a_ listas suspensas fará com que a Azure Data Studio pare de responder. Você precisará fechar o Studio de dados do Azure e verifique se você usar um kernel com suporte (Python3, Spark | R, o Spark | Scala, PySpark, PySpark3)
* Link da interface do usuário do Spark Falha ao usar PySpark3 ou outros kernels Spark contra o ponto de extremidade do SQL Server. Como alternativa, clique na interface do usuário do Spark no painel de ou conectar-se usando o tipo de conexão do cluster de big data do SQL Server, pois isso terá o hiperlink correto de interface do usuário do Spark

### <a name="extensibility-improvements"></a>Aprimoramentos de extensibilidade
Uma série de aprimoramentos que ajudam a extensores foram adicionada nesta versão
* Um novo `ObjectExplorerNodeProvider` API permite que extensões contribuir com pastas sob o SQL Server ou outros nós de Conexão. Isso é como o `Data Services` nó é adicionado em instâncias do SQL Server 2019, mas pode ser usado para adicionar o monitoramento ou outras pastas facilmente na interface do usuário.
* Dois novos valores de chave de contexto estão disponíveis para ajudar a mostrar/ocultar contribuições para o painel.
  * `mssql:iscluster` Indica se este é um Cluster de dados grande do SQL Server de 2019
  * `mssql:servermajorversion` tem a versão do servidor (15 para o SQL Server 2019, 14 para SQL Server 2017 e assim por diante). Isso pode ajudar se recursos devem apenas ser mostrados para o SQL Server 2017 ou maior, por exemplo.


## <a name="release-notes-v080"></a>Notas de versão (v0.8.0)
*Blocos de anotações*:
* Adicionando células antes / depois existente agora há suporte para células, clicando no botão de célula "Mais ações"
* **Adicionar nova Conexão** opção foi adicionada para as conexões na lista suspensa "Anexar a"
* Um **reinstalar as dependências do bloco de anotações** comando foi adicionado para ajudar com as atualizações de pacote do Python e resolver casos em que o install foi parado parada no meio fechando o aplicativo. Isso pode ser executado a partir da paleta de comandos (use `Ctrl/Cmd+Shift+P` e digite `Reinstall Notebook Dependencies`)
* O pacote do python PROSA foi atualizado para a versão 1.1.0 e inclui uma série de correções de bugs. Use o **reinstalar as dependências do bloco de anotações** comando para este pacote de atualização
* Um **limpar saída** agora há suporte para o comando clicando o **mais ações** botão da célula
* Corrigido o seguinte problemas relatados pelo cliente:
  * Sessão de notebook não pôde iniciar no Windows devido a problemas de caminho
  * Não foi possível iniciar o bloco de anotações na pasta raiz de uma unidade, como C:\ ou D:\
  * [#2820](https://github.com/Microsoft/azuredatastudio/issues/2820) não é possível editar os blocos de anotações criados a partir de anúncios no VS Code
  * Link da interface do usuário do Spark agora funciona ao executar um kernel do Spark
  * Renomeado de "Gerenciado por pacotes" para "Instalar pacotes"

*Criar dados externos*:

* Mensagens de erro podem ser copiados e foram separadas em um modo de exibição resumido e detalhado para o mais fácil
* Layout de interface do usuário aprimorada e muito mais confiabilidade e tratamento de erros
* Corrigido o seguinte problemas relatados pelo cliente:
  * Tabelas com mapeamentos de coluna inválido são mostradas como desabilitados e um aviso explica o erro

## <a name="release-notes-v072"></a>Notas de versão (v0.7.2)
* Gerenciador de recursos do Azure agora é interno ao estúdio de dados do Azure e foi removido dessa extensão. Agradecemos seus comentários sobre isso!
* Desempenho aprimorado de blocos de anotações com o número de células de Markdown.
* Células de código de tamanho automático no bloco de anotações. Isso ainda tem um tamanho mínimo com base na barra de ferramentas de célula.
* Notifique o usuário ao instalar as dependências do bloco de anotações. No Windows em particular isso pode levar muito tempo, portanto, as notificações são agora exibidas no modo de exibição de tarefas.
* Suporte ao reinstalar as dependências do bloco de anotações. Isso é útil se o usuário fechou anteriormente Studio do Azure Data parcialmente por meio de instalação.
* Cancelando a execução de célula no bloco de anotações de suporte.
* Confiabilidade aprimorada ao usar o Assistente para criar dados externos, especificamente quando conexão ocorrem erros.
* Bloquear o uso do Assistente para criar dados externos se o PolyBase não está habilitado ou está em execução no servidor de destino.
* Verificar ortografia e correções relacionadas ao SQL Server 2019 e criar dados externos de nomenclatura.
* Removido um grande número de erros do console de depuração do estúdio de dados do Azure.

##  <a name="sql-server-2019-big-data-cluster-support"></a>Suporte de Cluster de Big Data do SQL Server de 2019

* Clique em **Adicionar Conexão** na *Pesquisador de objetos* e escolha **cluster de big data do SQL Server** como o tipo de conexão.

   > [!TIP]
   > Se você não vir as **cluster de big data do SQL Server** tipo de conexão, reinicie o Studio de dados do Azure.

* Insira o nome do host ou endereço IP do ponto de extremidade do cluster plus o nome de usuário e senha usadas para se conectar.
* Opcionalmente, incluir um nome de exibição amigável na **nome** campo.
* Clique em **Connect** e, em seguida, você pode iniciar tarefas comuns do painel, navegue **HDFS** no Pesquisador de objetos e tarefas a serem executadas no contexto de lá.
* Para enviar um trabalho do Spark no cluster, clique com botão direito no nó do servidor no *Pesquisador de objetos* e escolha **enviar trabalho do Spark** para abrir a caixa de diálogo de envio.
* Para abrir um bloco de anotações, consulte a próxima seção.

Para obter detalhes, consulte [Clusters de Big Data](../big-data-cluster/big-data-cluster-overview.md).


## <a name="azure-data-studio-notebooks"></a>Blocos de anotações do Studio dados do Azure

* Abra um bloco de anotações em uma das seguintes maneiras:
  * Abra um novo bloco de anotações do *paleta de comandos*.
  * Abra a árvore do Pesquisador de objetos do HDFS para um cluster de big data 2019 do SQL Server e qualquer um:
    * Clique com o botão direito no nó do servidor e escolha **novo Jupyter Notebook**.
    * Clique com botão direito em um arquivo CSV e escolha **analisar no bloco de anotações**.
  * Abrir um arquivo ipynb existente do **arquivo** explorer de menu ou arquivo *(arquivos. ipynb devem ser atualizados para a versão 4 ou superior para carregar corretamente)*
* Escolha um kernel. Para a execução do bloco de anotações local, escolha o Python 3. Para a execução remota, escolha o PySpark ou Spark | Scala.
* Escolha um ponto de extremidade do cluster de big data do SQL Server para se conectar ao se executar remotamente (isso não é necessário para o desenvolvimento local com o Python 3).
* Adicione as células de código ou markdown por meio de botões no cabeçalho de bloco de anotações. Remova as células com o ícone de Lixeira à esquerda de cada célula.
* Executar as células com o botão Reproduzir para células de código e ativar/desativar a edição de markdown e visualizar com o ícone de olho

## <a name="polybase-create-external-table-wizard"></a>O PolyBase criar Assistente de tabela externa

* De uma instância do SQL Server 2019 a *criar Assistente de tabela externa* pode ser aberto de três maneiras:
  * Clique com botão direito em um servidor, escolha **Manage**, clique na guia para o SQL Server 2019 (visualização) e escolha **Create External Table**.
  * Com uma instância do SQL Server 2019 selecionada na *Pesquisador de objetos*, abrirá *Assistente externos para criar* via o *paleta de comandos*.
  * Clique com botão direito em um banco de dados SQL Server 2019 *Pesquisador de objetos* e escolha **Create External Table**.
* Nesta versão da extensão, tabelas externas podem ser criadas para acessar tabelas remotas do SQL Server e Oracle.

  > [!NOTE]
  > Embora a funcionalidade de tabela externa é um recurso de 2019 SQL, o SQL Server remoto pode estar executando uma versão anterior do SQL Server.

* Escolha se você estiver acessando o SQL Server ou Oracle na primeira página do assistente e continua.
* Você será solicitado a criar uma chave mestra de banco de dados se um já não tiver sido criado (senhas de complexidade insuficiente serão bloqueadas).
* Criar uma conexão de fonte de dados e nomeado de credencial para o servidor remoto.
* Escolha quais objetos para mapear para sua nova tabela externa.
* Escolher **Gerar Script** ou **criar** para concluir o assistente.
* Após a criação da tabela externa, ela aparece imediatamente na árvore de objetos do banco de dados no qual ele foi criado.


## <a name="known-issues"></a>Problemas Conhecidos

* Se a senha não é salvo durante a criação de uma conexão, algumas ações como enviar trabalho do Spark podem não ter êxito.
* Blocos de anotações ipynb existentes devem ser atualizados para a versão 4 ou superior para carregar conteúdo no visualizador.
* Executando o **reinstalar as dependências do bloco de anotações** comando pode mostrar 2 tarefas na exibição de tarefas, um deles falha. Isso não causa falha na instalação
* Escolhendo **adicionar nova Conexão** em um bloco de anotações e clicando em ' Cancelar ' fará com que **Selecionar Conexão** a serem mostrados, mesmo se você já estava conectado.
