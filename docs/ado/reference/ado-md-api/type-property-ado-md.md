---
description: Propriedade Type (ADO MD)
title: Propriedade Type (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 52b07fe68f905c7f27bad4685d5df56c25cb2c13
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985967"
---
# <a name="type-property-ado-md"></a>Propriedade Type (ADO MD)
Indica o tipo do [membro](./member-object-ado-md.md)atual.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um valor [MemberTypeEnum](./membertypeenum.md) e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 Essa propriedade tem suporte apenas em objetos [Membros](./member-object-ado-md.md) que pertencem a um objeto de [nível](./level-object-ado-md.md) . Um erro ocorre quando essa propriedade é referenciada de objetos **Membros** que pertencem a um objeto [Position](./position-object-ado-md.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Member (ADO MD)](./member-object-ado-md.md)