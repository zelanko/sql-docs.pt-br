---
title: Propriedade PageCount (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::PageCount
helpviewer_keywords:
- PageCount property [ADO]
ms.assetid: b601b56c-0ac4-44ee-bc91-c3d2d104f00a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: caecbded7964a1815204ccf1d6c8944fb999f6bc
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="pagecount-property-ado"></a>Propriedade PageCount (ADO)
Indica quantas páginas de dados a [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto contém.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um **longo** valor que indica o número de páginas no **registros**.  
  
## <a name="remarks"></a>Remarks  
 Use o **PageCount** propriedade para determinar quantas páginas de dados estão no **registros** objeto. *Páginas* são grupos de registros cujo tamanho é igual a [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) configuração de propriedade. Mesmo que a última página está incompleta porque há menos registros que o **PageSize** valor, ela será considerada como uma página adicional no **PageCount** valor. Se o **registros** objeto não dá suporte a essa propriedade, o valor será -1 para indicar que o **PageCount** for indeterminável.  
  
 Consulte o **PageSize** e [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) propriedades para a funcionalidade de página em mais.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedades de PageSize (VB), PageCount e AbsolutePage](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage, PageCount e exemplo de propriedades de PageSize (VC + +)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [Propriedade AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [Propriedade PageSize (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)   
 [Propriedade RecordCount (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
