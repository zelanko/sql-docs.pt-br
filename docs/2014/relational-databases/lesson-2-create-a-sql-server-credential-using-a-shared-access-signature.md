---
title: 'Lição 3: criar uma credencial de SQL Server | Microsoft Docs'
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
ms.openlocfilehash: 61a25d1f4e86204d05b3be6bf2a5dbc8cd0474b9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70153831"
---
# <a name="lesson-3-create-a-sql-server-credential"></a>Lição 3: Criar uma credencial do SQL Server
  Nesta lição, você criará uma credencial para armazenar informações de segurança usadas para acessar a conta de armazenamento do Azure.  
  
 Uma credencial do SQL Server é um objeto usado para armazenar as informações de autenticação necessárias para se conectar a um recurso fora do SQL Server. A credencial armazena o caminho de URI do contêiner de armazenamento e os valores de chave de assinatura de acesso compartilhado. Para cada contêiner de armazenamento usado por um arquivo de dados ou de log, você deve criar uma Credencial do SQL Server cujo nome corresponda ao caminho do contêiner.  
  
 Para obter informações gerais sobre credenciais, consulte [credenciais &#40;Mecanismo de Banco de Dados&#41;](security/authentication-access/credentials-database-engine.md).  
  
> [!IMPORTANT]  
>  Os requisitos para criar uma credencial de SQL Server descrito abaixo são específicos para o recurso [SQL Server arquivos de dados no Azure](databases/sql-server-data-files-in-microsoft-azure.md) . Para obter informações sobre como criar credenciais para processos de backup no armazenamento do Azure, consulte [Lesson 2: Create a SQL Server Credential](../tutorials/lesson-2-create-a-sql-server-credential.md).  
  
 Para criar uma Credencial do SQL Server, execute estas etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.  
  
2.  No Pesquisador de Objetos, conecte-se à instância do Mecanismo de Banco de Dados instalado.  
  
3.  Na barra de ferramentas Padrão, clique em Nova Consulta.  
  
4.  Copie e cole o exemplo a seguir na janela de consulta, e modifique conforme necessário. A instrução a seguir criará uma credencial SQL Server para armazenar o certificado de acesso compartilhado do seu contêiner de armazenamento.  
  
    ```sql  
  
    USE master  
    CREATE CREDENTIAL credentialname - this name should match the container path and it must start with https.   
       WITH IDENTITY='SHARED ACCESS SIGNATURE', -- this is a mandatory string and do not change it.   
       SECRET = 'sharedaccesssignature' -- this is the shared access signature key that you obtained in Lesson 2.   
    GO  
  
    ```  
  
     Para obter informações detalhadas, consulte [criar credencial &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql) em manuais online do SQL Server.  
  
5.  Para ver todas as credenciais disponíveis, você pode executar a instrução a seguir na janela de consulta:  
  
    ```sql  
    SELECT * from sys.credentials  
    ```  
  
     Para obter mais informações sobre sys. Credentials, consulte [Sys. credentials &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-credentials-transact-sql) em manuais online do SQL Server.  
  
 **Próxima lição:**  
  
 [Lição 4: Criar um banco de dados no Armazenamento do Azure](lesson-3-database-backup-to-url.md)  
  
  
