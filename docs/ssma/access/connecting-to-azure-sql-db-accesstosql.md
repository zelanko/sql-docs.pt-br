---
title: Conectando-se ao BD SQL do Azure (AccessToSQL) | Microsoft Docs
description: Saiba como se conectar a uma instância de destino do banco de dados SQL do Azure para migrar bancos de dados do Access. O SSMA obtém metadados sobre bancos de dados no banco de dados SQL do Azure.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- instance of SQL Azure
- metadata, refreshing
- refreshing metadata
- SQL Azure
- SQL Azure, connecting
- SQL Azure, connecting to
- SQL Azure, reconnecting
- SQL Azure, synchronizing metadata
ms.assetid: 1ba0d113-dc05-4431-8689-e14a8821bafd
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: f07d63387a6abd55aa2a130f2809681b00a71b19
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293123"
---
# <a name="connecting-to-azure-sql-db-accesstosql"></a>Conectando-se ao BD SQL do Azure (AccessToSQL)
Para migrar bancos de dados do Access para SQL Azure, você deve se conectar à instância de destino do SQL Azure. Quando você se conecta, o SSMA obtém metadados sobre todos os bancos de dados na instância do SQL Azure e exibe os metadados do banco de dados no SQL Azure Gerenciador de metadados. O SSMA armazena informações sobre a instância do SQL Azure à qual você está conectado, mas não armazena senhas.  
  
Sua conexão com SQL Azure permanece ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar ao SQL Azure se quiser uma conexão ativa com o servidor. Você pode trabalhar offline até carregar os objetos de banco de dados em SQL Azure e migrar.  
  
Os metadados sobre a instância do SQL Azure não são sincronizados automaticamente. Em vez disso, para atualizar os metadados no SQL Azure Gerenciador de metadados, você deve atualizar manualmente os metadados de SQL Azure. Para obter mais informações, consulte a seção "sincronizando metadados de SQL Azure" mais adiante neste tópico.  
  
## <a name="required-sql-azure-permissions"></a>Permissões de SQL Azure necessárias  
A conta usada para se conectar ao SQL Azure requer permissões diferentes dependendo das ações que a conta executa:  
  
-   Para converter objetos do Access em [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe, para atualizar metadados de SQL Azure ou para salvar a sintaxe convertida em scripts, a conta deve ter permissão para fazer logon na instância do SQL Azure.  
  
-   Para carregar objetos de banco de dados em SQL Azure, o requisito mínimo de permissão é a associação na função de banco de dados **db_owner** no banco de dados de destino.  
  
## <a name="establishing-a-sql-azure-connection"></a>Estabelecendo uma conexão SQL Azure  
Antes de converter objetos de banco de dados do Access para SQL Azure sintaxe, você deve estabelecer uma conexão com a instância do SQL Azure em que você deseja migrar o banco de dados ou bancos de dados do Access.  
  
Ao definir as propriedades de conexão, você também especifica o banco de dados em que os objetos e data serão migrados. Você pode personalizar esse mapeamento no nível de esquema de acesso depois de se conectar ao SQL Azure. Para obter mais informações, consulte [mapeando bancos de dados do Access para esquemas de SQL Server](mapping-source-and-target-databases-accesstosql.md)  
  
> [!IMPORTANT]  
> Antes de tentar se conectar ao SQL Azure, verifique se a instância do SQL Azure está em execução e pode aceitar conexões.  
  
**Para se conectar ao SQL Azure**  
  
1.  No menu **arquivo** , selecione **conectar-se a SQL Azure** (essa opção é habilitada após a criação de um projeto).  
  
    Se você se conectou anteriormente ao SQL Azure, o nome do comando será **reconectado ao SQL Azure**.  
  
2.  Na caixa de diálogo conexão, insira ou selecione o nome do servidor de SQL Azure.  
  
3.  Insira, selecione ou **procure** o nome do banco de dados.  
  
4.  Insira ou selecione o **nome de usuário**.  
  
5.  Insira a **senha**.  
  
6.  O SSMA recomenda a conexão criptografada com SQL Azure.  
  
7.  Clique em **Conectar**.  
  
> [!IMPORTANT]  
> O SSMA para Access não oferece suporte à conexão com o banco de dados **mestre** no SQL Azure.  
  
Se não houver bancos de dados na conta de SQL Azure, você poderá criar o primeiro banco usando a opção **criar banco de dados do Azure** que aparece no clique no botão **procurar** .  
  
## <a name="synchronizing-sql-azure-metadata"></a>Sincronizando metadados de SQL Azure  
Metadados sobre bancos de dados SQL Azure não são atualizados automaticamente. Os metadados no SQL Azure Gerenciador de metadados é um instantâneo dos metadados quando você se conecta pela primeira vez ao SQL Azure, ou a última vez que você atualizou os metadados manualmente. Você pode atualizar os metadados manualmente para todos os bancos de dados ou para qualquer banco de dados ou objeto de banco de dados individual.  
  
**Para sincronizar metadados**  
  
1.  Verifique se você está conectado a SQL Azure.  
  
2.  No SQL Azure Gerenciador de metadados, marque a caixa de seleção ao lado do banco de dados ou esquema de banco de dados que você deseja atualizar.  
  
    Por exemplo, para atualizar os metadados de todos os bancos de dados, selecione a caixa ao lado de bancos de dados.  
  
3.  Clique com o botão direito do mouse em bancos de dados ou em um esquema ou banco de dados individual e selecione **sincronizar com Banco de dados**.  
  
## <a name="refreshing-sql-azure-metadata"></a>Atualizando metadados de SQL Azure  
Se SQL Azure esquemas forem alterados depois de se conectar, você poderá atualizar os metadados do servidor.  
  
**Para atualizar SQL Azure metadados**  
  
-   No SQL Azure Gerenciador de metadados, clique com o botão direito do mouse em **bancos**de dados e selecione **Atualizar do Database**.  
  
## <a name="reconnecting-to-sql-azure"></a>Reconectando ao SQL Azure  
Sua conexão com SQL Azure permanece ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar ao SQL Azure se quiser uma conexão ativa com o servidor. Você pode trabalhar offline até carregar os objetos de banco de dados em SQL Azure e migrar.  
  
O procedimento para reconectar-se a SQL Azure é o mesmo que o procedimento para estabelecer uma conexão.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa na migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento entre esquemas de acesso e bancos de dados SQL Azure e esquemas, consulte [mapeando bancos de dados de acesso para esquemas de SQL Server](mapping-source-and-target-databases-accesstosql.md).  
  
-   Para personalizar as opções de configuração para os projetos, consulte [definindo opções de projeto](setting-conversion-and-migration-options-accesstosql.md).  
  
-   Para personalizar o mapeamento de tipos de dados de origem e de destino, consulte [mapeando tipos de dados de origem e de destino](mapping-source-and-target-data-types-accesstosql.md).  
  
-   Se você não precisar executar nenhuma dessas tarefas, poderá converter as definições de objeto de banco de dados do Access em SQL Azure definições de objeto. Para obter mais informações, consulte [convertendo bancos de dados do Access](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados do Access para SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
