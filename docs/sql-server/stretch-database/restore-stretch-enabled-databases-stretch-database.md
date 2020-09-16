---
description: Restaurar bancos de dados habilitados para Stretch (Stretch Database)
title: Restaurar bancos de dados habilitados para Stretch
ms.date: 07/06/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: cebc1f6d-d5ea-460d-ae60-d047d29c2723
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 8cef37be62e91b608852a4b5867d5917e72e8742
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492593"
---
# <a name="restore-stretch-enabled-databases-stretch-database"></a>Restaurar bancos de dados habilitados para Stretch (Stretch Database)
[!INCLUDE [sqlserver2016-windows-only](../../includes/applies-to-version/sqlserver2016-windows-only.md)]


  Restaure um banco de dados de backup, quando necessário, para se recuperar de muitos tipos de falhas, erros e desastres.
  
  Para obter mais informações sobre backup, veja [Fazer backup de bancos de dados habilitados para Stretch](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md).

> [!TIP]
> O backup é apenas uma parte de uma solução de continuidade dos negócios e de alta disponibilidade. Para obter mais informações sobre a alta disponibilidade, consulte [Soluções de alta disponibilidade](../../database-engine/sql-server-business-continuity-dr.md).

## <a name="restore-your-sql-server-data"></a>Restaurar os dados do SQL Server
Para se recuperar de falhas de hardware ou de corrupção, restaure o banco de dados SQL Server habilitado para Stretch por meio de um backup. Você pode continuar a usar os métodos de restauração do SQL Server que você utiliza atualmente. Para obter mais informações, veja [Visão geral da recuperação e restauração](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).

Depois de restaurar o banco de dados SQL Server, você precisa executar o procedimento armazenado **sys.sp_rda_reauthorize_db** para restabelecer a conexão entre o banco de dados SQL Server habilitado para Stretch e o banco de dados remoto do Azure. Para obter mais informações, veja [Restaurar a conexão entre o banco de dados SQL Server e o banco de dados remoto do Azure](#reconnect).

## <a name="restore-your-remote-azure-data"></a>Restaurar os dados remotos do Azure

### <a name="recover-a-live-azure-database"></a>Recuperar um banco de dados dinâmico do Azure
O serviço SQL Server Stretch Database no Azure tira instantâneos de todos os dados dinâmicos com uma frequência mínima de intervalos de 8 horas usando os Instantâneos do Armazenamento do Azure. Esses instantâneos são mantidos por 7 dias. Isso permite que você restaure os dados em, no mínimo, um dos 21 pontos específicos dos últimos 7 dias até a hora em que o último instantâneo foi tirado.

Para restaurar um banco de dados dinâmico do Azure em um ponto específico anterior por meio do portal do Azure, siga o procedimento a seguir.

1. Faça logon no [Portal do Azure][].
2. No lado esquerdo da tela, selecione **PROCURAR** e **Bancos de Dados SQL**.
3. Navegue até o banco de dados e selecione-o.
4. Na parte superior da folha do banco de dados, clique em **Restaurar**.
5. Especifique um novo **Nome de banco de dados**, selecione um **Ponto de restauração** e clique em **Criar**.
6. O processo de restauração de banco de dados será iniciado e poderá ser monitorado com **NOTIFICATIONS**.

### <a name="recover-a-deleted-azure-database"></a>Recuperar um banco de dados excluído do Azure
O serviço SQL Server Stretch Database no Azure tira um instantâneo de banco de dados antes que um banco de dados seja removido e o retém por 7 dias. Depois disso, ele não retém mais instantâneos do banco de dados dinâmico. Isso permite restaurar um banco de dados excluído no ponto em que ele foi excluído.

Para restaurar um banco de dados do Azure excluído no ponto em que ele foi excluído usando o portal do Azure, siga os procedimentos a seguir.

1. Faça logon no [Portal do Azure][].
2. No lado esquerdo da tela, selecione **PROCURAR** e **SQL Servers**.
3. Navegue até o servidor e selecione-o.
4. Role para baixo até Operações na folha do servidor e clique no bloco **Bancos de Dados Excluídos** .
5. Selecione o banco de dados excluído que você deseja restaurar.
5. Especifique um novo **Nome de banco de dados** e clique em **Criar**.
6. O processo de restauração de banco de dados será iniciado e poderá ser monitorado com **NOTIFICATIONS**.

## <a name="restore-the-connection-between-the-sql-server-database-and-the-remote-azure-database"></a><a name="reconnect"></a>Restaurar a conexão entre o banco de dados SQL Server e o banco de dados remoto do Azure

1.  Se você pretende se conectar a um banco de dados Azure restaurado com um nome diferente ou em uma região diferente, execute o procedimento armazenado [sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md) para se desconectar do banco de dados do Azure anterior.  
  
2.  Execute o procedimento armazenado [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) para reconectar o banco de dados local habilitado para Stretch ao banco de dados do Azure.  
  
    -   Forneça as credenciais no escopo do banco de dados existente como um sysname ou um valor varchar(128). (Não use varchar(max)). É possível procurar o nome da credencial na exibição **sys.database_scoped_credentials**.  
  
    -   Especifique se deseja fazer uma cópia dos dados remotos e conectar-se à cópia (recomendado).  
  
    ```sql  
    USE <Stretch-enabled database name>;
    GO
    EXEC sp_rda_reauthorize_db
        @credential = N'<existing_database_scoped_credential_name>',
        @with_copy = 1 ;  
    GO  
    ```  
    
  ## <a name="see-also"></a>Consulte Também  
 [Fazer backup de bancos de dados habilitados para Stretch](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
 [Gerenciar e solucionar problemas no Stretch Database](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)   
 [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 
 [sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)  
 [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
 
 [Azure portal]: https://portal.azure.com/
 
