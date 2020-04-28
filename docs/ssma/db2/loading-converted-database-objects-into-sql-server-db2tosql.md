---
title: Carregando objetos de banco de dados convertidos em SQL Server (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 7af5566094c9cc4c40ba2aa33f27e79bae1c7445
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68141032"
---
# <a name="loading-converted-database-objects-into-sql-server-db2tosql"></a>Carregando objetos de banco de dados convertidos em SQL Server (DB2ToSQL)
Depois de converter os esquemas do DB2 no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode carregar os objetos de banco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dados resultantes no. Você pode fazer com que o SSMA crie os objetos, ou pode criar o script dos objetos e executar os scripts por conta própria. Além disso, o SSMA permite que você atualize os metadados de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o conteúdo real do banco de dados.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Escolhendo entre a sincronização e os scripts  
Se você quiser carregar os objetos de banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] convertidos em sem modificação, você pode fazer com que o SSMA crie ou recrie os objetos de banco de dados diretamente. Esse método é rápido e fácil, mas não permite a [!INCLUDE[tsql](../../includes/tsql-md.md)] personalização do código que define os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos, além dos procedimentos armazenados.  
  
Se você quiser modificar o que [!INCLUDE[tsql](../../includes/tsql-md.md)] é usado para criar objetos ou se quiser mais controle sobre a criação de objetos, use o SSMA para criar scripts. Em seguida, você pode modificar esses scripts, criar cada objeto individualmente e até [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mesmo usar o Agent para agendar a criação desses objetos.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Usando o SSMA para sincronizar objetos com SQL Server  
Para usar o SSMA para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criar objetos de banco de dados, selecione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os objetos no Gerenciador de metadados e sincronize os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]objetos com, conforme mostrado no procedimento a seguir. Por padrão, se os objetos já existirem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]no, e se os metadados do SSMA forem mais recentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]que o objeto no, o SSMA alterará as definições de objeto no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode alterar o comportamento padrão editando **as configurações do projeto**.  
  
> [!NOTE]  
> Você pode selecionar objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de banco de dados existentes que não foram convertidos de bancos de dados DB2. No entanto, esses objetos não serão recriados ou alterados pelo SSMA.  
  
**Para sincronizar objetos com SQL Server**  
  
1.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, expanda [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o nó superior e depois expanda **bancos de dados**.  
  
2.  Selecione os objetos a serem processados:  
  
    -   Para sincronizar um banco de dados completo, marque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para sincronizar ou omitir objetos individuais ou categorias de objetos, marque ou desmarque a caixa de seleção ao lado do objeto ou da pasta.  
  
3.  Depois de selecionar os objetos a serem processados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Gerenciador de metadados, clique com o botão direito do mouse em **bancos**de dados e clique em **sincronizar com o banco de dados**.  
  
    Você também pode sincronizar objetos individuais ou categorias de objetos clicando com o botão direito do mouse no objeto ou em sua pasta pai e clicando em **sincronizar com o banco de dados**.  
  
    Depois disso, o SSMA exibirá a caixa de diálogo **sincronizar com o banco de dados** , onde você poderá ver dois grupos de itens. No lado esquerdo, o SSMA mostra os objetos de banco de dados selecionados representados em uma árvore. No lado direito, você pode ver uma árvore que representa os mesmos objetos em metadados do SSMA. Você pode expandir a árvore clicando no botão à direita ou à esquerda ' + '. A direção da sincronização é mostrada na coluna ação colocada entre as duas árvores.  
  
    Um sinal de ação pode estar em três Estados:  
  
    -   Uma seta para a esquerda significa que o conteúdo dos metadados será salvo no banco de dados (o padrão).  
  
    -   Uma seta para a direita significa que o conteúdo do banco de dados substituirá os metadados do SSMA.  
  
    -   Um sinal cruzado significa que nenhuma ação será executada.  
  
Clique no sinal de ação para alterar o estado. A sincronização real será executada quando você clicar no botão **OK** da caixa de diálogo **sincronizar com Banco de dados** .  
  
## <a name="scripting-objects"></a>Objetos de script  
Para salvar [!INCLUDE[tsql](../../includes/tsql-md.md)] as definições dos objetos de banco de dados convertidos ou alterar as definições de objeto e executar scripts por conta própria, você pode salvar as [!INCLUDE[tsql](../../includes/tsql-md.md)] definições de objeto de banco de dados convertido em scripts.  
  
**Para salvar objetos como scripts**  
  
1.  Depois de selecionar os objetos a serem salvos em um script, clique com o botão direito do mouse em **bancos de dados**e clique em **salvar como script**.  
  
    Você também pode criar scripts de objetos individuais ou categorias de objetos clicando com o botão direito do mouse no objeto ou em sua pasta pai e clicando em **salvar como script**.  
  
2.  Na caixa de diálogo **salvar como** , localize a pasta onde você deseja salvar o script, insira um nome de arquivo na caixa **nome do arquivo** e, em [!INCLUDE[clickOK](../../includes/clickok-md.md)]seguida,. O SSMA acrescentará a extensão de nome de arquivo. Sql.  
  
### <a name="modifying-scripts"></a>Modificando scripts  
Depois de salvar as definições [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de objeto como um ou mais scripts, você pode usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o para exibir e modificar os scripts.  
  
**Para modificar um script**  
  
1.  No menu [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Arquivo** , aponte para **Abrir**e clique em **Arquivo**.  
  
2.  Na caixa de diálogo **abrir** , selecione o arquivo de script e clique em OK.
  
3.  Edite o arquivo de script usando o editor de consultas.  
  
    Para obter mais informações sobre o editor de consultas, consulte "comandos e recursos de conveniência [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do editor" nos manuais online do.  
  
4.  Para salvar o script, no menu arquivo, clique em **salvar**.  
  
### <a name="running-scripts"></a>Executando scripts  
Você pode executar um script, ou instruções individuais, no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
**Para executar um script**  
  
1.  No menu [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Arquivo** , aponte para **Abrir**e clique em **Arquivo**.  
  
2.  Na caixa de diálogo **abrir** , selecione o arquivo de script e, em seguida,[!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  Para executar o script completo, pressione a tecla **F5** .  
  
4.  Para executar um conjunto de instruções, selecione as instruções na janela do editor de consultas e pressione a tecla **F5** .  
  
Para obter mais informações sobre como usar o editor de consultas para executar scripts, consulte [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] "consultar" [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nos manuais online do.  
  
Você também pode executar scripts na linha de comando usando o utilitário **sqlcmd** e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente. Para obter mais informações sobre o **sqlcmd**, consulte o "utilitário [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sqlcmd" nos manuais online do. Para obter mais informações [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sobre o Agent, consulte "automatizando tarefas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administrativas (agente) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] " nos manuais online do.  
  
## <a name="securing-objects-in-sql-server"></a>Protegendo objetos no SQL Server  
Depois de carregar os objetos de banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]convertidos no, você pode conceder e negar permissões nesses objetos. É uma boa ideia fazer isso antes de migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o. Para obter informações sobre como ajudar a proteger objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]no, consulte "considerações de segurança para bancos de dados e aplicativos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados" nos manuais online do.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa do processo de migração é [migrar dados do DB2 para o SQL Server](https://msdn.microsoft.com/86cbd39f-6dac-409a-9ce1-7dd54403f84b).  
  
## <a name="see-also"></a>Consulte Também  
[Migrar dados do DB2 para o SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
