---
title: "Alterar a conta para o log do SSIS expansão | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ec785459e5f9585776d83cde3f460c1e79367e46
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="change-the-account-for-scale-out-logging"></a>Alterar a conta para o log de expansão
Quando a execução de pacotes em expansão, as mensagens de evento são registradas em SSISDB com um usuário criado automaticamente **MS_SSISLogDBWorkerAgentLogin # # # #**. O logon do usuário usa a autenticação do SQL Server. Para alterar a conta, seguir as etapas abaixo:

## <a name="1-create-a-user-of-ssisdb"></a>1. Criar um usuário do SSISDB
Para obter instruções de criação de um usuário de banco de dados, consulte [criar um usuário de banco de dados](../../relational-databases/security/authentication-access/create-a-database-user.md).

## <a name="2-add-the-user-to-database-role-ssisclusterworker"></a>2. Adicione o usuário ao ssis_cluster_worker da função de banco de dados

Para obter instruções de junção de uma função de banco de dados, consulte [unir uma função](../../relational-databases/security/authentication-access/join-a-role.md).

## <a name="3-update-logging-information-in-ssisdb"></a>3. Atualizar as informações de registro em log no SSISDB
Chame o procedimento armazenado [catalog]. [update_logdb_info] com a cadeia de nome e a conexão do Sql Server como parâmetros.

#### <a name="example"></a>Exemplo
```sql
SET @serverName = CONVERT(sysname, SERVERPROPERTY('servername'))
SET @connectionString = 'Data Source=' + @serverName + ';Initial Catalog=SSISDB;Integrated Security=SSPI;'
EXEC [internal].[update_logdb_info] @serverName, @connectionString
GO
```

## <a name="4-restart-scale-out-worker-service"></a>4. Reinicie o serviço de escala fora do trabalho

> [!NOTE]
> Se você usar uma conta de usuário do Windows para fazer logon, ele deve ser a mesma conta que está executando o serviço de escala fora do trabalho. Caso contrário, o logon para o SQL Server falhará.

