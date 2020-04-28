---
title: Propriedade MaxRecords (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5acd8997af6993a49ac4cbcca6e3b4c8bd26acfd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932231"
---
# <a name="maxrecords-property-ado"></a>Propriedade MaxRecords (ADO)
Indica o número máximo de registros a serem retornados a um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) de uma consulta.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor **longo** que indica o número máximo de registros a serem retornados. O padrão é zero (**0**), o que significa que não há limite.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **MaxRecords** para limitar o número de registros que o provedor retorna da fonte de dados. A configuração padrão dessa propriedade é zero, o que significa que o provedor retorna todos os registros solicitados.  
  
 A propriedade **MaxRecords** é de leitura/gravação quando o **conjunto de registros** é fechado e somente leitura quando é aberto.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade MaxRecords (VB)](../../../ado/reference/ado-api/maxrecords-property-example-vb.md)   
 [Exemplo da propriedade MaxRecords (VC++)](../../../ado/reference/ado-api/maxrecords-property-example-vc.md)   
