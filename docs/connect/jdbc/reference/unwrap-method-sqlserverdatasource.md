---
title: "Método unwrap (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eb8abe29-f3ec-4752-a590-1d5dc3e48f08
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6c7fd1ebcd5f1a9a1d963298212b2423f90e194d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="unwrap-method-sqlserverdatasource"></a>Método unwrap (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna um objeto que implementa a interface especificada para permitir acesso a [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-métodos específicos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *iface*  
  
 Uma classe do tipo T que define uma interface.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto que implementa a interface especificada.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 O [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md) método é definido pela interface Java.SQL, introduzida no JDBC 4.0 Spec.  
  
 Aplicativos talvez precisem acessar extensões para a API do JDBC que são específicas para o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. O método unwrap dá suporte ao desencapsulamento em classes públicas que esse objeto, caso as classes exponham extensões do fornecedor.  
  
 Quando este método é chamado, o objeto é desencapsulado o [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) classe.  
  
 Para obter mais informações, consulte [Wrappers e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte também  
 [Método isWrapperFor &#40; SQLServerDataSource &#41;](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)   
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

