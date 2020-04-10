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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e98b901663a63b353e14ae31308e244a55a78369
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80915113"
---
# <a name="iswrapperfor-method-sqlserverstatement"></a>Método isWrapperFor (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se o objeto da instrução é um wrapper para a interface especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isWrapperFor(Class iface)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *iface*  
  
 Uma **classe** que define uma interface.  
  
## <a name="return-value"></a>Valor retornado  
 **true** se esse objeto implementar a interface ou encapsular um objeto que implementa a interface. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 O método [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) e o método [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) são definidos pela interface java.sql.Wrapper, introduzida no JDBC 4.0.  
  
 Se esse método retornar true, a chamada de [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) com o mesmo argumento será bem-sucedida.  
  
 Para ver um exemplo de código, confira [Como atualizar um exemplo de dados grandes](../../../connect/jdbc/updating-large-data-sample.md).  
  
 Para obter mais informações, confira [Wrappers e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Método unwrap &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)   
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
