---
title: Método setNClob (int, Java.IO. Reader) | Microsoft Docs
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
ms.assetid: 9fc9938c-b821-41c7-8df7-e21cb83a46d4
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 135d82aec8995f94ca87345cf3b4ade1466c33be
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setnclob-method-int-javaioreader"></a>Método setNClob (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o objeto Reader especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setNClob(int parameterIndex,  
                    java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *parameterIndex*  
  
 Um **int** que indica o índice do parâmetro.  
  
 *Leitor*  
  
 Um objeto do leitor que indica o valor do parâmetro.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setNClob é especificado pelo método setNClob na interface PreparedStatement.  
  
## <a name="see-also"></a>Consulte também  
 [Método setNClob &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
