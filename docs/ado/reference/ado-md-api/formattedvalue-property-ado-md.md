---
description: Propriedade FormattedValue (ADO MD)
title: Propriedade FormattedValue (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell::FormattedValue
- FormattedValue
helpviewer_keywords:
- FormattedValue property [ADO MD]
ms.assetid: 5c06451e-06ec-4da6-9a87-2d043469248a
author: rothja
ms.author: jroth
ms.openlocfilehash: 5905b4aba040505c60fa78721718b3ab03c51622
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986697"
---
# <a name="formattedvalue-property-ado-md"></a>Propriedade FormattedValue (ADO MD)
Indica a exibição formatada de um valor de [célula](./cell-object-ado-md.md) .  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna uma **cadeia de caracteres** e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **FormattedValue** para obter o valor de exibição formatado da propriedade [Value](./value-property-ado-md.md) de um objeto [Cell](./cell-object-ado-md.md) . Por exemplo, se o valor de uma célula fosse 1056,87, e esse valor representou um valor de dólar, **FormattedValue** seria $1056.87.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Cell (ADO MD)](./cell-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de células (VB)](./cellset-example-vb.md)   
 [Propriedade Value (ADO MD)](./value-property-ado-md.md)