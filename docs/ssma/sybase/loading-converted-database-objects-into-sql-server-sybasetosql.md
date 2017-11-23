---
title: Carregando convertidos do banco de dados objetos no SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords: Loading Converted Database Objects
ms.assetid: 4c59256f-99a8-4351-9559-a455813dbd06
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f2ca6ad4ea8c894b3e6100af1a2f6199e089e50f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="loading-converted-database-objects-into-sql-server-sybasetosql"></a>Carregando convertidos do banco de dados objetos no SQL Server (SybaseToSQL)
Depois de converter objetos de banco de dados do Sybase Adaptive Server Enterprise (ASE) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, você pode carregar os objetos de banco de dados resultante em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Você pode ter o SSMA criar os objetos, ou você pode executar scripts nos objetos e executar os scripts por conta própria. Além disso, o SSMA permite atualizar metadados de destino com o conteúdo real de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados do SQL Azure.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Escolha entre Scripts e sincronização  
Se você deseja carregar os objetos de banco de dados convertido em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, sem modificações, você pode ter o SSMA criar ou recriar os objetos de banco de dados diretamente. Esse método é rápido e fácil, mas não permite a personalização do [!INCLUDE[tsql](../../includes/tsql_md.md)] código que define o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou objetos do SQL Azure, diferente de procedimentos armazenados.  
  
Se você quiser modificar o [!INCLUDE[tsql](../../includes/tsql_md.md)] que é usado para criar objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure, ou se você quiser mais controle sobre quando e como os objetos são criados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure, use o SSMA para criar [!INCLUDE[tsql](../../includes/tsql_md.md)] scripts. Você pode, em seguida, modificar esses scripts, crie cada objeto individualmente e até mesmo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure Agent para agendar a criação desses objetos.  
  
