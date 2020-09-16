---
description: Método isWrapperFor (SQLServerDataSource)
title: Método isWrapperFor (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f77af027-c021-4a17-b264-1ee592bfdd84
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bcd792e3029a1591eaa05f88de80569e750429e9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433318"
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
  
 Uma **classe** que define uma interface.  
  
## <a name="return-value"></a>Valor de retorno  
 **true** se esse objeto implementar a interface ou encapsular um objeto que implementa a interface. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 O método [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md) e o método [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md) são definidos pela interface java.sql.Wrapper introduzida no JDBC 4.0 Spec.  
  
 Se esse método retornar true, a chamada de [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md) com o mesmo argumento será bem-sucedida.  
  
 Para obter mais informações, confira [Wrappers e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Método unwrap &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)   
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
