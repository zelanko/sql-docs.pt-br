---
title: desencapsular método (SQLServerConnectionPoolDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f5c9b734-2096-4ae4-a284-6b4d1b4a00d4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab408e917a1e6c22cdbe320eb19f5c9995c6e216
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985613"
---
# <a name="unwrap-method-sqlserverconnectionpooldatasource"></a>Método unwrap (SQLServerConnectionPoolDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna um objeto que implementa a interface especificada para permitir o acesso aos métodos específicos do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *iface*  
  
 Uma classe do tipo **T** que define uma interface.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto que implementa a interface especificada.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 O método [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md) é definido pela interface java.sql.Wrapper introduzida no JDBC 4.0 Spec.  
  
 Os aplicativos talvez precisem acessar extensões para a API do JDBC específicas do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. O método unwrap é compatível com o desencapsulamento para classes públicas estendidas por esse objeto, caso as classes exponham extensões do fornecedor.  
  
 A classe [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) estende a classe [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md). Quando esse método é chamado, o objeto é desencapsulado para as classes [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) e [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md).  
  
 Para obter mais informações, consulte [wrappers e interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [Membros SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [Classe SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  
