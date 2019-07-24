---
title: Método isWrapperFor (SQLServerConnectionPoolDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 09ed10eb-6e46-437b-a7c0-3c55574aad38
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 45e7e2cd5e14392d5acc00601d05d3c7eb42f192
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977088"
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
  
 Uma **classe** que define uma interface.  
  
## <a name="return-value"></a>Valor retornado  
 **true** se esse objeto implementar a interface ou encapsular um objeto que implementa a interface. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 O método [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md) e o método [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md) são definidos pela interface java.sql.Wrapper introduzida no JDBC 4.0 Spec.  
  
 Se esse método retornar true, a chamada de [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md) com o mesmo argumento será bem-sucedida.  
  
 Para obter mais informações, consulte [wrappers e interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Método unwrap &#40;SQLServerConnectionPoolDataSource&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)   
 [Métodos SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [Membros SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [Classe SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  
