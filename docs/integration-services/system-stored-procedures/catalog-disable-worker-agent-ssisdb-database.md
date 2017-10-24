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
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 8f4a8cd24278742ffb13d16791ce5f1f3a95f301
ms.contentlocale: pt-br
ms.lasthandoff: 10/20/2017

---
# <a name="catalogdisableworkeragent-ssisdb-database"></a>Catalog.disable_worker_agent (banco de dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Desabilitar um trabalho de fora de escala para escala Out mestre funcionam com essa [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] catálogo.

## <a name="syntax"></a>Sintaxe

```sql
catalog.disable_worker_agent [@WorkerAgentId =] WorkerAgentId
```
## <a name="arguments"></a>Argumentos
[@WorkerAgentId =] *WorkerAgentId* o agente de trabalho ID de escala Out trabalhador. O *WorkerAgentId* é **uniqueidentifier**.

## <a name="example"></a>Exemplo
Este exemplo desabilita a escala Out trabalho no computador.

```sql
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
Se a ID do agente de trabalho não é válida, o procedimento armazenado retornará um erro.

