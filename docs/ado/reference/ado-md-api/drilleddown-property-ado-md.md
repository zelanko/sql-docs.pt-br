---
description: Propriedade DrilledDown (ADO MD)
title: Propriedade DrilledDown (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DrilledDown
- Member::DrilledDown
helpviewer_keywords:
- DrilledDown property [ADO MD]
ms.assetid: bf39dd36-fc7a-4f6e-86c0-fa71430c0d86
author: rothja
ms.author: jroth
ms.openlocfilehash: 7560f7f2c487f42d26d83236d824bf997b4f49d1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778145"
---
# <a name="drilleddown-property-ado-md"></a>Propriedade DrilledDown (ADO MD)
Indica se os filhos seguem imediatamente o [membro](./member-object-ado-md.md) no eixo.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um valor **booliano** e é somente leitura. **DrilledDown** retornará **true** se não houver membros filho do membro atual no eixo. **DrilledDown** retornará **false** se o membro atual tiver um ou mais membros filho no eixo.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **DrilledDown** para determinar se há pelo menos um filho deste membro no eixo imediatamente após este membro. Essas informações são úteis ao exibir o membro.  
  
 Só há suporte para essa propriedade em objetos [Membros](./member-object-ado-md.md) que pertencem a um objeto [Position](./position-object-ado-md.md) . Um erro ocorre quando essa propriedade é referenciada de objetos de **membro** que pertencem a um objeto de [nível](./level-object-ado-md.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Member (ADO MD)](./member-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade ParentSameAsPrev (ADO MD)](./parentsameasprev-property-ado-md.md)