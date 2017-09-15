---
title: Catalog.disable_worker_agent (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f19dc4c-a000-4318-8fe1-e80d56720e66
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: aab83dd2f179c8e6b90ad9ff7a212597a51038de
ms.contentlocale: pt-br
ms.lasthandoff: 09/08/2017

---
# <a name="catalogdisableworkeragent-ssisdb-database"></a>Catalog.disable_worker_agent (banco de dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Desabilitar um trabalho de fora de escala para escala Out mestre funcionam com essa [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] catálogo.

## <a name="syntax"></a>Sintaxe

```tsql
disable_worker_agent [@WorkerAgentId = ] WorkerAgentId
```
## <a name="arguments"></a>Argumentos
[ @WorkerAgentId =] *WorkerAgentId* a id do agente de trabalho da escala fora do trabalho. O *WorkerAgentId* é **uniqueidentifier**.

## <a name="example"></a>Exemplo
Este exemplo desabilita a escala Out trabalho no computador.
```tsql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    MachineA    --

EXEC [catalog].[disable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```

## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  

## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor 

## <a name="errors-and-warnings"></a>Erros e avisos
O procedimento armazenado retorna um erro se a ID do agente de trabalho não é válida.

