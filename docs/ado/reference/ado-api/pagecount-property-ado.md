---
description: Propriedade PageCount (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: aa050f7e99115ca13bf8871378ffa21b1f326d94
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773535"
---
# <a name="pagecount-property-ado"></a>Propriedade PageCount (ADO)
Indica quantas páginas de dados o objeto [Recordset](./recordset-object-ado.md) contém.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um valor **longo** que indica o número de páginas no **conjunto de registros**.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **PageCount** para determinar quantas páginas de dados estão no objeto **Recordset** . *Páginas* são grupos de registros cujo tamanho é igual à configuração da propriedade [PageSize](./pagesize-property-ado.md) . Mesmo que a última página esteja incompleta porque há menos registros do que o valor **PageSize** , ele conta como uma página adicional no valor **PageCount** . Se o objeto **Recordset** não oferecer suporte a essa propriedade, o valor será-1 para indicar que **PageCount** é interminável.  
  
 Consulte as propriedades **PageSize** e [AbsolutePage](./absolutepage-property-ado.md) para obter mais informações sobre a funcionalidade da página.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades AbsolutePage, PageCount e PageSize (VB)](./absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [Exemplo das propriedades AbsolutePage, PageCount e PageSize (VC + +)](./absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [Propriedade AbsolutePage (ADO)](./absolutepage-property-ado.md)   
 [Propriedade PageSize (ADO)](./pagesize-property-ado.md)   
 [Propriedade RecordCount (ADO)](./recordcount-property-ado.md)