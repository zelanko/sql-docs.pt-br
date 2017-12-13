---
title: Alterar a conta para registro em log do SSIS Scale Out | Microsoft Docs
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dcedbe0d2c2ef2c2089af1e2a8b31fbeb75ce2fc
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="change-the-account-for-scale-out-logging"></a>Alterar a conta para registro em log do Scale Out
Ao executar pacotes no Scale Out, as mensagens de evento são registradas no SSISDB com um usuário **##MS_SSISLogDBWorkerAgentLogin##** criado automaticamente. O logon do usuário usa a autenticação do SQL Server. Para alterar a conta, siga as etapas abaixo:

## <a name="1-create-a-user-of-ssisdb"></a>1. Criar um usuário do SSISDB
Para obter instruções de criação de um usuário de banco de dados, consulte [Criar um usuário de banco de dados](../../relational-databases/security/authentication-access/create-a-database-user.md).

## <a name="2-add-the-user-to-database-role-ssisclusterworker"></a>2. Adicionar o usuário à função de banco de dados ssis_cluster_worker

Para obter instruções como unir uma função de banco de dados, consulte [Unir uma função](../../relational-databases/security/authentication-access/join-a-role.md).

## <a name="3-update-logging-information-in-ssisdb"></a>3. Atualizar as informações de registro em log no SSISDB
Chame o procedimento armazenado [catalog].[update_logdb_info] com a cadeia de conexão e o nome do SQL Server como parâmetros.

#### <a name="example"></a>Exemplo
```sql
SET @serverName = CONVERT(sysname, SERVERPROPERTY('servername'))
SET @connectionString = 'Data Source=' + @serverName + ';Initial Catalog=SSISDB;Integrated Security=SSPI;'
EXEC [internal].[update_logdb_info] @serverName, @connectionString
GO
```

## <a name="4-restart-scale-out-worker-service"></a>4. Reiniciar o serviço Trabalho do Scale Out

> [!NOTE]
> Se você usar uma conta de usuário do Windows para fazer logon, ela deverá ser a mesma que está executando o serviço de Trabalho do Scale Out. Caso contrário, o logon para o SQL Server falhará.
