---
title: Propriedade PageSize (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::PageSize
helpviewer_keywords:
- PageSize property [ADO]
ms.assetid: e57930a6-46c4-4a17-a3b6-f79e94d5c9c7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c33b8a757e699a78c699cc87e7fd7dba26006b5d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47741444"
---
# <a name="pagesize-property-ado"></a>Propriedade PageSize (ADO)
Indica o número de registros constituem uma página na [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **longo** valor que indica quantos registros estão em uma página. O padrão é **10**.  
  
## <a name="remarks"></a>Comentários  
 Use o **PageSize** propriedade para determinar quantos registros compõem uma página lógica dos dados. Estabelecer um tamanho de página permite que você use o [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) propriedade para mover para o primeiro registro de uma página específica. Isso é útil em cenários de servidor Web quando você deseja permitir que o usuário à página por meio de dados, exibindo um determinado número de registros por vez.  
  
 Essa propriedade pode ser definida em qualquer momento, e seu valor será usado para calcular a localização do primeiro registro de uma página específica.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [AbsolutePage, PageCount, PageSize exemplo das propriedades e (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage, PageCount, PageSize exemplo das propriedades e (VC + +)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [Propriedade AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [Propriedade PageCount (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
