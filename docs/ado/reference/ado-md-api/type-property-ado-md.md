---
description: Propriedade Type (ADO MD)
title: Propriedade Type (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Type
- Type
helpviewer_keywords:
- Type property [ADO MD]
ms.assetid: 34698910-64b9-41d8-8531-9de12f2b1e32
author: rothja
ms.author: jroth
ms.openlocfilehash: 30cf3c161e30884d370aea0fefd81260bafe141e
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777815"
---
# <a name="type-property-ado-md"></a>Propriedade Type (ADO MD)
Indica o tipo do [membro](./member-object-ado-md.md)atual.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um valor [MemberTypeEnum](./membertypeenum.md) e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 Essa propriedade tem suporte apenas em objetos [Membros](./member-object-ado-md.md) que pertencem a um objeto de [nível](./level-object-ado-md.md) . Um erro ocorre quando essa propriedade é referenciada de objetos **Membros** que pertencem a um objeto [Position](./position-object-ado-md.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Member (ADO MD)](./member-object-ado-md.md)