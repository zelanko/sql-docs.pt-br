---
description: Propriedade MaxRecords (ADO)
title: Propriedade MaxRecords (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MaxRecords
helpviewer_keywords:
- MaxRecords property [ADO]
ms.assetid: 20c76571-8c9a-482c-a99e-726ab1d93f8b
author: rothja
ms.author: jroth
ms.openlocfilehash: 31870c4df71b20c162f95f1f1d942dde63885227
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990637"
---
# <a name="maxrecords-property-ado"></a>Propriedade MaxRecords (ADO)
Indica o número máximo de registros a serem retornados a um [conjunto de registros](./recordset-object-ado.md) de uma consulta.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor **longo** que indica o número máximo de registros a serem retornados. O padrão é zero (**0**), o que significa que não há limite.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **MaxRecords** para limitar o número de registros que o provedor retorna da fonte de dados. A configuração padrão dessa propriedade é zero, o que significa que o provedor retorna todos os registros solicitados.  
  
 A propriedade **MaxRecords** é de leitura/gravação quando o **conjunto de registros** é fechado e somente leitura quando é aberto.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade MaxRecords (VB)](./maxrecords-property-example-vb.md)   
 [Exemplo da propriedade MaxRecords (VC++)](./maxrecords-property-example-vc.md)