---
title: Propriedade AbsolutePage (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AbsolutePage
helpviewer_keywords:
- AbsolutePage property [ADO]
ms.assetid: ddb58a35-ec3a-423c-a504-3c65e62c23d4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 12b2e6c6f12fc06cb223551b55cb7f9a38df9ac3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67921838"
---
# <a name="absolutepage-property-ado"></a>Propriedade AbsolutePage (ADO)
Indica em qual página o registro atual reside.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Para o código de 32 bits, o define ou retorna um valor **longo** de 1 para o número de páginas no objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) ([PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)) ou retorna um dos valores de [PositionEnum](../../../ado/reference/ado-api/positionenum.md) .  
  
 Para o código de 64 bits, use um tipo de dados que forneça o armazenamento de um valor de 64 bits. Por exemplo, você pode usar um valor **longo** ou outro que pode ter comprimento de 64 bits, como DBORDINAL. Não use valores de **PositionEnum** porque eles são limitados a comprimento de 32 bits.  
  
## <a name="remarks"></a>Comentários  
 Essa propriedade pode ser usada para identificar o número de página no qual o registro atual está localizado. Ele usa a propriedade [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) para dividir logicamente a contagem total de conjunto de linhas do objeto **Recordset** em uma série de páginas, cada uma com o número de registros igual a **PageSize** (exceto a última página, que pode ter menos registros). O provedor deve dar suporte à funcionalidade apropriada para que essa propriedade esteja disponível.  
  
-   Ao obter ou definir a propriedade **AbsolutePage** , o ADO usa a propriedade [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) e a propriedade [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) juntas da seguinte maneira:  
  
-   Para obter o **AbsolutePage**, o ADO primeiro recupera o **AbsolutePosition**e, em seguida, divide-o pelo **PageSize**.  
  
-   Para definir o **AbsolutePage**, o ADO move o **AbsolutePosition** da seguinte maneira: ele multiplica o **PageSize** pelo novo valor **AbsolutePage** e, em seguida, adiciona 1 ao valor. Como resultado, a posição atual no conjunto de **registros** após a definição bem-sucedida de **AbsolutePage** é o primeiro registro nessa página.  
  
 Como a propriedade **AbsolutePosition** , **AbsolutePage** é baseado em 1 e é igual a 1 quando o registro atual é o primeiro registro no **conjunto de registros**. Defina essa propriedade para mover para o primeiro registro de uma página específica. Obtenha o número total de páginas da propriedade **PageCount** .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades AbsolutePage, PageCount e PageSize (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [Exemplo das propriedades AbsolutePage, PageCount e PageSize (VC + +)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [Propriedade AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [Propriedade PageCount (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)   
 [Propriedade PageSize (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)
