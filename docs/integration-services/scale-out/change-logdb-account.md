---
title: Alterar a conta para registro em log do SSIS Scale Out | Microsoft Docs
description: Este artigo descreve como alterar a conta de usuário para o log do SSIS Scale Out
ms.custom: performance
ms.date: 12/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: maghan
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: 92cf3e13f1e386a77ba4621b817567af95b42884
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67896983"
---
# <a name="change-the-account-for-scale-out-logging"></a>Alterar a conta para registro em log do Scale Out

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Quando você executa pacotes do SSIS no Scale Out, as mensagens de evento são registradas no banco de dados SSISDB com uma conta de usuário criada automaticamente chamada **##MS_SSISLogDBWorkerAgentLogin##** . O logon desse usuário usa a autenticação do SQL Server.

Se desejar alterar a conta usada para o log do Scale Out, siga estas etapas:

> [!NOTE]
> Caso você use uma conta de usuário do Windows para o log, use a mesma conta que executa o serviço Trabalho do Scale Out. Caso contrário, o logon no SQL Server falhará.

## <a name="1-create-a-user-for-ssisdb"></a>1. Criar um usuário para o SSISDB
Para obter instruções sobre como criar um usuário de banco de dados, consulte [Criar um usuário de banco de dados](../../relational-databases/security/authentication-access/create-a-database-user.md).

## <a name="2-add-the-user-to-the-database-role-ssis_cluster_worker"></a>2. Adicionar o usuário à função de banco de dados ssis_cluster_worker

Para obter instruções sobre como unir uma função de banco de dados, consulte [Unir uma função](../../relational-databases/security/authentication-access/join-a-role.md).

## <a name="3-update-the-logging-information-in-ssisdb"></a>3. Atualizar as informações de log no SSISDB
Chame o procedimento armazenado `[catalog].[update_logdb_info]` com o nome e a cadeia de conexão do SQL Server como parâmetros, conforme mostrado no seguinte exemplo:

    ```sql
    SET @serverName = CONVERT(sysname, SERVERPROPERTY('servername'))
    SET @connectionString = 'Data Source=' + @serverName + ';Initial Catalog=SSISDB;Integrated Security=SSPI;'
    EXEC [internal].[update_logdb_info] @serverName, @connectionString
    GO
    ```

## <a name="4-restart-the-scale-out-worker-service"></a>4. Reiniciar o serviço Trabalho do Scale Out
Reinicie o serviço Trabalho do Scale Out para efetivar a alteração.

## <a name="next-steps"></a>Próximas etapas
-   [Gerenciador do Integration Services Scale Out](integration-services-ssis-scale-out-manager.md)
