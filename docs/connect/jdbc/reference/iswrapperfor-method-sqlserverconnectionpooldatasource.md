---
title: "Método isWrapperFor (SQLServerConnectionPoolDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 09ed10eb-6e46-437b-a7c0-3c55574aad38
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8025e9271a706aac4bb35bd9fd1565762632d6b9
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="iswrapperfor-method-sqlserverconnectionpooldatasource"></a>Método isWrapperFor (SQLServerConnectionPoolDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se o objeto em questão é um wrapper para a interface especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isWrapperFor(Class iface)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *iface*  
  
 Um **classe** define uma interface.  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se esse objeto implementa a interface ou encapsular um objeto que implementa a interface. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 O [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md) método e o [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md) método são definidos pela interface Java.SQL, introduzida no JDBC 4.0 Spec.  
  
 Se esse método retornar true, chamar [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md) com o mesmo argumento será bem-sucedida.  
  
 Para obter mais informações, consulte [Wrappers e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte também  
 [decodificar método &#40; SQLServerConnectionPoolDataSource &#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)   
 [Métodos SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [Membros SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [Classe SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  

