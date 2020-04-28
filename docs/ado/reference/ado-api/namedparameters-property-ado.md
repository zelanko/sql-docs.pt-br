---
title: Propriedade namedParameters (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::NamedParameters
helpviewer_keywords:
- NamedParameters property [ADO]
ms.assetid: 42409387-026c-435f-a9b1-bf4167095875
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d63c413ebed585782ca5ce0568119dd7e05bf8ac
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932069"
---
# <a name="namedparameters-property-ado"></a>Propriedade NamedParameters (ADO)
Indica se os nomes de parâmetro devem ser passados para o provedor.  
  
## <a name="remarks"></a>Comentários  
 Quando essa propriedade é true, o ADO passa o valor da propriedade **Name** de cada parâmetro na coleção de **parâmetros** para o [objeto Command](../../../ado/reference/ado-api/command-object-ado.md). O provedor usa um nome de parâmetro para corresponder parâmetros nas propriedades **CommandText** ou **CommandStream** . Se essa propriedade for false (o padrão), os nomes de parâmetros serão ignorados e o provedor usará a ordem dos parâmetros para corresponder valores aos parâmetros nas propriedades **CommandText** ou **CommandStream** .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [Propriedade CommandStream (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Coleção Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
