---
title: Assistente de migração (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Migration Wizard dialog box
- Migration Wizard, adding Access databases
- Migration Wizard, Connect to SQL Azure
- Migration Wizard, Connect to SQL Server
- Migration Wizard, Link Tables
- Migration Wizard, Migration status
- Migration Wizard, New Project
- Migration Wizard, Selecting objects to migrate
ms.assetid: 5bab5914-b2ae-4795-8cf5-83e42d64bef2
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 658487186924fe5547edee70425524b2b4e3be6c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68083589"
---
# <a name="migration-wizard-accesstosql"></a>Assistente de migração (AccessToSQL)
O assistente de migração orienta você pela migração de um ou mais bancos de dados de acesso ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Usando o assistente, você criará um projeto, adicionará bancos de dados ao projeto, selecionará objetos para migrar e se conectará [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Você também irá converter, carregar e migrar esquemas e dados de acesso. Opcionalmente, você pode vincular tabelas de acesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a tabelas ou SQL Azure.  
  
A maioria das páginas do assistente de migração contém as mesmas opções que as caixas de diálogo do SSMA existentes. Portanto, as páginas do assistente são descritas aqui e os links são fornecidos para que você possa saber mais sobre as opções individuais. Se uma página contiver opções exclusivas, elas serão documentadas aqui.  
  
## <a name="starting-the-migration-wizard"></a>Iniciando o assistente de migração  
Por padrão, o assistente de migração é exibido quando você inicia o SSMA. Você também pode iniciar o assistente no menu **arquivo** selecionando **Assistente de migração**.  
  
## <a name="welcome-page"></a>Página de boas-vindas  
A página de boas-vindas apresenta o assistente de migração e fornece a opção a seguir para iniciar o assistente.  
  
**Inicie este assistente na inicialização.**  
Por padrão, o SSMA iniciará o assistente de migração quando você iniciar o SSMA. Para evitar o início automático do assistente, desmarque essa caixa de seleção.  
  
## <a name="create-new-project-page"></a>Página Criar novo projeto  
A página Criar novo projeto é onde você insere o nome do arquivo de projeto, local e tipo de projeto de migração (a versão do SQL Server de destino usada para migração). Para obter mais informações, consulte [novo projeto (SSMA)](https://msdn.microsoft.com/ca294f6d-eeb5-42ca-9306-156281a3f0f3)  
  
## <a name="add-access-databases-page"></a>Página Adicionar bancos de dados do Access  
A página Adicionar bancos de dados do Access é onde você adiciona um ou mais bancos de dados do Access ao projeto. Você pode adicionar bancos de dados individuais clicando em **Adicionar bancos de dados**e, em seguida, selecionando os bancos de dados na janela **abrir** . Ou, você pode encontrar bancos de dados usando o botão **Localizar bancos de dados** . Para obter mais informações, consulte estes tópicos:  
  
-   [Adicionando e removendo arquivos de banco de dados do Access](adding-and-removing-access-database-files-accesstosql.md)  
  
-   [Assistente Localizar Bancos de Dados (selecione os locais)](https://msdn.microsoft.com/00b2d32a-998b-47a7-b25c-589b5bd6777a)  
  
-   [Assistente Localizar Bancos de Dados (selecione os arquivos)](https://msdn.microsoft.com/2f574a34-4bab-40a4-89a8-ad4907ffc3fd)  
  
-   [Assistente Localizar Bancos de Dados (verifique a seleção)](https://msdn.microsoft.com/62e20e03-50cc-4ac8-8072-524d194d2ec3)  
  
## <a name="select-objects-to-migrate-page"></a>Página Selecionar objetos a serem migrados  
Na página Selecionar objetos a serem migrados, você seleciona os objetos a serem convertidos. Você pode selecionar todos os objetos, grupos de objetos ou objetos individuais.  
  
**Para selecionar objetos**  
  
1.  Expanda **acesso-metabase**e expanda **bancos de dados**.  
  
2.  Execute uma ou mais das seguintes opções:  
  
    -   Para converter todos os bancos de dados, marque a caixa de seleção ao lado de **bancos de dados**.  
  
    -   Para converter ou omitir bancos de dados individuais, marque ou desmarque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para converter ou omitir consultas, expanda o banco de dados e marque ou desmarque a caixa de seleção **consultas** .  
  
    -   Para converter ou omitir tabelas individuais, expanda o banco de dados, expanda **tabelas**e marque ou desmarque a caixa de seleção ao lado da tabela.  
  
Se você tiver muitos objetos, talvez queira usar as opções de **seleção de objetos avançadas** no painel direito para filtrar objetos de banco de dados do Access. Por exemplo, se você selecionar **tabelas** no painel esquerdo, poderá filtrar a lista de tabelas inserindo cadeias de caracteres na caixa de **filtro** . Você pode selecionar ou limpar as tabelas filtradas para migração usando os botões na parte superior do painel.  
  
Para obter mais informações sobre filtragem, consulte a seção Opções da [seleção avançada de objetos (SSMA Common)](https://msdn.microsoft.com/f53b0c79-5473-410a-a0dc-d8f544f7a63c).  
  
## <a name="connect-to-sql-server-page"></a>Conectar à página de SQL Server  
Na página conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , especifique as propriedades de conexão e, em seguida, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Conecte-se ao. Para obter mais informações, consulte [conectar-se a SQL Server](connect-to-sql-server-accesstosql.md).
  
> [!IMPORTANT]  
> Assim que a conexão for bem sucedido, você encontrará a página **vincular tabelas** , em que você tem a opção de vincular as tabelas. Clique em **Avançar** e a migração será iniciada.  
  
## <a name="connect-to-sql-azure-page"></a>Conectar à página de SQL Azure  
Na página conectar a SQL Azure, especifique as propriedades de conexão e conecte-se ao SQL Azure. Para criar um novo banco de dados do Azure, você pode fazer isso usando a opção **criar banco de dados do Azure** que aparece no clique no botão **procurar** . Para obter mais informações, consulte [conectar-se ao SQL Azure](connect-to-azure-sql-db-accesstosql.md)  
  
> [!IMPORTANT]  
> Assim que a conexão for bem sucedido, você encontrará a página **vincular tabelas** , em que você tem a opção de vincular as tabelas. Clique no botão **Avançar** na página links para iniciar a migração.  
  
## <a name="link-tables-page"></a>Página vincular tabelas  
A página vincular tabelas permite vincular as tabelas originais do Access às tabelas migradas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. A vinculação de tabelas modifica seu banco de dados do Access de forma que suas consultas, formulários, relatórios e páginas de acesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] data usem os dados no banco de dado ou SQL Azure em vez dos dados no banco de dado do Access.  
  
**Vincular tabelas**  
Marque a caixa de seleção **vincular tabelas** para vincular tabelas de acesso às tabelas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] migradas ou SQL Azure. Para iniciar a migração, clique no botão **Avançar** .  
  
## <a name="migration-status-page"></a>Página status da migração  
A página status da migração mostra o progresso da conversão dos esquemas de acesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ou SQL Azure esquemas, o carregamento dos esquemas convertidos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em ou SQL Azure e, em seguida, a migração de dados.  
  
Para obter mais informações sobre essa página, consulte [converter, carregar e migrar](https://msdn.microsoft.com/4ec83e96-88a5-4b7b-8d5a-f3429d9a936b)  
  
## <a name="see-also"></a>Consulte Também  
[Introdução com Assistente de Migração do SQL Server para acesso &#40;AccessToSQL&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[Migrando bancos de dados do Access para SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Referência da interface do usuário (Access)](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
