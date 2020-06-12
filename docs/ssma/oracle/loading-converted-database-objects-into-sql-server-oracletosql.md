---
title: Carregando objetos de banco de dados convertidos em SQL Server (OracleToSQL) | Microsoft Docs
description: Saiba como carregar os objetos de banco de dados convertidos do Oracle na instância de SQL Server usando o SSMA para Oracle.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Synchronization, Securing Objects in SQL Server
- Synchronization,Scripting Objects
ms.assetid: a8ae33b2-1883-4785-922b-ea0e31c0b37a
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 69c4d30b3a803cfd5eb8e196f540c33952de3bf5
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293843"
---
# <a name="loading-converted-database-objects-into-sql-server-oracletosql"></a>Carregar objetos de banco de dados convertidos no SQL Server (OracleToSQL)
Depois de converter os esquemas do Oracle para SQL Server, você pode carregar os objetos de banco de dados resultantes em SQL Server. Você pode fazer com que o SSMA crie os objetos, ou pode criar o script dos objetos e executar os scripts por conta própria. Além disso, o SSMA permite que você atualize metadados de destino com o conteúdo real do banco de dados SQL Server.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Escolhendo entre a sincronização e os scripts  
Se você quiser carregar os objetos de banco de dados convertidos em SQL Server sem modificação, poderá fazer com que o SSMA crie ou recrie os objetos de banco de dados diretamente. Esse método é rápido e fácil, mas não permite a personalização do [!INCLUDE[tsql](../../includes/tsql-md.md)] código que define os objetos SQL Server, além dos procedimentos armazenados.  
  
Se você quiser modificar o [!INCLUDE[tsql](../../includes/tsql-md.md)] que é usado para criar objetos ou se quiser mais controle sobre a criação de objetos, use o SSMA para criar scripts. Em seguida, você pode modificar esses scripts, criar cada objeto individualmente e até mesmo usar SQL Server Agent para agendar a criação desses objetos.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Usando o SSMA para sincronizar objetos com SQL Server  
Para usar o SSMA para criar SQL Server objetos de banco de dados, selecione os objetos em SQL Server Gerenciador de metadados e sincronize os objetos com SQL Server, conforme mostrado no procedimento a seguir. Por padrão, se os objetos já existirem no SQL Server, e se os metadados do SSMA forem mais novos do que o objeto no SQL Server, o SSMA alterará as definições de objeto no SQL Server. Você pode alterar o comportamento padrão editando **as configurações do projeto**.  
  
> [!NOTE]  
> Você pode selecionar objetos de banco de dados SQL Server existentes que não foram convertidos de bancos de dados Oracle. No entanto, esses objetos não serão recriados ou alterados pelo SSMA.  
  
**Para sincronizar objetos com SQL Server**  
  
1.  No SQL Server Gerenciador de metadados, expanda o nó SQL Server superior e, em seguida, expanda **bancos de dados**.  
  
2.  Selecione os objetos a serem processados:  
  
    -   Para sincronizar um banco de dados completo, marque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para sincronizar ou omitir objetos individuais ou categorias de objetos, marque ou desmarque a caixa de seleção ao lado do objeto ou da pasta.  
  
3.  Depois de selecionar os objetos a serem processados no Gerenciador de metadados SQL Server, clique com o botão direito do mouse em **bancos**de dados e clique em **sincronizar com o banco de dados**.  
  
    Você também pode sincronizar objetos individuais ou categorias de objetos clicando com o botão direito do mouse no objeto ou em sua pasta pai e clicando em **sincronizar com o banco de dados**.  
  
    Depois disso, o SSMA exibirá a caixa de diálogo **sincronizar com o banco de dados** , onde você poderá ver dois grupos de itens. No lado esquerdo, o SSMA mostra os objetos de banco de dados selecionados representados em uma árvore. No lado direito, você pode ver uma árvore que representa os mesmos objetos em metadados do SSMA. Você pode expandir a árvore clicando no botão à direita ou à esquerda ' + '. A direção da sincronização é mostrada na coluna ação colocada entre as duas árvores.  
  
    Um sinal de ação pode estar em três Estados:  
  
    -   Uma seta para a esquerda significa que o conteúdo dos metadados será salvo no banco de dados (o padrão).  
  
    -   Uma seta para a direita significa que o conteúdo do banco de dados substituirá os metadados do SSMA.  
  
    -   Um sinal cruzado significa que nenhuma ação será executada.  
  
