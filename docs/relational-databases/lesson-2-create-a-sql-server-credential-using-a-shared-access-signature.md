---
title: "Lição 2: Criar uma credencial do SQL Server usando uma assinatura de acesso compartilhado | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 02/25/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 29e57ebd-828f-4dff-b473-c10ab0b1c597
caps.latest.revision: 17
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f6e88b211fc2a053ffeadb038298a28179a94d88
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-2-create-a-sql-server-credential-using-a-shared-access-signature"></a>Lição 2: Criar uma credencial do SQL Server usando uma assinatura de acesso compartilhado
Nesta lição, você aprenderá a criar uma credencial para armazenar as informações de segurança que serão usadas pelo SQL Server para gravar e ler o contêiner do Azure criado na [Lição 1: Criar uma política de acesso armazenado e uma assinatura de acesso compartilhado em um contêiner do Azure](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md).  
  
Uma credencial do SQL Server é um objeto usado para armazenar as informações de autenticação necessárias para se conectar a um recurso fora do SQL Server. A credencial armazena o caminho de URI do contêiner de armazenamento e a assinatura de acesso compartilhado desse contêiner.  
  
> [!NOTE]  
> Se quiser fazer backup de um banco de dados SQL Server 2012 SP1 CU2 ou posterior ou SQL Server 2014 nesse contêiner do Azure, você poderá usar a [sintaxe preterida](https://technet.microsoft.com/en-US/library/dn435916(v=sql.120).aspx) documentada aqui para criar uma credencial do SQL Server baseada em sua chave de conta de armazenamento.  
  
## <a name="create-sql-server-credential"></a>Criar uma credencial do SQL Server  
Para criar uma credencial do SQL Server, siga estas etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.  
  
2.  Abra uma nova janela de consulta e conecte-se à instância do SQL Server 2016 do mecanismo de banco de dados no ambiente local.  
  
3.  Na nova janela de consulta, cole a instrução CREATE CREDENTIAL com a assinatura de acesso compartilhado da Lição 1 e execute esse script.  
  
    O script será parecido com o código a seguir.  
  
    ```Transact-SQL  
  
    USE master  
    CREATE CREDENTIAL [https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>] – this name must match the container path, start with https and must not contain a forward slash.  
       WITH IDENTITY='SHARED ACCESS SIGNATURE' -- this is a mandatory string and do not change it.   
       , SECRET = 'sharedaccesssignature' –- this is the shared access signature key that you obtained in Lesson 1.   
    GO  
  
    ```  
  
4.  Para ver todas as credenciais disponíveis, você pode executar a seguinte instrução em uma janela de consulta conectada à sua instância:  
  
    ```Transact-SQL  
    SELECT * from sys.credentials  
    ```  
  
5.  Abra uma nova janela de consulta e conecte-se à instância do SQL Server 2016 do mecanismo de banco de dados na máquina virtual do Azure.  
  
6.  Na nova janela de consulta, cole a instrução CREATE CREDENTIAL com a assinatura de acesso compartilhado da Lição 1 e execute esse script.  
  
7.  Repita as etapas 5 e 6 para todas as outras instâncias do SQL Server 2016 às quais você quer conceder acesso ao contêiner do Azure.  
  
**Próxima lição:**  
  
[Lição 3: Backup de banco de dados em URL](../relational-databases/lesson-3-database-backup-to-url.md)  
  
## <a name="see-also"></a>Consulte também  
[Credenciais &#40;Mecanismo de Banco de Dados&#41;](../relational-databases/security/authentication-access/credentials-database-engine.md)  
[CREATE CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-credential-transact-sql.md)  
[sys.credentials &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  


