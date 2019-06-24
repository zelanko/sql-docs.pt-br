---
title: Método setBinaryStream (int, java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6c32b904-c44b-472e-a084-38f008a742b4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 97de855dd6f80b044ec8a72d30a3041aa5990705
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66764713"
---
# <a name="setbinarystream-method-int-javaioinputstream"></a>Método setBinaryStream (int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o fluxo de entrada especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setAsciiStream(int parameterIndex,  
                                 java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *parameterIndex*  
  
 Um **int** que indica o número do parâmetro.  
  
 *x*  
  
 Um objeto java.io.InputStream.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setBinaryStream é especificado pelo método setBinaryStream na interface do PreparedStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Método setBinaryStream &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setbinarystream-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