Clique no sinal de ação para alterar o estado. A sincronização real será executada quando você clicar no botão **OK** da caixa de diálogo **sincronizar com Banco de dados** .  
  
## <a name="scripting-objects"></a>Objetos de script  
Para salvar as [!INCLUDE[tsql](../../includes/tsql-md.md)] definições dos objetos de banco de dados convertidos ou alterar as definições de objeto e executar scripts por conta própria, você pode salvar as definições de objeto de banco de dados convertido em [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts.  
  
**Para salvar objetos como scripts**  
  
1.  Depois de selecionar os objetos a serem salvos em um script, clique com o botão direito do mouse em **bancos de dados**e clique em **salvar como script**.  
  
    Você também pode criar scripts de objetos individuais ou categorias de objetos clicando com o botão direito do mouse no objeto ou em sua pasta pai e clicando em **salvar como script**.  
  
2.  Na caixa de diálogo **salvar como** , localize a pasta onde você deseja salvar o script, insira um nome de arquivo na caixa **nome do arquivo** e clique em OK o SSMA acrescentará a extensão de nome de arquivo. Sql.  
  
### <a name="modifying-scripts"></a>Modificando scripts  
Depois de salvar as definições de objeto de SQL Server como um ou mais scripts, você pode usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o para exibir e modificar os scripts.  
  
**Para modificar um script**  
  
1.  No menu [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Arquivo** , aponte para **Abrir**e clique em **Arquivo**.  
  
2.  Na caixa de diálogo **abrir** , selecione o arquivo de script e clique em OK.
  
3.  Edite o arquivo de script usando o editor de consultas.  
  
    Para obter mais informações sobre o editor de consultas, consulte "comandos e recursos de conveniência do editor" em Manuais Online do SQL Server.  
  
4.  Para salvar o script, no menu arquivo, clique em **salvar**.  
  
### <a name="running-scripts"></a>Executando scripts  
Você pode executar um script, ou instruções individuais, no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
**Para executar um script**  
  
1.  No menu [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Arquivo** , aponte para **Abrir**e clique em **Arquivo**.  
  
2.  Na caixa de diálogo **abrir** , selecione o arquivo de script e clique em OK  
  
3.  Para executar o script completo, pressione a tecla **F5** .  
  
4.  Para executar um conjunto de instruções, selecione as instruções na janela do editor de consultas e pressione a tecla **F5** .  
  
Para obter mais informações sobre como usar o editor de consultas para executar scripts, consulte " [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] consultar" em manuais online do SQL Server.  
  
Você também pode executar scripts na linha de comando usando o utilitário **sqlcmd** e do SQL Server Agent. Para obter mais informações sobre o **sqlcmd**, consulte "utilitário sqlcmd" em manuais online do SQL Server. Para obter mais informações sobre SQL Server Agent, consulte "automatizando tarefas administrativas (SQL Server Agent)" em Manuais Online do SQL Server.  
  
## <a name="securing-objects-in-sql-server"></a>Protegendo objetos no SQL Server  
Depois de carregar os objetos de banco de dados convertidos em SQL Server, você pode conceder e negar permissões nesses objetos. É uma boa ideia fazer isso antes de migrar dados para SQL Server. Para obter informações sobre como ajudar a proteger objetos no SQL Server, consulte "considerações de segurança para bancos de dados e aplicativos de banco de dados" em Manuais Online do SQL Server.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa do processo de migração é [migrar dados para o SQL Server](migrating-oracle-data-into-sql-server-oracletosql.md).  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados Oracle para SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
