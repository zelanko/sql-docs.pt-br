---
title: 'Lição 2: criar uma credencial de SQL Server | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 64f8805c-1ddc-4c96-a47c-22917d12e1ab
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: baa337d33173f292145d92b60d6192af2a716c5e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70154334"
---
# <a name="lesson-2-create-a-sql-server-credential"></a>Lesson 2: Create a SQL Server Credential
  **Credencial:** Uma [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] credencial é um objeto usado para armazenar as informações de autenticação necessárias para se conectar a um recurso fora do SQL Server.  Aqui, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] os processos de backup e restauração usam a credencial para autenticar o serviço de armazenamento de BLOBs do Azure. A Credencial armazena o nome da conta de armazenamento e os valores de **access key** da conta de armazenamento. Depois que a credencial for criada, ela deverá ser especificada na opção WITH CREDENTIAL ao emitir instruções BACKUP/RESTORE. Para obter mais informações sobre como exibir, copiar ou gerar novamente as **access keys**da conta de armazenamento, consulte [Chaves de acesso da conta de armazenamento](https://msdn.microsoft.com/library/windowsazure/hh531566.aspx).  
  
 Para obter informações gerais sobre credenciais, consulte [credenciais](../relational-databases/security/authentication-access/credentials-database-engine.md).  
  
 Para obter informações, em outros exemplos em que as credenciais são usadas, consulte [criar um proxy de SQL Server Agent](../ssms/agent/create-a-sql-server-agent-proxy.md).  
  
> [!IMPORTANT]  
>  Os requisitos para criar uma credencial de SQL Server descrito abaixo são específicos para SQL Server processos de backup ([SQL Server Backup para URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)e [SQL Server Backup gerenciado para o Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)). O SQL Server, ao acessar o armazenamento do Azure para gravar ou ler backups, usa o nome da conta de armazenamento e as informações da tecla de acesso.  Para obter mais informações sobre como criar credenciais para armazenar arquivos de banco de dados no armazenamento do Azure, consulte [Lesson 3: Create a SQL Server Credential](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
## <a name="create-a-sql-server-credential"></a>Criar uma credencial do SQL Server  
 Para criar uma credencial do SQL Server, execute as seguintes etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.  
  
2.  No Pesquisador de Objetos, conecte-se à instância do Mecanismo de Banco de Dados que tem o banco de dados AdventureWorks2012 instalado, ou use o banco de dados que você pretende usar neste tutorial.  
  
3.  Na barra de ferramentas **Padrão** , clique em **Nova Consulta**.  
  
4.  Copie e cole o exemplo a seguir na janela de consulta, e modifique conforme necessário.  
  
    ```  
    CREATE CREDENTIAL mycredential   
    WITH IDENTITY= 'mystorageaccount' - this is the name of the storage account you specified when creating a storage account (See Lesson 1)   
    , SECRET = '<storage account access key>' - this should be either the Primary or Secondary Access Key for the storage account (See Lesson 1)  
  
    ```  
  
     ![mapeando a conta de armazenamento para as credenciais do sql](../../2014/tutorials/media/backuptocloud-storage-credential-mapping.gif "mapeando a conta de armazenamento para as credenciais do sql")  
  
5.  Verifique a instrução T-SQL e clique em **Executar**.  
  
 Para obter mais informações sobre o serviço de armazenamento de BLOBs do Azure para conceitos e requisitos de backup, consulte [SQL Server Backup e restauração com o serviço de armazenamento de BLOBs do Azure](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
### <a name="next-lesson"></a>Próxima lição  
 [Lição 3: gravar um backup de banco de dados completo no serviço de armazenamento de BLOBs do Azure](../../2014/tutorials/lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service.md).  
  
  
