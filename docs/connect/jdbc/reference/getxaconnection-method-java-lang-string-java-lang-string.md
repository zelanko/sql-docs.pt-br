---
title: Método (Java, Java) getXAConnection | Microsoft Docs
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
- SQLServerXADataSource.getXAConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 276e0093-3d42-4f73-acc4-2b5b98245b40
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8aec959822b00c79031226aaccbaf0085f68f79d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getxaconnection-method-javalangstring-javalangstring"></a>Método getXAConnection (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Tenta estabelecer uma conexão de banco de dados física usando o nome de usuário e senha determinados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public javax.sql.XAConnection getXAConnection(java.lang.String user,  
                                              java.lang.String password)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *user*  
  
 Um **cadeia de caracteres** que contém o nome de usuário.  
  
 *password*  
  
 Um **cadeia de caracteres** que contém a senha.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto XAConnection.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 Esse método getXAConnection é especificado pelo método getXAConnection na interface javax.SQL. xadatasource.  
  
> [!NOTE]  
>  Esse método é chamado geralmente pelas implementações de pool de conexões XA, mas não regularmente pelo código de aplicativo JDBC.  
  
## <a name="see-also"></a>Consulte também  
 [Método getXAConnection &#40;SQLServerXADataSource&#41;](../../../connect/jdbc/reference/getxaconnection-method-sqlserverxadatasource.md)   
 [Métodos SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [Membros de SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [Classe SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