## <a name="using-ssma-to-load-objects-into-sql-server-or-sql-azure"></a>Usando o SSMA para carregar objetos no SQL Server ou SQL Azure  
Usar o SSMA para criar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou objetos de banco de dados do SQL Azure, selecione os objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou Gerenciador de metadados do SQL Azure e, em seguida, sincronizar os objetos com [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure, conforme mostrado no procedimento a seguir. Por padrão, se os objetos já existirem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure e se os metadados do SSMA tem algumas alterações locais ou atualizações para a definição desses objetos muito, SSMA irá alterar as definições de objeto em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Você pode alterar o comportamento padrão, editando **configurações de projeto**.  
  
> [!NOTE]  
> Você pode selecionar existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou objetos de banco de dados do SQL Azure que não foram convertidos de bancos de dados ASE. No entanto, esses objetos não serão recriados ou alterados por SSMA.  
  
**Para sincronizar objetos com o SQL Server ou SQL Azure**  
  
1.  Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou Gerenciador de metadados do SQL Azure, expanda a parte superior [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou nó do SQL Azure e, em seguida, expanda **bancos de dados**.  
  
2.  Selecione os objetos a serem processados:  
  
    -   Para sincronizar um banco de dados completo, marque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para sincronizar ou omitir os objetos individuais ou as categorias de objetos, marque ou desmarque a caixa de seleção ao lado do objeto ou a pasta.  
  
3.  Depois de selecionar os objetos a serem processados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou Gerenciador de metadados do SQL Azure, clique com botão direito **bancos de dados**e, em seguida, clique em **sincronizar com o banco de dados**.  
  
    Também é possível sincronizar objetos individuais ou as categorias de objetos clicando duas vezes o objeto ou a pasta pai e, em seguida, clicando em **sincronizar com o banco de dados**.  
  
    Depois disso, o SSMA exibirá o **sincronizar com o banco de dados** caixa de diálogo, onde você pode ver dois grupos de itens. No lado esquerdo, SSMA mostra representados em uma árvore de objetos de banco de dados selecionado. No lado direito, você pode ver uma árvore que representa os mesmos objetos de metadados do SSMA. Você pode expandir a árvore, clique à direita ou esquerda botão ' +'. A direção da sincronização é mostrada na coluna ação colocada entre as duas árvores.  
  
    Pode ser um sinal de ação em três estados:  
  
    -   Uma seta para a esquerda significa que o conteúdo de metadados será salvo no banco de dados (o padrão).  
  
    -   Uma seta à direita significa que o conteúdo do banco de dados substituirão os metadados do SSMA.  
  
    -   Uma conexão cruzada significa que nenhuma ação será tomada.  
  
Clique no sinal de ação para alterar o estado. Sincronização real será executada quando você clicar em **Okey** botão do **sincronizar com o banco de dados** caixa de diálogo.  
  
## <a name="scripting-objects"></a>Objetos de script  
Se você deseja salvar [!INCLUDE[tsql](../../includes/tsql_md.md)] definições de objetos de banco de dados convertido ou se quiser alterar as definições de objeto e executar scripts por conta própria, você pode salvar definições de objeto para o banco de dados convertido [!INCLUDE[tsql](../../includes/tsql_md.md)] scripts.  
  
**Para salvar objetos como scripts**  
  
1.  Depois de selecionar os objetos para salvar um script, clique com botão direito **bancos de dados**e, em seguida, selecione **Salvar como Script**.  
  
    Você pode também gerar um script objetos individuais ou as categorias de objetos clicando duas vezes o objeto ou a pasta que contém, e, em seguida, selecionando **salvar Script**.  
  
2.  No **Salvar como** caixa de diálogo caixa, localize a pasta onde deseja salvar o script, digite um nome de arquivo no **nome de arquivo** caixa e, em seguida, clique em **Okey**.  
  
    O SSMA acrescentará a extensão de nome de arquivo. SQL.  
  
### <a name="modifying-scripts"></a>Modificando Scripts  
Depois que você salvou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou definições de objeto do SQL Azure como um ou mais scripts, você pode usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] para exibir e modificar os scripts.  
  
**Para modificar um script**  
  
1.  Sobre o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **arquivo** , aponte para **abrir**e, em seguida, clique em **arquivo**.  
  
2.  No **abrir** caixa de diálogo, navegue até e selecione o arquivo de script e, em seguida, clique em **Okey**.  
  
3.  Editar e o arquivo de script usando o editor de consulta.  
  
    Para obter mais informações sobre o editor de consultas, consulte "Editor conveniência comandos e recursos" [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
4.  Para salvar o script, no menu Arquivo, selecione **salvar**.  
  
### <a name="running-scripts"></a>Execução de Scripts  
Você pode executar um script ou instruções individuais, em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
**Para executar um script**  
  
1.  Sobre o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **arquivo** , aponte para **abrir**e, em seguida, clique em **arquivo**.  
  
2.  No **abrir** caixa de diálogo, navegue até e selecione o arquivo de script e, em seguida, clique em **Okey**.  
  
3.  Para executar o script completo, pressione a **F5** chave.  
  
4.  Para executar um conjunto de instruções, selecione as instruções na janela do editor de consulta e, em seguida, pressione a **F5** chave.  
  
Para obter mais informações sobre como usar o editor de consultas para executar scripts, consulte "[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] [!INCLUDE[tsql](../../includes/tsql_md.md)] consulta" em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
Você também pode executar scripts de linha de comando usando o **sqlcmd** utilitário e de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] agente. Para obter mais informações sobre **sqlcmd**, consulte "utilitário sqlcmd" [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online. Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent, consulte "automatizando tarefas administrativas ([!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] agente)" em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
## <a name="securing-objects-in-sql-server"></a>Proteção de objetos no SQL Server  
Depois que você carregou os objetos de banco de dados convertido em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], é possível conceder e negar permissões nesses objetos. É uma boa ideia fazer isso antes de migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obter informações sobre como ajudar a proteger objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte "Considerações para bancos de dados e banco de dados de aplicativos de segurança" no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração é [migrando dados do Sybase ASE para o SQL Server / SQL Azure(SybaseToSQL)](http://msdn.microsoft.com/en-us/54a39f5e-9250-4387-a3ae-eae47c799811).  
  
## <a name="see-also"></a>Consulte também  
[Migrando Sybase ASE bancos de dados do SQL Server - banco de dados SQL do Azure &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
