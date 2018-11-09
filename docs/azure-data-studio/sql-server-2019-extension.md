---
title: Extensão de dados Studio SQL Server 2019 do Azure (visualização) | Microsoft Docs
description: Extensão de 2019 Preview do SQL Server para o Studio de dados do Azure
ms.custom: tools|sos
ms.date: 11/06/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2ce04a8f41ec466980bd13d3d032660696e50870
ms.sourcegitcommit: a2be75158491535c9a59583c51890e3457dc75d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51269809"
---
# <a name="sql-server-2019-extension-preview"></a>Extensão do SQL Server 2019 (visualização)

A extensão de 2019 do SQL Server (versão prévia) fornece suporte de visualização para novos recursos e ferramentas de envio suportados [!INCLUDE [sql-server-2019](..\includes\sssqlv15-md.md)]. Isso inclui suporte para visualização [clusters do SQL Server 2019 big data](../big-data-cluster/big-data-cluster-overview.md), um integrada [experiência de notebook](../big-data-cluster/notebooks-guidance.md), um PolyBase [assistente Create External Table](../relational-databases/polybase/data-virtualization.md?toc=%2fsql%2fbig-data-cluster%2ftoc.json)e [Azure Resource Explorer](azure-resource-explorer.md).

## <a name="install-the-sql-server-2019-extension-preview"></a>Instalar a extensão do SQL Server 2019 (visualização)

Para instalar a extensão de 2019 do SQL Server (versão prévia), baixe e instale o arquivo. VSIX associado.

1. Baixe o arquivo. VSIX de extensão (visualização) do SQL Server 2019 para um diretório local:

   |Plataforma|Download|Data de liberação|Versão
   |:---|:---|:---|:---|
   |Windows|[. VSIX](https://go.microsoft.com/fwlink/?linkid=2038184)|6 de novembro de 2018 |0.8.0
   |macOS|[. VSIX](https://go.microsoft.com/fwlink/?linkid=2038178)|6 de novembro de 2018 |0.8.0
   |Linux|[. VSIX](https://go.microsoft.com/fwlink/?linkid=2038246)|6 de novembro de 2018 |0.8.0

1. No estúdio de dados do Azure, escolha **instalar a extensão do pacote VSIX** da **arquivo** menu e selecione o arquivo. VSIX baixado.

1. Escolher **Sim** quando for solicitado a confirmar a instalação e aguarde a notificação de que a instalação foi bem-sucedida.

1. Selecione **recarregar** para habilitar a extensão (necessário somente na primeira vez que você instalar uma extensão).

1. Após o recarregamento, a extensão instalará as dependências. Você pode ver o progresso na janela de saída, e pode levar vários minutos.

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


## <a name="known-issues"></a>Problemas conhecidos

* Se a senha não é salvo durante a criação de uma conexão, algumas ações como enviar trabalho do Spark podem não ter êxito.
* Blocos de anotações ipynb existentes devem ser atualizados para a versão 4 ou superior para carregar conteúdo no visualizador.
* Executando o **reinstalar as dependências do bloco de anotações** comando pode mostrar 2 tarefas na exibição de tarefas, um deles falha. Isso não causa falha na instalação
* Escolhendo **adicionar nova Conexão** em um bloco de anotações e clicando em ' Cancelar ' fará com que **Selecionar Conexão** a serem mostrados, mesmo se você já estava conectado.