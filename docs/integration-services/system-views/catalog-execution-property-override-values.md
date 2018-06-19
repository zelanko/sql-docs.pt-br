---
title: catalog.execution_property_override_values | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 83cbdd6f-ddde-47bf-abde-36bd24272621
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 787baa21f2039647084b271a7cb63c681b6e7438
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35409828"
---
# <a name="catalogexecutionpropertyoverridevalues"></a>catalog.execution_property_override_values
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe os valores de substituição de propriedade que foram definidos durante a execução do pacote.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|property_id|**bigint**|ID exclusiva do valor de substituição de propriedade.|  
|execution_id|**bigint**|ID exclusivo da instância de execução.|  
|property_path|**nvarchar(4000)**|O caminho para a propriedade no pacote.|  
|property_value|**nvarchar(max)**|O valor de substituição da propriedade.|  
|sensitive|**bit**|Quando o valor for 1, a propriedade será confidencial e criptografada quando for armazenada. Quando o valor for 0, a propriedade não será confidencial e o valor será armazenado em texto não criptografado.|  
  
## <a name="remarks"></a>Remarks  
 Essa exibição mostra uma linha para cada execução em que os valores de propriedade foram substituídos usando a seção **Substituições de propriedade** na guia **Avançado** da caixa de diálogo **Executar Pacote**. O caminho para a propriedade é derivado da propriedade **Caminho do Pacote** da tarefa de pacote.  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na instância de execução  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
> [!NOTE]  
>  Quando você tem permissão para executar uma operação no servidor, também tem permissão para exibir informações sobre a operação. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  
