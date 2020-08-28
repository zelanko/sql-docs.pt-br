---
description: MemberTypeEnum
title: MemberTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 441430cd164be017779afc54ba9af866edaea874
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986257"
---
# <a name="membertypeenum"></a>MemberTypeEnum
Especifica a configuração da propriedade [Type](./type-property-ado-md.md) de um objeto [membro](./member-object-ado-md.md) .  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adMemberAll**|4|Indica que o objeto de **membro** representa todos os membros do nível.|  
|**adMemberFormula**|3|Indica que o objeto de **membro** é calculado usando uma expressão de fórmula.|  
|**adMemberMeasure**|2|Indica que o objeto **membro** pertence à dimensão medidas e representa um atributo quantitativo.|  
|**adMemberRegular**|1|Padrão. Indica que o objeto de **membro** representa uma instância de uma entidade de negócios.|  
|**adMemberUnknown**|0|Não é possível determinar o tipo do membro.|