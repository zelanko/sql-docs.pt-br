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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938464"
---
# <a name="drilleddown-property-ado-md"></a>Propriedade DrilledDown (ADO MD)
Indica se filhos logo após o [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) no eixo.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um **Boolean** valor e é somente leitura. **DrilledDown** retorna **verdadeiro** se não houver nenhum membro filho do membro atual no eixo. **DrilledDown** retorna **falso** se o membro atual tiver um ou mais membros filhos no eixo.  
  
## <a name="remarks"></a>Comentários  
 Use o **DrilledDown** propriedade para determinar se há pelo menos um filho desse membro no eixo imediatamente após esse membro. Essa informação é útil ao exibir o membro.  
  
 Essa propriedade só é compatível com [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objetos que pertencem a um [posição](../../../ado/reference/ado-md-api/position-object-ado-md.md) objeto. Ocorre um erro quando essa propriedade é referenciada a partir **membro** objetos que pertencem a um [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md) objeto.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade ParentSameAsPrev (ADO MD)](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)
