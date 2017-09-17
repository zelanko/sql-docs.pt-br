---
title: "Método setResponseBuffering (SQLServerStatement) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apilocation:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apitype: Assembly
ms.assetid: 9f489835-6cda-4c8c-b139-079639a169cf
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c5af0e179ea15fc4d5a30604b606f5ff45c79a1b
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="setresponsebuffering-method-sqlserverstatement"></a>Método setResponseBuffering (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define a modo de buffer para esta resposta [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto maiusculas de minúsculas **cadeia de caracteres completa** ou **adaptável**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setResponseBuffering(java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *value*  
  
 Um **cadeia de caracteres** que contém o modo de buffer de resposta. O modo válido pode ser uma das seguintes cadeias de caracteres de maiusculas e minúsculas: **completo** ou **adaptável**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 **adaptável** Especifica o armazenamento em buffer o mínimo possível de dados quando necessário.  
  
 **completo** Especifica a leitura do resultado inteiro do servidor em tempo de execução.  
  
 adaptável é o valor padrão no Driver JDBC versão 2.0 e 3.0. completo era o padrão anterior ao JDBC Driver versão 2.0.  
  
 O [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) método permite que você substitua o **responseBuffering** conexão **cadeia de caracteres** propriedade atual [ SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto. Para obter mais informações sobre como usar a modo de buffer de resposta, consulte [buffer adaptável usando](../../../connect/jdbc/using-adaptive-buffering.md).  
  
 Se o aplicativo especificar um valor de parâmetro inválido para o [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) método, uma [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) é gerada.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)   
 [Usando buffer adaptável](../../../connect/jdbc/using-adaptive-buffering.md)  
  
  
