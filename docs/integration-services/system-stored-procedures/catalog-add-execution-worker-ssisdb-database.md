---
description: catalog.add_execution_worker (Banco de dados SSISDB)
title: catalog.add_execution_worker (Banco de dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d587cedd-6402-4d5c-9526-7cd25627a037
author: chugugrace
ms.author: chugu
monikerRange: '>= sql-server-2017'
ms.openlocfilehash: 905913f8728f82a14de1ed2aadf0e2e496946dd4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460589"
---
# <a name="catalogadd_execution_worker-ssisdb-database"></a>catalog.add_execution_worker (Banco de dados SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE[sqlserver2017](../../includes/applies-to-version/sqlserver2017.md)]

Adiciona um Trabalho do Scale Out do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a uma instância de execução no Scale Out.

## <a name="syntax"></a>Sintaxe

```sql
catalog.add_execution_worker [ @execution_id = ] execution_id, [ @workeragent_id = ] workeragent_id
```

## <a name="arguments"></a>Argumentos
[ @execution_id = ] *execution_id*  
 O identificador exclusivo da instância de execução. O *execution_id* é **bigint**.  
 
[@workeragent_id = ] *workeragent_id*  
A ID do agente de trabalho de um Trabalho do Scale Out. O *workeragent_id* é **uniqueIdentifier**.

## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  

## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e MODIFY na instância de execução  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
 
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
 
- O usuário não tem as permissões apropriadas.

- O identificador da execução não é válido.

- A ID do agente de trabalho não é válida.

- A execução não está no Scale Out.

## <a name="see-also"></a>Consulte Também
[Execute pacotes no Scale Out](~/integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md).

