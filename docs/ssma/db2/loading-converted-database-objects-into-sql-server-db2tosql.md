---
title: Carregando convertidos do banco de dados objetos no SQL Server (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 21962c8849204db6f3e5f114b6f8f86994d53b35
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53215492"
---
# <a name="loading-converted-database-objects-into-sql-server-db2tosql"></a>Carregando convertidos do banco de dados objetos no SQL Server (DB2ToSQL)
Depois de converter esquemas do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode carregar os objetos de banco de dados resultante em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode ter o SSMA criar os objetos, ou você pode gerar script dos objetos e executar os scripts por conta própria. Além disso, o SSMA permite atualizar os metadados de destino com o conteúdo real da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Escolhendo entre sincronização e Scripts  
Se você deseja carregar os objetos de banco de dados convertido em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem modificação, você pode ter o SSMA criar ou recriar os objetos de banco de dados diretamente. Esse método é rápido e fácil, mas não permite a personalização do [!INCLUDE[tsql](../../includes/tsql-md.md)] código que define o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos, diferentes procedimentos armazenados.  
  
Se você quiser modificar o [!INCLUDE[tsql](../../includes/tsql-md.md)] que é usado para criar objetos, ou se você quiser mais controle sobre a criação de objetos, use o SSMA para criar scripts. Você pode, em seguida, modificar esses scripts, criar cada objeto individualmente e até mesmo usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para agendar a criação desses objetos.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Usando o SSMA para sincronizar objetos com o SQL Server  
Usar o SSMA para criar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos de banco de dados, selecione os objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados e, em seguida, sincronizar os objetos com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], conforme mostrado no procedimento a seguir. Por padrão, se os objetos já existirem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e se os metadados do SSMA for mais recente do que o objeto na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o SSMA irá alterar as definições de objeto em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode alterar o comportamento padrão, editando **configurações do projeto**.  
  
> [!NOTE]  
> Você pode selecionar existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos que não foram convertidos de bancos de dados do DB2 do banco de dados. No entanto, esses objetos não serão recriados ou alterados por SSMA.  
  
**Para sincronizar objetos com o SQL Server**  
  
1.  Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, expanda a parte superior [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nó e, em seguida, expanda **bancos de dados**.  
  
2.  Selecione os objetos a serem processados:  
  
    -   Para sincronizar um banco de dados completo, marque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para sincronizar ou omitir objetos individuais ou categorias de objetos, marque ou desmarque a caixa de seleção ao lado do objeto ou pasta.  
  
3.  Depois de selecionar os objetos a serem processados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, clique com botão direito **bancos de dados**e, em seguida, clique em **sincronizar com o banco de dados**.  
  
    Você também pode sincronizar objetos individuais ou as categorias de objetos clicando com botão direito do objeto ou a pasta pai e, em seguida, clicando em **sincronizar com o banco de dados**.  
  
    Depois disso, o SSMA exibirá os **sincronizar com o banco de dados** caixa de diálogo, onde você pode ver dois grupos de itens. No lado esquerdo, o SSMA mostra representados em uma árvore de objetos de banco de dados selecionado. No lado direito, você pode ver uma árvore que representa os mesmos objetos nos metadados do SSMA. Você pode expandir a árvore clicando-se à direita ou esquerda botão ' +'. A direção da sincronização é mostrada na coluna ação colocado entre as duas árvores.  
  
    Um sinal de ação pode estar em três estados:  
  
    -   Uma seta para a esquerda significa que o conteúdo de metadados será salvo no banco de dados (o padrão).  
  
    -   Uma seta para a direita significa que o conteúdo do banco de dados substituirão os metadados do SSMA.  
  
    -   Um sinal cruzado significa que nenhuma ação será tomada.  
  
Clique no sinal de ação para alterar o estado. Sincronização real será executada quando você clica **Okey** botão da **sincronizar com o banco de dados** caixa de diálogo.  
  
## <a name="scripting-objects"></a>Objetos de script  
Para economizar [!INCLUDE[tsql](../../includes/tsql-md.md)] as definições dos objetos de banco de dados convertido, ou alterar as definições de objeto e executar scripts por conta própria, você pode salvar o banco de dados convertido definições de objeto para [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts.  
  
**Para salvar objetos como scripts**  
  
1.  Depois de selecionar os objetos para salvar um script, clique com botão direito **bancos de dados**e, em seguida, clique em **Salvar como Script**.  
  
    Você pode também gerar um script objetos individuais ou as categorias de objetos clicando com botão direito do objeto ou a pasta pai e, em seguida, clicando em **Salvar como Script**.  
  
2.  No **Salvar como** diálogo caixa, localize a pasta onde você deseja salvar o script, digite um nome de arquivo na **nome do arquivo** caixa e, em seguida, [!INCLUDE[clickOK](../../includes/clickok-md.md)]. O SSMA acrescentará a extensão de nome de arquivo. SQL.  
  
### <a name="modifying-scripts"></a>Modificando Scripts  
Depois de salvar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definições de objeto como um ou mais scripts, você pode usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para exibir e modificar os scripts.  
  
**Para modificar um script**  
  
1.  Sobre o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **arquivo** , aponte para **abra**e, em seguida, clique em **arquivo**.  
  
2.  No **abrir** caixa de diálogo, selecione o arquivo de script e, em seguida, clique em Okey.
  
3.  Edite o arquivo de script usando o editor de consultas.  
  
    Para obter mais informações sobre o editor de consultas, consulte "Editor de comandos e recursos de conveniência" no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.  
  
4.  Para salvar o script no arquivo menu, clique em **salvar**.  
  
### <a name="running-scripts"></a>Execução de Scripts  
Você pode executar um script ou instruções individuais, em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
**Para executar um script**  
  
1.  Sobre o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **arquivo** , aponte para **abra**e, em seguida, clique em **arquivo**.  
  
2.  No **abrir** caixa de diálogo, selecione o arquivo de script e, em seguida, [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  Para executar o script completo, pressione a **F5** chave.  
  
4.  Para executar um conjunto de instruções, selecione as instruções na janela do editor de consulta e, em seguida, pressione a **F5** chave.  
  
Para obter mais informações sobre como usar o editor de consultas para executar scripts, consulte " [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta" no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.  
  
Você também pode executar scripts da linha de comando usando o **sqlcmd** utilitário e para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente. Para obter mais informações sobre **sqlcmd**, consulte "utilitário sqlcmd" em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online. Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, consulte "automatizar tarefas administrativas ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente)" em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.  
  
## <a name="securing-objects-in-sql-server"></a>Protegendo os objetos no SQL Server  
Depois que você carregou os objetos de banco de dados convertido em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível conceder e negar permissões nesses objetos. É uma boa ideia fazer isso antes de migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter informações sobre como ajudar a proteger objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte "Considerações para bancos de dados e banco de dados de aplicativos de segurança" em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.  
  
## <a name="next-step"></a>Próxima etapa  
É a próxima etapa no processo de migração [migrando dados do DB2 para o SQL Server](https://msdn.microsoft.com/86cbd39f-6dac-409a-9ce1-7dd54403f84b).  
  
## <a name="see-also"></a>Consulte também  
[Migrando dados do DB2 para o SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
