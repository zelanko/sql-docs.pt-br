---
title: Método isWrapperFor (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53f3291f-d43a-476b-a656-d86168dacf6c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 34ead896ef4ba8ae6fc5d8ca57c1623a00aa5165
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796279"
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
  
 Um **classe** definindo uma interface.  
  
## <a name="return-value"></a>Valor retornado  
 **True** se esse objeto implementa a interface ou encapsula um objeto que implementa a interface. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 O método [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) e o método [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) são definidos pela interface java.sql.Wrapper, introduzida no JDBC 4.0.  
  
 Se esse método retornar true, a chamada de [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) com o mesmo argumento será bem-sucedida.  
  
 Para um exemplo de código, consulte [atualizando exemplo de dados grandes](../../../connect/jdbc/updating-large-data-sample.md).  
  
 Para obter mais informações, consulte [Wrappers e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Método unwrap &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)   
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
