---
description: Propriedade Precision (ADOX)
title: Propriedade Precision (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::put_Precision
- _Column::PutPrecision
- _Column::GetPrecision
- _Column::get_Precision
- _Column::Precision
helpviewer_keywords:
- Precision property [ADOX]
ms.assetid: 0e0ecbbf-d7de-49d4-a128-5a519ecd54ba
author: rothja
ms.author: jroth
ms.openlocfilehash: 4f0126da4e68ee84d9a8f155ee1dc50a89ab4646
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983707"
---
# <a name="precision-property-adox"></a>Propriedade Precision (ADOX)
Indica a precisão máxima dos valores de dados na [coluna](./column-object-adox.md).  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define e retorna um valor **longo** que é a precisão máxima de valores de dados na coluna quando a propriedade [Type](./type-property-column-adox.md) é um tipo numérico. A **precisão** é ignorada para todos os outros tipos de dados.  
  
## <a name="remarks"></a>Comentários  
 O valor padrão é zero (**0**).  
  
 Esta propriedade é somente leitura para objetos de [coluna](./column-object-adox.md) já anexados a uma coleção.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Column (ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de código ADOX: exemplo de propriedades NumericScale e Precision (VB)](./adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Propriedade Type (coluna) (ADOX)](./type-property-column-adox.md)   
 [Objeto Column (ADOX)](./column-object-adox.md)