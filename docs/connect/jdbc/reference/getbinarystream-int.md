---
title: getBinaryStream (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBinaryStream(int paramIndex)
apilocation:
- SQLServerCallableStatement.getBinaryStream(int paramIndex)
apitype: Assembly
ms.assetid: a766818e-cd05-4a07-a1ae-88966017448c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0e5e2a85e2db6dd89e571185712514a27621e835
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67953753"
---
# <a name="getbinarystream-int"></a>getBinaryStream (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um fluxo binário de bytes ininterruptos, considerando o índice do parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final java.io.InputStream getBinaryStream(int paramIndex)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *paramIndex*  
  
 Um **int** que indica o índice do parâmetro.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto InputStream.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Método getBinaryStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
