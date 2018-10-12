---
title: Método getXAConnection (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXADataSource.getXAConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 276e0093-3d42-4f73-acc4-2b5b98245b40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b75d79c0cb211a2d0da7b5e0f026d9ec2171d75d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694424"
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
  
 Uma **String** que contém o nome do usuário.  
  
 *password*  
  
 Uma **String** que contém a senha.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto XAConnection.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 Esse método getXAConnection é especificado pelo método getXAConnection na interface xadatasource.  
  
> [!NOTE]  
>  Esse método é chamado geralmente pelas implementações de pool de conexões XA, mas não regularmente pelo código de aplicativo JDBC.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getXAConnection &#40;SQLServerXADataSource&#41;](../../../connect/jdbc/reference/getxaconnection-method-sqlserverxadatasource.md)   
 [Métodos SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [Membros SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [Classe SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
