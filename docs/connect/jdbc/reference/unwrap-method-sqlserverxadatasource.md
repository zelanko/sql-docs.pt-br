---
title: Método unwrap (SQLServerXADataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d97c99b3-2224-4abb-8b32-40aff49fe759
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6b1ef2e7b05361ece8e54847b3c4d0d1df5ace08
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926076"
---
# <a name="unwrap-method-sqlserverxadatasource"></a>Método unwrap (SQLServerXADataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna um objeto que implementa a interface especificada para permitir o acesso aos métodos específicos do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *iface*  
  
 Uma classe do tipo **T** que define uma interface.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto que implementa a interface especificada.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 O método [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md) é definido pela interface java.sql.Wrapper introduzida no JDBC 4.0 Spec.  
  
 Os aplicativos talvez precisem acessar extensões para a API do JDBC específicas do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. O método unwrap é compatível com o desencapsulamento para classes públicas estendidas por esse objeto, caso as classes exponham extensões do fornecedor.  
  
 A classe [SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md) estende a classe [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md), que é estendida da classe [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md). Quando este método é chamado, o objeto é desencapsulado nas classes seguintes: [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md), [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) e [SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md).  
  
 Para obter mais informações, confira [Wrappers e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [Membros SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [Classe SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
