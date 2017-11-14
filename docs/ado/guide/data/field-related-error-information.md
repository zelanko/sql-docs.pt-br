---
title: "Informações de erro relacionada ao campo | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- field-related errors [ADO]
- errors [ADO], field-related
ms.assetid: 5e7b1af4-996b-47c5-9161-c5575ad4fec9
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3a7609b4c4a0d67f1bade86c2e6ec3bb66b07553
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="field-related-error-information"></a>Informações de erro relacionada ao campo
Se o erro está relacionado diretamente a um campo — por exemplo, se os dados estão ausentes ou se ele é do tipo errado para o campo — você pode recuperar mais informações sobre a causa do problema examinando o **campo** do objeto **Status**  propriedade. Essa propriedade foi aprimorada para fornecer informações específicas sobre o problema. Assim, por exemplo, quando uma chamada para **UpdateBatch** falhar, a causa do problema pode ser determinada examinando o **Status** propriedade o **campos** em cada uma da afetados registros. A propriedade conterá um dos valores a **FieldStatusEnum** constante. A tabela a seguir inclui os valores que são de interesse específico quando ocorre um erro.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adFieldCantConvertValue**|2|Indica que o campo não pode ser recuperado ou armazenado sem perda de dados.|  
|**adFieldDataOverflow**|6|Indica que os dados retornados do provedor estouraram o tipo de dados do campo.|  
|**adFieldDefault**|13|Indica que o valor padrão para o campo foi usado ao definir os dados.|  
|**adFieldIgnore**|15|Indica que esse campo foi ignorado quando os valores na fonte de dados de configuração. Nenhum valor foi definido pelo provedor.|  
|**adFieldIntegrityViolation**|10|Indica que o campo não pode ser modificado porque é uma entidade calculada ou derivada.|  
|**adFieldIsNull**|3|Indica que o provedor retornou um valor nulo.|  
|**adFieldOutOfSpace**|22|Indica que o provedor não é possível obter o espaço de armazenamento suficiente para concluir a movimentação ou a operação de cópia.|

