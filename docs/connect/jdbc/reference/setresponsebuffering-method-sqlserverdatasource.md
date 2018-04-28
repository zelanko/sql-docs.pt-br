---
title: Método setResponseBuffering (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerDataSource.setResponseBuffering(String responseBufferingValue)
apilocation:
- SQLServerDataSource.setResponseBuffering(String responseBufferingValue)
apitype: Assembly
ms.assetid: c9e43ff2-8117-4dca-982d-83c863d0c8e1
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f188e7310725f56f69cce65b7496205a668c109f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="setresponsebuffering-method-sqlserverdatasource"></a>Método setResponseBuffering (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define a resposta de modo de buffer de conexões criadas usando esse [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setResponseBuffering(java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *value*  
  
 Um **cadeia de caracteres** que contém o modo de buffer e streaming. O modo válido pode ser uma das seguintes cadeias de caracteres de maiusculas e minúsculas: **completo** ou **adaptável**.  
  
## <a name="remarks"></a>Remarks  
 O **completo** valor Especifica a leitura do resultado inteiro do servidor em tempo de execução.  
  
 O **adaptável** valor Especifica o armazenamento em buffer o mínimo possível de dados quando necessário. O **adaptável** valor é o modo de buffer padrão.  
  
 Para obter mais informações sobre como usar a modo de buffer de resposta, consulte [buffer adaptável usando](../../../connect/jdbc/using-adaptive-buffering.md).  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
