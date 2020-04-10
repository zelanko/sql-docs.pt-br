---
title: Método unwrap (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: eb8abe29-f3ec-4752-a590-1d5dc3e48f08
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5ad619a07e1eb10a74acd9ab5769baa7f0d1c653
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926109"
---
# <a name="unwrap-method-sqlserverdatasource"></a>Método unwrap (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna um objeto que implementa a interface especificada para permitir o acesso aos métodos específicos do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *iface*  
  
 Uma classe do tipo T que define uma interface.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto que implementa a interface especificada.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 O método [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md) é definido pela interface java.sql.Wrapper introduzida no JDBC 4.0 Spec.  
  
 Os aplicativos talvez precisem acessar extensões para a API do JDBC específicas do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. O método unwrap é compatível com o desencapsulamento para classes públicas estendidas por esse objeto, caso as classes exponham extensões do fornecedor.  
  
 Quando esse método é chamado, o objeto é desencapsulado na classe [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
 Para obter mais informações, confira [Wrappers e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Método isWrapperFor &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)   
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
