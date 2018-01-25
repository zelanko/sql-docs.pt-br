---
title: ALTER EXTERNAL DATA SOURCE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/09/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL DATA SOURCE
- ALTER_EXTERNAL_DATA_SOURCE
dev_langs: TSQL
helpviewer_keywords:
- polybase, alter external data source statement
- ALTER EXTERNAL DATA SOURCE statement
ms.assetid: a34b9e90-199d-46d0-817a-a7e69387bf5f
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 16ea77011039c1b48ab83bfd335028c83c6f3c3e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="alter-external-data-source-transact-sql"></a>ALTER EXTERNAL DATA SOURCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Modifica uma fonte de dados externa usada para criar uma tabela externa. Fonte de dados externa pode ser o armazenamento de BLOBs do Azure ou Hadoop (WASB).
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Modify an external data source
-- Applies to: SQL Server (2016 or later)
ALTER EXTERNAL DATA SOURCE data_source_name SET
    {   
        LOCATION = 'server_name_or_IP' [,] |
        RESOURCE_MANAGER_LOCATION = <'IP address;Port'> [,] |
        CREDENTIAL = credential_name
    }  
    [;]  

-- Modify an external data source pointing to Azure Blob storage
-- Applies to: SQL Server (starting with 2017)
ALTER EXTERNAL DATA SOURCE data_source_name
    WITH (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://storage_account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ]
    )  
```  
  
## <a name="arguments"></a>Argumentos  
 data_source_name Especifica o nome da fonte de dados definido pelo usuário. O nome deve ser exclusivo.
  
 LOCAL = 'server_name_or_IP' especifica o nome do servidor ou endereço IP.
  
 RESOURCE_MANAGER_LOCATION = '\<endereço IP; Porta >' especifica o local do Gerenciador de recursos do Hadoop. Quando especificado, o otimizador de consulta pode escolher pré-processar dados para uma consulta do PolyBase usando recursos de computação do Hadoop. Isso é uma decisão baseada em custo. Chamado a aplicação de predicado, isso pode reduzir significativamente o volume de dados transferidos entre Hadoop e SQL e, portanto, melhorar o desempenho da consulta.
  
 CREDENCIAL = Credential_Name Especifica a credencial nomeada. Consulte [CREATE DATABASE SCOPED CREDENTIAL &#40; Transact-SQL &#41; ](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).

TYPE = BLOB_STORAGE   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].
Para as operações em massa, `LOCATION` devem ser válidas a URL para o armazenamento de BLOBs do Azure. Não coloque  **/** , nome de arquivo ou compartilhado parâmetros de assinatura de acesso no final de `LOCATION` URL.
A credencial usada, deve ser criada usando `SHARED ACCESS SIGNATURE` como a identidade. Para mais informações sobre assinaturas de acesso compartilhado, consulte [Usando SAS (Assinatura de Acesso Compartilhado)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).

  
  
## <a name="remarks"></a>Remarks
 Somente a única fonte pode ser modificado por vez. Solicitações simultâneas para modificar a mesma fonte de fazer com que uma instrução de espera. No entanto, as fontes diferentes podem ser modificados ao mesmo tempo. Essa instrução pode executar simultaneamente com outras instruções.
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY EXTERNAL DATA SOURCE.
 > [!IMPORTANT]  
 >  A permissão ALTER ANY EXTERNAL DATA SOURCE concede qualquer entidade de segurança a capacidade de criar e modificar qualquer objeto de fonte de dados externa e, portanto, isso também concede a capacidade de acessar todas as credenciais de banco de dados com escopo no banco de dados. Essa permissão deve ser considerada como altamente privilegiada e, portanto, deve ser concedida somente para entidades confiáveis no sistema.

  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera o local e o local do Gerenciador de recursos de uma fonte de dados existente.
  
```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET
     LOCATION = 'hdfs://10.10.10.10:8020',
     RESOURCE_MANAGER_LOCATION = '10.10.10.10:8032'
    ;
  
```  

 O exemplo a seguir altera a credencial para se conectar a uma fonte de dados existente.
  
```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET
   CREDENTIAL = new_hadoop_user
    ;
```