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
ms.openlocfilehash: 5b9795f962d0ead59a8d4f993e799a0ae4e2b750
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67921690"
---
# <a name="absoluteposition-property-ado"></a>Propriedade AbsolutePosition (ADO)
Indica a posição ordinal do registro atual de um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Para o código de 32 bits, o define ou retorna um valor **longo** de 1 para o número de registros no objeto **Recordset** ([RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)) ou retorna um dos valores [PositionEnum](../../../ado/reference/ado-api/positionenum.md) .  
  
 Para o código de 64 bits, use um tipo de dados que forneça o armazenamento de um valor de 64 bits. Por exemplo, você pode usar um valor Long ou outro que tenha tamanho de 64 bits, como DBORDINAL. Não use valores de **PositionEnum** , pois eles são limitados a comprimento de 32 bits.  
  
## <a name="remarks"></a>Comentários  
 Para definir a propriedade **AbsolutePosition** , o ADO requer que o provedor de OLE DB que você está usando implemente a interface [IRowsetLocate: IRowset](https://msdn.microsoft.com/library/windows/desktop/ms721190.aspx) .  
  
 O acesso à propriedade **AbsolutePosition** de um **conjunto de registros** que foi aberto com um cursor de somente avanço ou dinâmico gera o erro **adErrFeatureNotAvailable**. Com outros tipos de cursor, a posição correta será retornada contanto que o provedor de OLE DB dê suporte à interface **IRowsetScroll: IRowsetLocate** . Se o provedor não oferecer suporte à interface **IRowsetScroll** , a propriedade será definida como **adPosUnknown**. Consulte a documentação do seu provedor para determinar se ele oferece suporte a **IRowsetScroll**.  
  
 Use a propriedade **AbsolutePosition** para mover para um registro com base em sua posição ordinal no objeto **Recordset** ou para determinar a posição ordinal do registro atual. O provedor deve dar suporte à funcionalidade apropriada para que essa propriedade esteja disponível.  
  
 Como a propriedade [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) , **AbsolutePosition** é baseado em 1 e é igual a 1 quando o registro atual é o primeiro registro no **conjunto de registros**. Você pode obter o número total de registros no objeto **Recordset** da propriedade [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) .  
  
 Quando você define a propriedade **AbsolutePosition** , mesmo que seja para um registro no cache atual, o ADO recarrega o cache com um novo grupo de registros, começando com o registro especificado. A propriedade [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) determina o tamanho desse grupo.  
  
> [!NOTE]
>  Você não deve usar a propriedade **AbsolutePosition** como um número de registro substituto. A posição de um determinado registro é alterada quando você exclui um registro anterior. Também não há nenhuma garantia de que um determinado registro terá o mesmo **AbsolutePosition** se o objeto **Recordset** for reconsultado ou reaberto. Os indicadores ainda são a maneira recomendada de reter e retornar a uma determinada posição e são a única maneira de posicionar em todos os tipos de objetos **Recordset** .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades AbsolutePosition e CursorLocation (VB)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vb.md)   
 [Exemplo das propriedades AbsolutePosition e CursorLocation (VC + +)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vc.md)   
 [Propriedade AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [Propriedade RecordCount (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
