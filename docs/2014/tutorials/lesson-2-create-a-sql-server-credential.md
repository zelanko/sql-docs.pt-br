---
title: 'Lição 2: Criar uma credencial do SQL Server | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 64f8805c-1ddc-4c96-a47c-22917d12e1ab
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 358c88c0fef9c4ffaf7c7fc93458be1b1563d94e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37163797"
---
# <a name="lesson-2-create-a-sql-server-credential"></a>Lesson 2: Create a SQL Server Credential
  **Credencial:** uma credencial do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é um objeto usado para armazenar as informações de autenticação necessárias para se conectar a um recurso fora do SQL Server.  Aqui, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] processos de backup e restauração usam a credencial para se autenticar no serviço de armazenamento de Blob do Windows Azure. A Credencial armazena o nome da conta de armazenamento e os valores de **access key** da conta de armazenamento. Depois que a credencial for criada, ela deverá ser especificada na opção WITH CREDENTIAL ao emitir instruções BACKUP/RESTORE. Para obter mais informações sobre como exibir, copiar ou gerar novamente as **access keys**da conta de armazenamento, consulte [Chaves de acesso da conta de armazenamento](http://msdn.microsoft.com/library/windowsazure/hh531566.aspx).  
  
 Para obter informações gerais sobre credenciais, consulte [Credenciais](http://msdn.microsoft.com/library/ms161950.aspx).  
  
 Para obter informações sobre outros exemplos em que as credenciais são usadas, consulte [Criar um proxy do SQL Server Agent](http://msdn.microsoft.com/library/ms175834.aspx).  
  
> [!IMPORTANT]  
>  Os requisitos para a criação de uma credencial do SQL Server descritos abaixo são específicos para processos de backup do SQL Server ([SQL Server Backup to URL](../relational-databases/backup-restore/sql-server-backup-to-url.md), e [SQL Server Managed Backup to Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)). O SQL Server, ao acessar o armazenamento do Azure para gravar ou ler backups, usa o nome da conta de armazenamento e as informações da tecla de acesso.  Para obter mais informações sobre como criar credenciais para armazenar arquivos de banco de dados no armazenamento do Azure, consulte [lição 3: criar uma credencial do SQL Server](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
## <a name="create-a-sql-server-credential"></a>Criar uma credencial do SQL Server  
 Para criar uma credencial do SQL Server, execute as seguintes etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.  
  
2.  No Pesquisador de Objetos, conecte-se à instância do Mecanismo de Banco de Dados que tem o banco de dados AdventureWorks2012 instalado, ou use o banco de dados que você pretende usar neste tutorial.  
  
3.  Na barra de ferramentas **Padrão** , clique em **Nova Consulta**.  
  
4.  Copie e cole o exemplo a seguir na janela de consulta, e modifique conforme necessário.  
  
    ```  
    CREATE CREDENTIAL mycredential   
    WITH IDENTITY= 'mystorageaccount' – this is the name of the storage account you specified when creating a storage account (See Lesson 1)   
    , SECRET = '<storage account access key>' – this should be either the Primary or Secondary Access Key for the storage account (See Lesson 1)  
  
    ```  
  
     ![mapeamento de conta de armazenamento para as credenciais do sql](../../2014/tutorials/media/backuptocloud-storage-credential-mapping.gif "mapeando a conta de armazenamento para as credenciais do sql")  
  
5.  Verifique a instrução T-SQL e clique em **Executar**.  
  
 Para obter mais informações sobre o serviço de armazenamento de Blob do Windows Azure para requisitos e conceitos de backup, consulte [SQL Server Backup and Restore with Windows Azure Blob Storage Service](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
### <a name="next-lesson"></a>Próxima lição  
 [Lição 3: Gravar um Backup de banco de dados completo para o serviço de armazenamento de BLOBs do Azure Windows](../../2014/tutorials/lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service.md).  
  
  
