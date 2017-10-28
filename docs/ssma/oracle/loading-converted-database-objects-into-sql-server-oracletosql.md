---
title: Carregando convertidos do banco de dados objetos no SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Synchronization, Securing Objects in SQL Server
- Synchronization,Scripting Objects
ms.assetid: a8ae33b2-1883-4785-922b-ea0e31c0b37a
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6fd5616c61af419d5d2ff3134177ae296b317d57
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="loading-converted-database-objects-into-sql-server-oracletosql"></a>Carregando convertidos do banco de dados objetos no SQL Server (OracleToSQL)
Depois de converter esquemas Oracle para o SQL Server, você pode carregar os objetos de banco de dados resultante no SQL Server. Você pode ter o SSMA criar os objetos, ou você pode executar scripts nos objetos e executar os scripts por conta própria. Além disso, o SSMA permite atualizar os metadados de destino com o conteúdo real do banco de dados do SQL Server.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Escolha entre Scripts e sincronização  
Se você deseja carregar os objetos de banco de dados convertido no SQL Server sem modificação, você pode ter o SSMA criar ou recriar os objetos de banco de dados diretamente. Que método é rápido e fácil, mas não permite a personalização do [!INCLUDE[tsql](../../includes/tsql_md.md)] código que define os objetos do SQL Server, diferente de procedimentos armazenados.  
  
Se você quiser modificar o [!INCLUDE[tsql](../../includes/tsql_md.md)] que é usado para criar objetos, ou se você quiser mais controle sobre a criação de objetos, use o SSMA para criar scripts. Você pode modificar esses scripts, crie cada objeto individualmente e até usar o SQL Server Agent para agendar a criação desses objetos.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Usando o SSMA para sincronizar objetos com o SQL Server  
Para usar o SSMA para criar objetos de banco de dados do SQL Server, selecione os objetos no Pesquisador de metadados do SQL Server e, em seguida, sincronizar os objetos com o SQL Server, conforme mostrado no procedimento a seguir. Por padrão, se os objetos já existem no SQL Server, e se os metadados do SSMA for mais recente que o objeto no SQL Server, o SSMA irá alterar as definições de objeto no SQL Server. Você pode alterar o comportamento padrão, editando **configurações de projeto**.  
  
> [!NOTE]  
> Você pode selecionar objetos de banco de dados do SQL Server existentes que não foram convertidos de bancos de dados Oracle. No entanto, esses objetos não serão recriados ou alterados por SSMA.  
  
**Para sincronizar objetos com o SQL Server**  
  
1.  No Gerenciador de metadados do SQL Server, expanda o nó superior do SQL Server e, em seguida, expanda **bancos de dados**.  
  
2.  Selecione os objetos a serem processados:  
  
    -   Para sincronizar um banco de dados completo, marque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para sincronizar ou omitir os objetos individuais ou as categorias de objetos, marque ou desmarque a caixa de seleção ao lado do objeto ou a pasta.  
  
3.  Depois de selecionar os objetos a serem processados no Gerenciador de metadados do SQL Server, clique com botão direito **bancos de dados**e, em seguida, clique em **sincronizar com o banco de dados**.  
  
    Também é possível sincronizar objetos individuais ou as categorias de objetos clicando duas vezes o objeto ou a pasta pai e, em seguida, clicando em **sincronizar com o banco de dados**.  
  
    Depois disso, o SSMA exibirá o **sincronizar com o banco de dados** caixa de diálogo, onde você pode ver dois grupos de itens. No lado esquerdo, SSMA mostra representados em uma árvore de objetos de banco de dados selecionado. No lado direito, você pode ver uma árvore que representa os mesmos objetos de metadados do SSMA. Você pode expandir a árvore, clique à direita ou esquerda botão ' +'. A direção da sincronização é mostrada na coluna ação colocada entre as duas árvores.  
  
    Pode ser um sinal de ação em três estados:  
  
    -   Uma seta para a esquerda significa que o conteúdo de metadados será salvo no banco de dados (o padrão).  
  
    -   Uma seta à direita significa que o conteúdo do banco de dados substituirão os metadados do SSMA.  
  
    -   Uma conexão cruzada significa que nenhuma ação será tomada.  
  
