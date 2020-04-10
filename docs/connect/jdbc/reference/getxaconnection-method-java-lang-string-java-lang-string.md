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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1e76596e52afa115a436cc7e421fc5deb06139b6
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80910052"
---
# <a name="getxaconnection-method-javalangstring-javalangstring"></a>Método getXAConnection (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Tenta estabelecer uma conexão de banco de dados física usando o nome de usuário e senha determinados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public javax.sql.XAConnection getXAConnection(java.lang.String user,  
                                              java.lang.String password)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *user*  
  
 Uma **String** que contém o nome do usuário.  
  
 *password*  
  
 Uma **String** que contém a senha.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto XAConnection.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Comentários  
 Esse método getXAConnection é especificado pelo método getXAConnection na interface javax.sql.XADataSource.  
  
> [!NOTE]  
>  Esse método é chamado geralmente pelas implementações de pool de conexões XA, mas não regularmente pelo código de aplicativo JDBC.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getXAConnection &#40;SQLServerXADataSource&#41;](../../../connect/jdbc/reference/getxaconnection-method-sqlserverxadatasource.md)   
 [Métodos SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [Membros SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [Classe SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
