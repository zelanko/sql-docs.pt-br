---
title: catalog.disable_worker_agent (banco de dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3f19dc4c-a000-4318-8fe1-e80d56720e66
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 86243f3f2cc79baf322ee628e9fc4b651217906f
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35407528"
---
# <a name="catalogdisableworkeragent-ssisdb-database"></a>catalog.disable_worker_agent (banco de dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Desabilite um Trabalho do Scale Out para o Mestre do Scale Out que trabalha com este catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].

## <a name="syntax"></a>Sintaxe

```sql
catalog.disable_worker_agent [@WorkerAgentId =] WorkerAgentId
```
## <a name="arguments"></a>Argumentos
[@WorkerAgentId =] *WorkerAgentId* A ID do agente do Trabalho do Scale Out. O *WorkerAgentId* é **uniqueidentifier**.

## <a name="example"></a>Exemplo
Este exemplo desabilita o Trabalho do Scale Out em MachineA.

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
 Nenhum  

## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin** 

## <a name="errors-and-warnings"></a>Erros e avisos
Se a ID do agente de trabalho não é válida, o procedimento armazenado retorna um erro.
