---
title: Propriedade AbsolutePosition (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AbsolutePosition
helpviewer_keywords:
- AbsolutePosition property [ADO]
ms.assetid: 79f8ee5e-fc70-46d8-8c29-ebf943c66592
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4444c54df6e3629e7f69e3fe0d54625f66c3e703
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63155175"
---
# <a name="absoluteposition-property-ado"></a>Propriedade AbsolutePosition (ADO)
Indica a posição ordinal de um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) registro atual do objeto.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Para o código de 32 bits, define ou retorna um **longo** valor entre 1 e o número de registros na **conjunto de registros** objeto ([RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)), ou retorna um do [ PositionEnum](../../../ado/reference/ado-api/positionenum.md) valores.  
  
 Para o código de 64 bits, use um tipo de dados que fornece armazenamento de um valor de 64 bits. Por exemplo, você pode usar longa ou outro valor que é o comprimento de 64 bits como DBORDINAL. Não use **PositionEnum** valores, pois eles são limitados a 32 bits de comprimento.  
  
## <a name="remarks"></a>Comentários  
 Para definir a **AbsolutePosition** propriedade, o ADO requer que o provedor OLE DB que você está usando é implementar a [IRowsetLocate:IRowset](https://msdn.microsoft.com/library/windows/desktop/ms721190.aspx) interface.  
  
 Acessando o **AbsolutePosition** propriedade de uma **conjunto de registros** que foi aberto com um somente de avanço ou cursor dinâmico gera o erro **adErrFeatureNotAvailable**. Com outros tipos de cursor, a posição correta será retornada desde que o provedor OLE DB oferece suporte a **IRowsetScroll:IRowsetLocate** interface. Se o provedor não dá suporte a **IRowsetScroll** interface, a propriedade é definida como **adPosUnknown**. Consulte a documentação do seu provedor para determinar se ele suporta **IRowsetScroll**.  
  
 Use o **AbsolutePosition** propriedade a ser movido para um registro com base em sua posição ordinal na **Recordset** objeto, ou para determinar a posição ordinal do registro atual. O provedor deve oferecer suporte a funcionalidade apropriada para essa propriedade estar disponível.  
  
 Como o [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) propriedade **AbsolutePosition** é baseado em 1 e é igual a 1 quando o registro atual é o primeiro registro na **conjunto de registros**. Você pode obter o número total de registros no **conjunto de registros** de objeto de [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) propriedade.  
  
 Quando você define o **AbsolutePosition** propriedade, mesmo se for para um registro no cache atual, ADO recarrega o cache com um novo grupo de registros que começam com o registro especificado. O [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) propriedade determina o tamanho desse grupo.  
  
> [!NOTE]
>  Você não deve usar o **AbsolutePosition** a propriedade como um número de registro de substituto. A posição de um determinado registro muda quando você exclui um registro anterior. Também não há nenhuma garantia de que um determinado registro têm a mesma **AbsolutePosition** se o **Recordset** objeto será novamente consultado ou reaberto. Indicadores ainda são a maneira recomendada de reter e retornar para uma determinada posição e são a única maneira de posicionamento em todos os tipos de **Recordset** objetos.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de AbsolutePosition e CursorLocation exemplo das propriedades (VB)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vb.md)   
 [Exemplo de AbsolutePosition e CursorLocation propriedades (VC + +)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vc.md)   
 [Propriedade AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [Propriedade RecordCount (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