Clique no sinal de ação para alterar o estado. Sincronização real será executada quando você clicar em **Okey** botão do **sincronizar com o banco de dados** caixa de diálogo.  
  
## <a name="scripting-objects"></a>Objetos de script  
Para salvar [!INCLUDE[tsql](../../includes/tsql_md.md)] as definições dos objetos de banco de dados convertido, ou alterar as definições de objeto e executar scripts por conta própria, você pode salvar o banco de dados convertido definições de objeto para [!INCLUDE[tsql](../../includes/tsql_md.md)] scripts.  
  
**Para salvar objetos como scripts**  
  
1.  Depois de selecionar os objetos para salvar um script, clique com botão direito **bancos de dados**e, em seguida, clique em **Salvar como Script**.  
  
    Você pode também gerar um script objetos individuais ou as categorias de objetos clicando duas vezes o objeto ou a pasta pai e, em seguida, clicando em **Salvar como Script**.  
  
2.  No **Salvar como** caixa de diálogo caixa, localize a pasta onde deseja salvar o script, digite um nome de arquivo no **nome de arquivo** caixa e, em seguida, clique em Okey SSMA acrescentará a extensão de nome de arquivo. SQL.  
  
### <a name="modifying-scripts"></a>Modificando Scripts  
Depois de salvar as definições de objeto do SQL Server como um ou mais scripts, você pode usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] para exibir e modificar os scripts.  
  
**Para modificar um script**  
  
1.  Sobre o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **arquivo** , aponte para **abrir**e, em seguida, clique em **arquivo**.  
  
2.  No **abrir** caixa de diálogo, selecione o arquivo de script, clique Okey.
  
3.  Edite o arquivo de script usando o editor de consulta.  
  
    Para obter mais informações sobre o editor de consultas, consulte "Editor conveniência comandos e recursos" nos Manuais Online do SQL Server.  
  
4.  Para salvar o script de clique do menu arquivo **salvar**.  
  
### <a name="running-scripts"></a>Execução de Scripts  
Você pode executar um script ou instruções individuais, em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
**Para executar um script**  
  
1.  Sobre o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **arquivo** , aponte para **abrir**e, em seguida, clique em **arquivo**.  
  
2.  No **abrir** caixa de diálogo, selecione o arquivo de script e, em seguida, clique em Okey  
  
3.  Para executar o script completo, pressione a **F5** chave.  
  
4.  Para executar um conjunto de instruções, selecione as instruções na janela do editor de consulta e, em seguida, pressione a **F5** chave.  
  
Para obter mais informações sobre como usar o editor de consultas para executar scripts, consulte "[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] [!INCLUDE[tsql](../../includes/tsql_md.md)] consulta" nos Manuais Online do SQL Server.  
  
Você também pode executar scripts de linha de comando usando o **sqlcmd** utility e no SQL Server Agent. Para obter mais informações sobre **sqlcmd**, consulte "utilitário sqlcmd" nos Manuais Online do SQL Server. Para obter mais informações sobre o SQL Server Agent, consulte "Automatizando tarefas administrativas (SQL Server Agent)" nos Manuais Online do SQL Server.  
  
## <a name="securing-objects-in-sql-server"></a>Proteção de objetos no SQL Server  
Depois que você carregou os objetos de banco de dados convertido no SQL Server, você pode conceder e negar permissões nesses objetos. É uma boa ideia fazer isso antes de migrar dados para o SQL Server. Para obter informações sobre como ajudar a proteger objetos no SQL Server, consulte "Considerações para bancos de dados e banco de dados de aplicativos de segurança" nos Manuais Online do SQL Server.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração é [migrar dados para o SQL Server](http://msdn.microsoft.com/en-us/e23c5268-41ed-4e55-9fe7-a11376202a13).  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados Oracle para o SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  

