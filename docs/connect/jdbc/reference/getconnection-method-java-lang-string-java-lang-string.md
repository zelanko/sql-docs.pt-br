---
title: Método (Java, Java) getConnection | Microsoft Docs
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
- SQLServerDataSource.getConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 78db89d6-a8a0-4116-8885-548e627220ed
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fb33640c75d98fa065c6388458aaffc3067c3126
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32832291"
---
# <a name="getconnection-method-javalangstring-javalangstring"></a>Método getConnection (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Tenta estabelecer uma conexão com os dados de origem que este [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto representa usando o nome de usuário e senha.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Connection getConnection(java.lang.String username,  
                                         java.lang.String password)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *username*  
  
 Um **cadeia de caracteres** que contém o nome de usuário.  
  
 *password*  
  
 Um **cadeia de caracteres** que contém a senha.  
  
## <a name="return-value"></a>Valor de retorno  
 Um [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 Esse método getConnection é especificado pelo método getConnection na interface javax.SQL.  
  
 Chamar o getConnection método com um nome de usuário não nulo ou senha substituirá as propriedades de nome e senha de usuário que são definidas na classe SQLServerDataSource ao inicializar o objeto SQLServerConnection. Por exemplo, se o chamador chamou [setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) e [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) na fonte de dados e chamadas getConnection e nome de usuário de fontes não nulo ou uma senha não nula, o nome de usuário e a senha definida setUser e setPassword serão substituídos pelo nome de usuário e a senha em getConnection.  
  
> [!NOTE]  
>  O nome de usuário e senha que são definidos dentro da URL usando uma chamada para o [setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md) método não será alterado nesse caso.  
  
## <a name="see-also"></a>Consulte também  
 [Método getConnection &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)   
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
