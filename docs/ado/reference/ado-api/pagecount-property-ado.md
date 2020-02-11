---
title: Propriedade PageCount (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::PageCount
helpviewer_keywords:
- PageCount property [ADO]
ms.assetid: b601b56c-0ac4-44ee-bc91-c3d2d104f00a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ea893a019ab6d1333cecc5da5f1f66928467adfc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931782"
---
# <a name="pagecount-property-ado"></a>Propriedade PageCount (ADO)
Indica quantas páginas de dados o objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) contém.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um valor **longo** que indica o número de páginas no **conjunto de registros**.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **PageCount** para determinar quantas páginas de dados estão no objeto **Recordset** . *Páginas* são grupos de registros cujo tamanho é igual à configuração da propriedade [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) . Mesmo que a última página esteja incompleta porque há menos registros do que o valor **PageSize** , ele conta como uma página adicional no valor **PageCount** . Se o objeto **Recordset** não oferecer suporte a essa propriedade, o valor será-1 para indicar que **PageCount** é interminável.  
  
 Consulte as propriedades **PageSize** e [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) para obter mais informações sobre a funcionalidade da página.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades AbsolutePage, PageCount e PageSize (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [Exemplo das propriedades AbsolutePage, PageCount e PageSize (VC + +)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [Propriedade AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [Propriedade PageSize (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)   
 [Propriedade RecordCount (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
