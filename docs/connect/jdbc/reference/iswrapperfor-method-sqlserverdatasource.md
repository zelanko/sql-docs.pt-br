---
title: "Método isWrapperFor (SQLServerDataSource) | Microsoft Docs"
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
ms.assetid: f77af027-c021-4a17-b264-1ee592bfdd84
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9d9537b797aefd83d1a09b90b37677e2a5c9b957
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="iswrapperfor-method-sqlserverdatasource"></a>Método isWrapperFor (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se o objeto da fonte de dados é um wrapper da interface especificada.  
  
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
 O [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md) método e o [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md) método são definidos pela interface Java.SQL, introduzida no JDBC 4.0 Spec.  
  
 Se esse método retornar true, chamar [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md) com o mesmo argumento será bem-sucedida.  
  
 Para obter mais informações, consulte [Wrappers e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte também  
 [decodificar método &#40; SQLServerDataSource &#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)   
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

