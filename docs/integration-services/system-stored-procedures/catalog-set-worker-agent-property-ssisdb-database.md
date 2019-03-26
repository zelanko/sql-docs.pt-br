---
title: catalog.set_worker_agent_property (banco de dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ddd2a534-6925-4d66-90e7-541c14f41de7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a3069bcda85895297626c3f1ec691381e8f071ab
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58270964"
---
# <a name="catalogsetworkeragentproperty-ssisdb-database"></a>catalog.set_worker_agent_property (banco de dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Define a propriedade de um Trabalho do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out.

## <a name="syntax"></a>Sintaxe

```sql
catalog.set_worker_agent_property [@WorkerAgentId =] WorkerAgentId, [@PropertyName =] PropertyName, [@PropertyValue =] PropertyValue 
```

## <a name="arguments"></a>Argumentos
[@WorkerAgentId =] *WorkerAgentId*  
A ID do agente de trabalho do Trabalhador do Scale Out. O *WorkerAgentId* é **uniqueidentifier**.

[@PropertyName =] *PropertyName*  
O nome da propriedade. O *PropertyName* é **nvarchar(256)**.

[@PropertyValue =] *PropertyValue*  
O valor da propriedade. O *PropertyValue* é **nvarchar(max)**.

## <a name="remarks"></a>Remarks
Os nomes de propriedade válidos são **DisplayName**, **Description** e **Tags**.

## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  

## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**

## <a name="errors-and-warnings"></a>Erros e avisos
  A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   O usuário não tem as permissões apropriadas 

-   A ID do agente de trabalho não é válida.

-   O nome da propriedade não é válido.

-   O valor da propriedade não é válido.  
