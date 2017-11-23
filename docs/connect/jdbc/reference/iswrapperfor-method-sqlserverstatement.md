---
title: "Método isWrapperFor (SQLServerStatement) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 53f3291f-d43a-476b-a656-d86168dacf6c
caps.latest.revision: "20"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1c9ddb7aab2cad2a7acd4f5cf685df5f5fff674a
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="iswrapperfor-method-sqlserverstatement"></a>Método isWrapperFor (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se o objeto da instrução é um wrapper para a interface especificada.  
  
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
 O [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) método e o [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) método são definidos pela interface Java.SQL, introduzida no JDBC 4.0.  
  
 Se esse método retornar true, chamar [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) com o mesmo argumento será bem-sucedida.  
  
 Para um exemplo de código, consulte [amostra de dados grande atualização](../../../connect/jdbc/updating-large-data-sample.md).  
  
 Para obter mais informações, consulte [Wrappers e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte também  
 [decodificar método &#40; SQLServerStatement &#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)   
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
