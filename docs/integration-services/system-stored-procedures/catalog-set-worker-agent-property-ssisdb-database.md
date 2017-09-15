---
title: Catalog.set_worker_agent_property (banco de dados SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ddd2a534-6925-4d66-90e7-541c14f41de7
caps.latest.revision: 2
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: d0476bbb67cff44a05aed1441a31d679882b4cb3
ms.contentlocale: pt-br
ms.lasthandoff: 09/08/2017

---
# <a name="catalogsetworkeragentproperty-ssisdb-database"></a>Catalog.set_worker_agent_property (banco de dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Define a propriedade de um [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] escala fora do trabalho.

## <a name="syntax"></a>Sintaxe

```tsql
set_worker_agent_property [ @WorkerAgentId = ] WorkerAgentId, [ @PropertyName = ] PropertyName, [ @PropertyValue = ] PropertyValue 
```

## <a name="arguments"></a>Argumentos
[ @WorkerAgentId =] *WorkerAgentId*  
A id do agente de trabalho da escala fora do trabalho. O *WorkerAgentId* é **uniqueidentifier**.

[ @PropertyName =] *PropertyName*  
O nome da propriedade. O *PropertyName* é **nvarchar (256)**.

[ @PropertyValue =] *PropertyValue*  
O valor da propriedade. O *PropertyValue* é **nvarchar (max)**.

## <a name="remarks"></a>Comentários
Os nomes de propriedades válidos são **DisplayName**, **descrição**, **marcas**.

## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  

## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor

## <a name="erros-and-warnings"></a>Erros e avisos
  A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   O usuário não tem as permissões apropriadas 

-   A id do agente de trabalho não é válida.

-   O nome da propriedade não é válido.

-   O valor da propriedade não é vilid.  
