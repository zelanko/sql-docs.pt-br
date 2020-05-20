---
title: MemberTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- MemberTypeEnum
helpviewer_keywords:
- MemberTypeEnum enumeration [ADO MD]
ms.assetid: 5d8132c0-7ca2-4f86-8336-1b34213869ad
author: rothja
ms.author: jroth
ms.openlocfilehash: 7e05d8307f4dca4479b407db7364ab4d893d684e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765137"
---
# <a name="membertypeenum"></a>MemberTypeEnum
Especifica a configuração da propriedade [Type](../../../ado/reference/ado-md-api/type-property-ado-md.md) de um objeto [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) .  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adMemberAll**|4|Indica que o objeto de **membro** representa todos os membros do nível.|  
|**adMemberFormula**|3|Indica que o objeto de **membro** é calculado usando uma expressão de fórmula.|  
|**adMemberMeasure**|2|Indica que o objeto **membro** pertence à dimensão medidas e representa um atributo quantitativo.|  
|**adMemberRegular**|1|Padrão. Indica que o objeto de **membro** representa uma instância de uma entidade de negócios.|  
|**adMemberUnknown**|0|Não é possível determinar o tipo do membro.|
