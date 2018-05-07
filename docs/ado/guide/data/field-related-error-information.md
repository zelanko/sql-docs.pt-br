---
title: Informações de erro relacionada ao campo | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- field-related errors [ADO]
- errors [ADO], field-related
ms.assetid: 5e7b1af4-996b-47c5-9161-c5575ad4fec9
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b53698e1042af197db9d9fa7ddfc4af555721607
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="field-related-error-information"></a>Informações de erro relacionada ao campo
Se o erro está relacionado diretamente a um campo — por exemplo, se os dados estão ausentes ou se ele é do tipo errado para o campo — você pode recuperar mais informações sobre a causa do problema examinando o **campo** do objeto **Status**  propriedade. Essa propriedade foi aprimorada para fornecer informações específicas sobre o problema. Assim, por exemplo, quando uma chamada para **UpdateBatch** falhar, a causa do problema pode ser determinada examinando o **Status** propriedade o **campos** em cada uma da afetados registros. A propriedade conterá um dos valores a **FieldStatusEnum** constante. A tabela a seguir inclui os valores que são de interesse específico quando ocorre um erro.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adFieldCantConvertValue**|2|Indica que o campo não pode ser recuperado ou armazenado sem perda de dados.|  
|**adFieldDataOverflow**|6|Indica que os dados retornados do provedor estouraram o tipo de dados do campo.|  
|**adFieldDefault**|13|Indica que o valor padrão para o campo foi usado ao definir os dados.|  
|**adFieldIgnore**|15|Indica que esse campo foi ignorado quando os valores na fonte de dados de configuração. Nenhum valor foi definido pelo provedor.|  
|**adFieldIntegrityViolation**|10|Indica que o campo não pode ser modificado porque é uma entidade calculada ou derivada.|  
|**adFieldIsNull**|3|Indica que o provedor retornou um valor nulo.|  
|**adFieldOutOfSpace**|22|Indica que o provedor não é possível obter o espaço de armazenamento suficiente para concluir a movimentação ou a operação de cópia.|
