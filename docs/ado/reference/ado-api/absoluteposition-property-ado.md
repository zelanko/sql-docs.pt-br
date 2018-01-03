---
title: Propriedade AbsolutePosition (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Recordset15::AbsolutePosition
helpviewer_keywords: AbsolutePosition property [ADO]
ms.assetid: 79f8ee5e-fc70-46d8-8c29-ebf943c66592
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 17fe4e32b8a54d51ac3009e06e74e77e74321171
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="absoluteposition-property-ado"></a>Propriedade AbsolutePosition (ADO)
Indica a posição ordinal de um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) registro atual do objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Para o código de 32 bits, define ou retorna um **longo** valor entre 1 e o número de registros no **registros** objeto ([RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)), ou retorna um do [ PositionEnum](../../../ado/reference/ado-api/positionenum.md) valores.  
  
 Para o código de 64 bits, use um tipo de dados que fornece armazenamento de um valor de 64 bits. Por exemplo, você pode usar longa ou outro valor que é o comprimento de 64 bits como DBORDINAL. Não use **PositionEnum** valores como eles estão limitados a 32 bits de comprimento.  
  
## <a name="remarks"></a>Remarks  
 Para definir o **AbsolutePosition** propriedade, o ADO requer que implementa o provedor OLE DB que você estiver usando o [IRowsetLocate:IRowset](https://msdn.microsoft.com/library/windows/desktop/ms721190.aspx) interface.  
  
 Acessando o **AbsolutePosition** propriedade de um **registros** que foi aberto com um um somente de encaminhamento ou cursor dinâmico gera o erro **adErrFeatureNotAvailable**. Com outros tipos de cursor, a posição correta será retornada como o provedor OLE DB oferece suporte a **IRowsetScroll:IRowsetLocate** interface. Se o provedor não oferece suporte a **IRowsetScroll** interface, a propriedade é definida como **adPosUnknown**. Consulte a documentação do provedor determinar se ele dá suporte a **IRowsetScroll**.  
  
 Use o **AbsolutePosition** propriedade mover para um registro com base em sua posição ordinal no **registros** objeto, ou para determinar a posição ordinal do registro atual. O provedor deve oferecer suporte a funcionalidade apropriada para essa propriedade disponível.  
  
 Como o [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) propriedade **AbsolutePosition** é baseado em 1 e é igual a 1 quando o registro atual é o primeiro registro no **registros**. Você pode obter o número total de registros a **Recordset** de objeto o [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) propriedade.  
  
 Quando você define o **AbsolutePosition** propriedade, mesmo se ele é um registro no cache atual, ADO recarrega o cache com um novo grupo de registros que começam com o registro especificado. O [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) propriedade determina o tamanho desse grupo.  
  
> [!NOTE]
>  Você não deve usar o **AbsolutePosition** a propriedade como um número de registro de substitutos. A posição de um determinado registro muda quando você excluir um registro anterior. Também não há nenhuma garantia de que um determinado registro terá o mesmo **AbsolutePosition** se o **registros** objeto é novamente consultado ou reaberto. Indicadores ainda são a maneira recomendada de reter e retornar para uma determinada posição e são a única maneira de posicionamento de todos os tipos de **registros** objetos.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de propriedades de CursorLocation (VB) e AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vb.md)   
 [Exemplo de propriedades de CursorLocation (VC + +) e AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vc.md)   
 [Propriedade AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [Propriedade RecordCount (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
