---
title: 'Lição 3: Criar uma credencial do SQL Server | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 29e57ebd-828f-4dff-b473-c10ab0b1c597
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 85e60c359df2a209742b5b10693fcb72ac9cb37a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090848"
---
# <a name="lesson-3-create-a-sql-server-credential"></a>Lição 3: Criar uma credencial do SQL Server
  Nesta lição, você criará uma credencial para armazenar as informações de segurança usadas para acessar a conta de armazenamento do Windows Azure.  
  
 Uma credencial do SQL Server é um objeto usado para armazenar as informações de autenticação necessárias para se conectar a um recurso fora do SQL Server. A credencial armazena o caminho de URI do contêiner de armazenamento e os valores de chave de assinatura de acesso compartilhado. Para cada contêiner de armazenamento usado por um arquivo de dados ou de log, você deve criar uma Credencial do SQL Server cujo nome corresponda ao caminho do contêiner.  
  
 Para obter informações gerais sobre credenciais, consulte [credenciais &#40;mecanismo de banco de dados&#41;](security/authentication-access/credentials-database-engine.md).  
  
> [!IMPORTANT]  
>  Os requisitos para a criação de uma credencial do SQL Server descritos abaixo são específicos para o [arquivos de dados do SQL Server no Windows Azure](databases/sql-server-data-files-in-microsoft-azure.md) recurso. Para obter informações sobre como criar credenciais para processos de backup no armazenamento do Azure, consulte [lição 2: Criar uma credencial do SQL Server](../tutorials/lesson-2-create-a-sql-server-credential.md).  
  
 Para criar uma Credencial do SQL Server, execute estas etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.  
  
2.  No Pesquisador de Objetos, conecte-se à instância do Mecanismo de Banco de Dados instalado.  
  
3.  Na barra de ferramentas Padrão, clique em Nova Consulta.  
  
4.  Copie e cole o exemplo a seguir na janela de consulta, e modifique conforme necessário. A instrução a seguir criará uma credencial do SQL Server para armazenar o certificado de acesso compartilhado do contêiner de armazenamento.  
  
    ```sql  
  
    USE master  
    CREATE CREDENTIAL credentialname - this name should match the container path and it must start with https.   
       WITH IDENTITY='SHARED ACCESS SIGNATURE', -- this is a mandatory string and do not change it.   
       SECRET = 'sharedaccesssignature' -- this is the shared access signature key that you obtained in Lesson 2.   
    GO  
  
    ```  
  
     Para obter informações detalhadas, consulte [CREATE CREDENTIAL &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-credential-transact-sql) nos Manuais Online do SQL Server.  
  
5.  Para ver todas as credenciais disponíveis, você pode executar a instrução a seguir na janela de consulta:  
  
    ```sql  
    SELECT * from sys.credentials  
    ```  
  
     Para obter mais informações sobre sys. Credentials, consulte [sys. Credentials &#40;Transact-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-credentials-transact-sql) nos Manuais Online do SQL Server.  
  
 **Próxima lição:**  
  
 [Lição 4: Criar um banco de dados no armazenamento do Windows Azure](lesson-3-database-backup-to-url.md)  
  
  
