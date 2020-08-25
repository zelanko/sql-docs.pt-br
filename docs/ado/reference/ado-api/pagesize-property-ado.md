---
description: Propriedade PageSize (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2c073d0ef7cceb74864b7f526ef9a5283ca946a7
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773525"
---
# <a name="pagesize-property-ado"></a>Propriedade PageSize (ADO)
Indica quantos registros constituem uma página no conjunto de [registros](./recordset-object-ado.md).  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor **longo** que indica quantos registros estão em uma página. O padrão é **10**.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **PageSize** para determinar quantos registros compõem uma página lógica de dados. O estabelecimento de um tamanho de página permite que você use a propriedade [AbsolutePage](./absolutepage-property-ado.md) para mover para o primeiro registro de uma página específica. Isso é útil em cenários de servidor Web quando você deseja permitir que o usuário percorra dados, exibindo um determinado número de registros por vez.  
  
 Essa propriedade pode ser definida a qualquer momento e seu valor será usado para calcular o local do primeiro registro de uma página específica.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades AbsolutePage, PageCount e PageSize (VB)](./absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [Exemplo das propriedades AbsolutePage, PageCount e PageSize (VC + +)](./absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [Propriedade AbsolutePage (ADO)](./absolutepage-property-ado.md)   
 [Propriedade PageCount (ADO)](./pagecount-property-ado.md)