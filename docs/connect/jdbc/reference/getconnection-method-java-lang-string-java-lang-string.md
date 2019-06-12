---
title: Método getConnection (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 78db89d6-a8a0-4116-8885-548e627220ed
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 86c6637a3f502212b2b2f35a47207d7276ce8df5
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66763287"
---
# <a name="getconnection-method-javalangstring-javalangstring"></a>Método getConnection (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Tenta estabelecer uma conexão com a fonte de dados que o objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) representa usando o nome de usuário e a senha fornecidos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Connection getConnection(java.lang.String username,  
                                         java.lang.String password)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *username*  
  
 Uma **String** que contém o nome do usuário.  
  
 *password*  
  
 Uma **String** que contém a senha.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 Esse método getConnection é especificado pelo método getConnection na interface javax.  
  
 Chamar o getConnection método com um nome de usuário não nulo ou senha substituirá as propriedades de nome e a senha do usuário que são definidas na classe SQLServerDataSource ao inicializar o objeto SQLServerConnection. Por exemplo, se o chamador chamou [setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) e [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) na fonte de dados e, em seguida, chamar getConnection e fornecer um nome de usuário não nulo ou uma senha não nula, o nome de usuário e a senha definidos por setUser e setPassword serão substituídos pelo nome de usuário e pela senha transmitidos ao getConnection.  
  
> [!NOTE]  
>  O nome de usuário e a senha que são definidos dentro da URL usando uma chamada ao método [setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md) não serão alterados nesse caso.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getConnection &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)   
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
