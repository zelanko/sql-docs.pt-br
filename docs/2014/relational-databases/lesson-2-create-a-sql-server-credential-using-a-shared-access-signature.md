---
title: 'Lição 3: Criar uma credencial de SQL Server | Microsoft Docs'
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
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153831"
---
# <a name="lesson-3-create-a-sql-server-credential"></a>Lição 3: Criar uma credencial do SQL Server
  Nesta lição, você criará uma credencial para armazenar informações de segurança usadas para acessar a conta de armazenamento do Azure.  
  
 Uma credencial do SQL Server é um objeto usado para armazenar as informações de autenticação necessárias para se conectar a um recurso fora do SQL Server. A credencial armazena o caminho de URI do contêiner de armazenamento e os valores de chave de assinatura de acesso compartilhado. Para cada contêiner de armazenamento usado por um arquivo de dados ou de log, você deve criar uma Credencial do SQL Server cujo nome corresponda ao caminho do contêiner.  
  
 Para obter informações gerais sobre credenciais, [consulte &#40;credenciais&#41;mecanismo de banco de dados](security/authentication-access/credentials-database-engine.md).  
  
> [!IMPORTANT]  
>  Os requisitos para criar uma credencial de SQL Server descrito abaixo são específicos para o recurso [SQL Server arquivos de dados no Azure](databases/sql-server-data-files-in-microsoft-azure.md) . Para obter informações sobre como criar credenciais para processos de backup no armazenamento [do Azure, consulte Lição 2: Crie uma credencial](../tutorials/lesson-2-create-a-sql-server-credential.md)de SQL Server.  
  
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
  
     Para obter informações detalhadas, consulte [criar &#40;credencial Transact&#41; -SQL](/sql/t-sql/statements/create-credential-transact-sql) em manuais online do SQL Server.  
  
5.  Para ver todas as credenciais disponíveis, você pode executar a instrução a seguir na janela de consulta:  
  
    ```sql  
    SELECT * from sys.credentials  
    ```  
  
     Para obter mais informações sobre sys. Credentials, consulte [Sys &#40;. Credentials&#41; Transact-SQL](/sql/relational-databases/system-catalog-views/sys-credentials-transact-sql) em manuais online do SQL Server.  
  
 **Próxima lição:**  
  
 [Lição 4: Criar um banco de dados no armazenamento do Azure](lesson-3-database-backup-to-url.md)  
  
  
