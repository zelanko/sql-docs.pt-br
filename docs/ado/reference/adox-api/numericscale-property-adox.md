---
description: Propriedade NumericScale (ADOX)
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
ms.openlocfilehash: 3420a3e3d1e6ee06eaa63926604f3688b3f0590b
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769905"
---
# <a name="numericscale-property-adox"></a>Propriedade NumericScale (ADOX)
Indica a escala de um valor numérico na coluna.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define e retorna um valor de **byte** que é a escala de valores de dados na coluna quando a propriedade [Type](./type-property-column-adox.md) é **adNumeric** ou **adDecimal**. **NumericScale** é ignorado para todos os outros tipos de dados.  
  
## <a name="remarks"></a>Comentários  
 O valor padrão é zero (0).  
  
 **NumericScale** é somente leitura para objetos de [coluna](./column-object-adox.md) já anexados a uma coleção.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Column (ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de código ADOX: exemplo de propriedades NumericScale e Precision (VB)](./adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Propriedade Type (Column) (ADOX)](./type-property-column-adox.md)