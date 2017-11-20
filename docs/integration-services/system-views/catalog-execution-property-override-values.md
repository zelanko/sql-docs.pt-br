---
title: Catalog.execution_property_override_values | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 83cbdd6f-ddde-47bf-abde-36bd24272621
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ed9ae4ea7a7165efe53a551832d8e4a0eb7a2114
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogexecutionpropertyoverridevalues"></a>catalog.execution_property_override_values
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe os valores de substituição de propriedade que foram definidos durante a execução do pacote.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|property_id|**bigint**|ID exclusiva do valor de substituição de propriedade.|  
|execution_id|**bigint**|ID exclusivo da instância de execução.|  
|property_path|**nvarchar(4000)**|O caminho para a propriedade no pacote.|  
|property_value|**nvarchar(max)**|O valor de substituição da propriedade.|  
|sensitive|**bit**|Quando o valor for 1, a propriedade será confidencial e criptografada quando for armazenada. Quando o valor for 0, a propriedade não será confidencial e o valor será armazenado em texto não criptografado.|  
  
## <a name="remarks"></a>Comentários  
 Essa exibição mostra uma linha para cada execução no qual propriedade valores foram substituídos usando o **substituições de propriedade** seção o **avançado** guia do **executar pacote** caixa de diálogo. O caminho para a propriedade é derivado de **caminho de pacote** propriedade da tarefa de pacote.  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na instância de execução  
  
-   Associação de **ssis_admin** função de banco de dados  
  
-   Associação de **sysadmin** função de servidor  
  
> [!NOTE]  
>  Quando você tem permissão para executar uma operação no servidor, também tem permissão para exibir informações sobre a operação. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  

