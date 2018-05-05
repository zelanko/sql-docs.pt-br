---
title: Método getResponseBuffering (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerStatement.getResponseBuffering()
apilocation:
- SQLServerStatement.getResponseBuffering()
apitype: Assembly
ms.assetid: a9a9ffdd-7ce3-4e0a-907c-34d6a54e6865
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 64ad84e838e64c0e4bd148705e2753277f908a3c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getresponsebuffering-method-sqlserverstatement"></a>Método getResponseBuffering (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera a modo de buffer para esta resposta [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final java.lang.String getResponseBuffering()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **cadeia de caracteres** que contém um minúsculas **completo** ou **adaptável**.  
  
## <a name="remarks"></a>Remarks  
 **adaptável** Especifica o armazenamento em buffer o mínimo possível de dados quando necessário.  
  
 **completo** Especifica a leitura do resultado inteiro do servidor em tempo de execução.  
  
 **adaptável** é o valor padrão no Driver JDBC versão 2.0 e 3.0. **completo** era o padrão anterior ao JDBC Driver versão 2.0.  
  
 Para obter mais informações sobre como usar a modo de buffer de resposta, consulte [buffer adaptável usando](../../../connect/jdbc/using-adaptive-buffering.md).  
  
## <a name="see-also"></a>Consulte também  
 [Método setResponseBuffering &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)   
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
