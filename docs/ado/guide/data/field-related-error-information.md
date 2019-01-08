---
title: Informações de erro relacionadas ao campo | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- field-related errors [ADO]
- errors [ADO], field-related
ms.assetid: 5e7b1af4-996b-47c5-9161-c5575ad4fec9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2ba956d2e442c914ddc50f2f023f225252fb1295
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52524504"
---
# <a name="field-related-error-information"></a>Informações de erro relacionadas ao campo
Se um erro está diretamente relacionado a um campo - por exemplo, se os dados estão ausentes ou se ele é do tipo incorreto para o campo - você pode recuperar mais informações sobre a causa do problema examinando os **campo** do objeto **Status**  propriedade. Essa propriedade foi aprimorada para fornecer informações específicas sobre o problema. Portanto, por exemplo, quando uma chamada para **UpdateBatch** falhar, a causa do problema pode ser determinado examinando a **Status** propriedade do **campos** em cada uma da afetados registros. A propriedade conterá um dos valores de **FieldStatusEnum** constante. A tabela a seguir inclui os valores que são de especial interesse quando ocorre um erro.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adFieldCantConvertValue**|2|Indica que o campo não pode ser recuperado ou armazenado sem perda de dados.|  
|**adFieldDataOverflow**|6|Indica que a retornada do provedor de dados estouraram o tipo de dados do campo.|  
|**adFieldDefault**|13|Indica que o valor padrão para o campo foi usado ao definir os dados.|  
|**adFieldIgnore**|15|Indica que esse campo foi ignorado quando valores na fonte de dados de configuração. Nenhum valor foi definido pelo provedor.|  
|**adFieldIntegrityViolation**|10|Indica que o campo não pode ser modificado porque é uma entidade calculada ou derivada.|  
|**adFieldIsNull**|3|Indica que o provedor retornou um valor nulo.|  
|**adFieldOutOfSpace**|22|Indica que o provedor é não é possível obter espaço de armazenamento suficiente para concluir uma movimentação ou a operação de cópia.|
