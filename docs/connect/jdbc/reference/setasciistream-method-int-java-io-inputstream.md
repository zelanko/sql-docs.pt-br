---
title: Método setAsciiStream (int, Java.IO. InputStream) | Microsoft Docs
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
ms.assetid: 02c2443d-44e1-4f16-a0d5-08d197838214
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b14ebff6ea1c5c27e9f3beeabaf83bc26e217f1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setasciistream-method-int-javaioinputstream"></a>Método setAsciiStream (int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o número de parâmetro designado como o objeto Java.IO. InputStream determinado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setAsciiStream(int parameterIndex,  
                                 java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *parameterIndex*  
  
 Um **int** que indica o número do parâmetro.  
  
 *x*  
  
 Um objeto Java.IO. InputStream.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setAsciiStream é especificado pelo método setAsciiStream na interface PreparedStatement.  
  
## <a name="see-also"></a>Consulte também  
 [Método setAsciiStream &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
