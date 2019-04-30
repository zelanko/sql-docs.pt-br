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
manager: craigg
ms.openlocfilehash: efdbd68bf464fea3a0d59396380b082eb66375b8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63156579"
---
# <a name="absolutepage-property-ado"></a>Propriedade AbsolutePage (ADO)
Indica em qual página de registro atual reside.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Para o código de 32 bits, define ou retorna um **longo** valor entre 1 e o número de páginas na [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto ([PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)), ou retorna um do [PositionEnum ](../../../ado/reference/ado-api/positionenum.md) valores.  
  
 Para o código de 64 bits, use um tipo de dados que fornece armazenamento de um valor de 64 bits. Por exemplo, você pode usar qualquer uma **longo** ou outro valor que pode ser o comprimento de 64 bits como DBORDINAL. Não use **PositionEnum** valores porque eles são limitados a 32 bits de comprimento.  
  
## <a name="remarks"></a>Comentários  
 Essa propriedade pode ser usada para identificar o número de página em que o registro atual está localizado. Ele usa o [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) propriedade logicamente dividir a contagem total de linhas da **conjunto de registros** objeto em uma série de páginas, cada qual com o número de registros iguais a **PageSize** (exceto a última página, que pode ter menos registros). O provedor deve oferecer suporte a funcionalidade apropriada para essa propriedade estar disponível.  
  
-   Ao obter ou definir a **AbsolutePage** propriedade, o ADO usa o [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) propriedade e o [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) propriedade juntos da seguinte maneira:  
  
-   Para obter o **AbsolutePage**, ADO primeiro recupera o **AbsolutePosition**e, em seguida, divide pela **PageSize**.  
  
-   Para definir a **AbsolutePage**, ADO move a **AbsolutePosition** da seguinte maneira: ele multiplica o **PageSize** pelo novo **AbsolutePage** valor e, em seguida, adiciona 1 ao valor. Como resultado, a posição atual na **conjunto de registros** depois de configurar com êxito **AbsolutePage** é o primeiro registro na página.  
  
 Como o **AbsolutePosition** propriedade **AbsolutePage** é baseado em 1 e é igual a 1 quando o registro atual é o primeiro registro na **conjunto de registros**. Defina essa propriedade para mover para o primeiro registro de uma página específica. Obter o número total de páginas a partir de **PageCount** propriedade.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [AbsolutePage, PageCount, PageSize exemplo das propriedades e (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage, PageCount, PageSize exemplo das propriedades e (VC + +)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [Propriedade AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [Propriedade PageCount (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)   
 [Propriedade PageSize (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)
