---
title: Método setResponseBuffering (SQLServerStatement) | Microsoft Docs
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
ms.topic: conceptual
apiname:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apilocation:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apitype: Assembly
ms.assetid: 9f489835-6cda-4c8c-b139-079639a169cf
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5abd900d5ba91939eb055b732a4710c4b89f0822
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
## <a name="remarks"></a>Remarks  
 **adaptável** Especifica o armazenamento em buffer o mínimo possível de dados quando necessário.  
  
 **completo** Especifica a leitura do resultado inteiro do servidor em tempo de execução.  
  
 adaptável é o valor padrão no Driver JDBC versão 2.0 e 3.0. completo era o padrão anterior ao JDBC Driver versão 2.0.  
  
 O [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) método permite que você substitua o **responseBuffering** conexão **cadeia de caracteres** propriedade atual [ SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto. Para obter mais informações sobre como usar a modo de buffer de resposta, consulte [buffer adaptável usando](../../../connect/jdbc/using-adaptive-buffering.md).  
  
 Se o aplicativo especificar um valor de parâmetro inválido para o [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) método, uma [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) é gerada.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)   
 [Usando buffer adaptável](../../../connect/jdbc/using-adaptive-buffering.md)  
  
  
