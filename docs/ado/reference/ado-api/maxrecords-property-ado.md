---
title: Propriedade MaxRecords (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::MaxRecords
helpviewer_keywords:
- MaxRecords property [ADO]
ms.assetid: 20c76571-8c9a-482c-a99e-726ab1d93f8b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 232f515c2250e1ec40fbb28bdff767baf9cf81c5
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="maxrecords-property-ado"></a>Propriedade MaxRecords (ADO)
Indica o número máximo de registros a serem retornados para um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) de uma consulta.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **longo** valor que indica o número máximo de registros a serem retornados. O padrão é zero (**0**), que significa sem limite.  
  
## <a name="remarks"></a>Comentários  
 Use o **MaxRecords** propriedade para limitar o número de registros que retorna o provedor da fonte de dados. A configuração padrão dessa propriedade é zero, o que significa que o provedor retorna que todos os registros de solicitados.  
  
 O **MaxRecords** propriedade é leitura/gravação quando o **registros** é fechado e somente leitura quando ela é aberta.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade MaxRecords (VB)](../../../ado/reference/ado-api/maxrecords-property-example-vb.md)   
 [Exemplo da propriedade MaxRecords (VC++)](../../../ado/reference/ado-api/maxrecords-property-example-vc.md)   

