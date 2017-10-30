---
title: Catalog.add_execution_worker (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d587cedd-6402-4d5c-9526-7cd25627a037
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8ce83f2678a1f3dcae6539f33beb33070b8e771b
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="catalogaddexecutionworker-ssisdb-database"></a>Catalog.add_execution_worker (banco de dados SSISDB)
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

Adiciona um [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] escala Out trabalho a uma instância de execução em expansão.

## <a name="syntax"></a>Sintaxe

```sql
catalog.add_execution_worker [@execution_id = ] execution_id, [@workeragent_id = ] workeragent_id
```

## <a name="arguments"></a>Argumentos
[ @execution_id =] *execution_id*  
 O identificador exclusivo da instância de execução. O *execution_id* é **bigint**.  
 
[@workeragent_id =] *workeragent_id*  
A id do agente de trabalho de um trabalho de fora de escala. O *workeragent_id* é **uniqueIdentifier**.

## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  

## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e MODIFY na instância de execução  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
 
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
 
- O usuário não tem as permissões apropriadas.

- O identificador da execução não é válido.

- A id do agente de trabalho não é válida.

- A execução não está em expansão.

## <a name="see-also"></a>Consulte também
[Executar pacotes em expansão](~/integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md).


