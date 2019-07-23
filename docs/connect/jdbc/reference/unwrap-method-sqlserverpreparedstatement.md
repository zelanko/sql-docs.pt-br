---
title: desencapsular método (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8e3ec950-3ac1-4c28-9e97-ddce3bd46578
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 81e533e32504df219155259e9639c83c3be4c647
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985596"
---
# <a name="unwrap-method-sqlserverpreparedstatement"></a>Método unwrap (SQLServerPreparedStatement)
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
 O método [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md) é definido pela interface java.sql.Wrapper introduzida no JDBC 4.0 Spec.  
  
 Os aplicativos talvez precisem acessar extensões para a API do JDBC específicas do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. O método unwrap é compatível com o desencapsulamento para classes públicas estendidas por esse objeto, caso as classes exponham extensões do fornecedor.  
  
 Quando este método é chamado, o objeto é desencapsulado nas seguintes: [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) e [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).  
  
 Para obter um exemplo de código, consulte desencapsular o [método &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md).  
  
 Para obter mais informações, consulte [wrappers e interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Método isWrapperFor &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
