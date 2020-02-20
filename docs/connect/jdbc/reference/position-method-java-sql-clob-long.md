---
title: Método position (java.sql.Clob, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.position (java.sql.Clob, long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b2fb34d5-1d34-4764-a795-712d9c6aa313
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 57b9af31e7701633e7cd73e8aaf0eb498b26c02c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67976411"
---
# <a name="position-method-javasqlclob-long"></a>Método position (java.sql.Clob, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna a posição de caractere do objeto CLOB especificado no CLOB com base na posição inicial fornecida.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public long position(java.sql.Clob searchstr,  
                     long start)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *searchstr*  
  
 A subcadeia de caracteres a ser pesquisada.  
  
 *start*  
  
 A posição em que a pesquisa deve ser iniciada. A primeira posição é 1.  
  
## <a name="return-value"></a>Valor retornado  
 A posição em que a subcadeia de caracteres aparece; ou -1 se ela não estiver presente. A primeira posição é 1.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método position é especificado pelo método position na interface java.sql.Clob.  
  
## <a name="see-also"></a>Consulte Também  
 [Método position &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/position-method-sqlserverclob.md)   
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
