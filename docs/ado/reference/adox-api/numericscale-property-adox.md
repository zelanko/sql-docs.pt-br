---
title: Propriedade NumericScale (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::PutNumericScale
- _Column::GetNumericScale
- _Column::NumericScale
- _Column::put_NumericScale
- _Column::get_NumericScale
helpviewer_keywords:
- NumericScale property [ADOX]
ms.assetid: 573ee5d1-57c7-4a27-be79-a0e12944ad9b
author: rothja
ms.author: jroth
ms.openlocfilehash: a0a0090a24207e6faad1b14aa3cb5afd6091bc87
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763807"
---
# <a name="numericscale-property-adox"></a>Propriedade NumericScale (ADOX)
Indica a escala de um valor numérico na coluna.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define e retorna um valor de **byte** que é a escala de valores de dados na coluna quando a propriedade [Type](../../../ado/reference/adox-api/type-property-column-adox.md) é **adNumeric** ou **adDecimal**. **NumericScale** é ignorado para todos os outros tipos de dados.  
  
## <a name="remarks"></a>Comentários  
 O valor padrão é zero (0).  
  
 **NumericScale** é somente leitura para objetos de [coluna](../../../ado/reference/adox-api/column-object-adox.md) já anexados a uma coleção.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de código ADOX: exemplo de propriedades NumericScale e Precision (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Propriedade Type (Column) (ADOX)](../../../ado/reference/adox-api/type-property-column-adox.md)
