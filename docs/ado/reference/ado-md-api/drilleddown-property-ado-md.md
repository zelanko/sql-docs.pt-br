---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f1175d2a70c376e3da1e079e4a3eb93a39235758
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67938464"
---
# <a name="drilleddown-property-ado-md"></a>Propriedade DrilledDown (ADO MD)
Indica se os filhos seguem imediatamente o [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) no eixo.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um valor **booliano** e é somente leitura. **DrilledDown** retornará **true** se não houver membros filho do membro atual no eixo. **DrilledDown** retornará **false** se o membro atual tiver um ou mais membros filho no eixo.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **DrilledDown** para determinar se há pelo menos um filho deste membro no eixo imediatamente após este membro. Essas informações são úteis ao exibir o membro.  
  
 Só há suporte para essa propriedade em objetos [Membros](../../../ado/reference/ado-md-api/member-object-ado-md.md) que pertencem a um objeto [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md) . Um erro ocorre quando essa propriedade é referenciada de objetos de **membro** que pertencem a um objeto de [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade ParentSameAsPrev (ADO MD)](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)
