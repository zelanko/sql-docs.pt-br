---
title: Informações de erro relacionadas a campo | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e61850ca788f6cff11d2a665000f68b89cd3ed45
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758282"
---
# <a name="field-related-error-information"></a>Informações de erro relacionadas ao campo
Se um erro estiver diretamente relacionado a um campo, por exemplo, se os dados estiverem ausentes ou se forem do tipo incorreto para o campo – você poderá recuperar mais informações sobre a causa do problema examinando a propriedade **status** do objeto **Field** . Esta propriedade foi aprimorada para fornecer informações específicas sobre o problema. Portanto, por exemplo, quando uma chamada para **UpdateBatch** falha, a causa do problema pode ser determinada examinando a propriedade **status** dos **campos** em cada um dos registros afetados. A propriedade conterá um dos valores na constante **FieldStatusEnum** . A tabela a seguir inclui os valores que são de interesse particular quando ocorre um erro.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adFieldCantConvertValue**|2|Indica que o campo não pode ser recuperado ou armazenado sem perda de dados.|  
|**adFieldDataOverflow**|6|Indica que os dados retornados do provedor estouram o tipo de dados do campo.|  
|**adFieldDefault**|13|Indica que o valor padrão do campo foi usado ao definir dados.|  
|**adFieldIgnore**|15|Indica que esse campo foi ignorado ao definir valores de dados na origem. Nenhum valor foi definido pelo provedor.|  
|**adFieldIntegrityViolation**|10|Indica que o campo não pode ser modificado porque é uma entidade calculada ou derivada.|  
|**adFieldIsNull**|3|Indica que o provedor retornou um valor nulo.|  
|**adFieldOutOfSpace**|22|Indica que o provedor não pode obter espaço de armazenamento suficiente para concluir uma operação de movimentação ou cópia.|
