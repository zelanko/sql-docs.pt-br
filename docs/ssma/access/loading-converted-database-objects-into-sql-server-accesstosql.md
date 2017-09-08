---
title: Carregando convertidos do banco de dados objetos no SQL Server (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Access databases, loading converted objects into SQL Azure
- Access databases, loading converted objects into SQL Server
- data, securing
- loading objects into SQL Azure
- loading objects into SQL Server
- migrating objects into SQL Azure
- migrating objects into SQL Server
- moving objects into SQL Azure
- moving objects into SQL Server
- schemas, loading into SQL Azure
- schemas, loading into SQL Server
- scripting converted objects
- securing data
- SQL Azure, loading objects into
- SQL Server, loading objects into
- synchronizing metadata with SQL Azure
- synchronizing metadata with SQL Server
- uploading objects into SQL Azure
- uploading objects into SQL Server
ms.assetid: 4e854eee-b10c-4f0b-9d9e-d92416e6f2ba
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 5def0c73f1c77a289eb926c4d8ab7691a6d19253
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="loading-converted-database-objects-into-sql-server-accesstosql"></a>Carregando convertidos do banco de dados objetos no SQL Server (AccessToSQL)
Depois de converter objetos de banco de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, você pode carregar os objetos de banco de dados resultante em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Você pode ter o SSMA criar os objetos, ou você pode executar scripts nos objetos e executar os scripts por conta própria. Além disso, o SSMA permite atualizar metadados de destino com o conteúdo real de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados do SQL Azure.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Escolha entre Scripts e sincronização  
Se você deseja carregar os objetos de banco de dados convertido em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, sem modificações, você pode ter o SSMA criar ou recriar os objetos de banco de dados diretamente. Esse método é rápido e fácil, mas não permite a personalização do [!INCLUDE[tsql](../../includes/tsql_md.md)] código que define o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou objetos do SQL Azure, diferente de procedimentos armazenados.  
  
Se você quiser modificar o [!INCLUDE[tsql](../../includes/tsql_md.md)] que é usado para criar objetos, ou se você quiser mais controle sobre a criação de objetos, use o SSMA para criar scripts. Você pode, em seguida, modificar esses scripts, crie cada objeto individualmente e até mesmo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent para agendar a criação desses objetos.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Usando o SSMA para sincronizar objetos com o SQL Server  
Usar o SSMA para criar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou objetos de banco de dados do SQL Azure, selecione os objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou Gerenciador de metadados do SQL Azure e, em seguida, sincronizar os objetos com [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure, conforme mostrado no procedimento a seguir. Por padrão, se os objetos já existirem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure e se os metadados do SSMA tem algumas alterações locais ou atualizações para a definição desses objetos muito, SSMA irá alterar as definições de objeto em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Você pode alterar o comportamento padrão, editando **configurações de projeto**.  
  
> [!NOTE]  
> Você pode selecionar existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou objetos de banco de dados do SQL Azure que não foram convertidos de bancos de dados do Access. No entanto, o SSMA não será recriar ou alterar esses objetos.  
  
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
  
**Para salvar um ou mais objetos em um script**  
  
1.  Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados, expanda o nó superior (o nome do servidor) e, em seguida, expanda **bancos de dados**.  
  
2.  Siga um ou mais destes procedimentos:  
  
    -   Para criar o script de um banco de dados completo, selecione a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para o script ou omita a exibições individuais, expanda o banco de dados, **exibições**e, em seguida, marque ou desmarque a caixa de seleção ao lado do modo de exibição.  
  
    -   Para o script ou omita tabelas individuais, expanda o banco de dados, **tabelas**e, em seguida, marque ou desmarque a caixa de seleção ao lado da tabela.  
  
    -   Para o script ou omita índices individuais de uma tabela, expanda a tabela, **índices**e, em seguida, marque ou desmarque o índice.  
  
3.  Clique com botão direito **bancos de dados** e selecione **Salvar como Script**.  
  
    Você também pode gerar o script de objetos individuais. Para criar o script de um objeto, independentemente de quais objetos são selecionados, clique no objeto e selecione **Salvar como Script**.  
  
4.  No **Salvar como** caixa de diálogo caixa, localize a pasta onde deseja salvar o script, digite um nome de arquivo no **nome de arquivo** caixa e, em seguida, clique em **Okey**.  
  
    O SSMA acrescentará a extensão de nome de arquivo. SQL.  
  
### <a name="modifying-scripts"></a>Modificando Scripts  
Depois que você salvou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou definições de objeto do SQL Azure como um script, você pode usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] para modificar o script.  
  
**Para modificar um script**  
  
1.  Sobre o [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] **arquivo** , aponte para **abrir**e, em seguida, clique em **arquivo**.  
  
2.  No **abrir** caixa de diálogo, localize e selecione o arquivo de script e, em seguida, clique em **Okey**.  
  
3.  Edite o arquivo de script usando o editor de consulta.  
  
    Para obter mais informações sobre o editor de consultas, consulte "Editor conveniência comandos e recursos" [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
4.  Para salvar o script, no menu Arquivo, selecione **salvar**.  
  
### <a name="running-scripts"></a>Execução de Scripts  
Você pode executar um script ou instruções individuais, em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
**Para executar um script**  
  
1.  Sobre o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **arquivo** , aponte para **abrir** e, em seguida, clique em **arquivo**.  
  
2.  No **abrir** caixa de diálogo, localize e selecione o arquivo de script e, em seguida, clique em **Okey**.  
  
3.  Para executar o script completo, pressione a **F5** chave.  
  
4.  Para executar um conjunto de instruções, selecione as instruções na janela do editor de consulta e, em seguida, pressione a **F5** chave.  
  
Para obter mais informações sobre como usar o editor de consultas para executar scripts, consulte "[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] [!INCLUDE[tsql](../../includes/tsql_md.md)] consulta" em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
Você também pode executar scripts de linha de comando usando o **sqlcmd** utilitário e de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] agente. Para obter mais informações sobre **sqlcmd**, consulte "utilitário sqlcmd" [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online. Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent, consulte "automatizar tarefas administrativas ([!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] agente)" em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
## <a name="securing-objects-in-sql-server"></a>Proteção de objetos no SQL Server  
Depois que você carregou os objetos de banco de dados convertido em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], é possível conceder e negar permissões nesses objetos. É uma boa ideia fazer isso antes de migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obter informações sobre como ajudar a proteger objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte "Considerações para bancos de dados e banco de dados de aplicativos de segurança" no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração é [migrar dados para o SQL Server](http://msdn.microsoft.com/en-us/f3b18af7-1af0-499d-a00d-a0af94895625).  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  

