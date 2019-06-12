---
title: Método getObjectInstance (SQLServerDataSourceObjectFactory) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSourceObjectFactory.getObjectInstance
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0a1503e2-e991-4d70-a223-087fc63baf73
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 13da5aeb7015255f0ff4b7a540b62462439ce30d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66765666"
---
# <a name="getobjectinstance-method-sqlserverdatasourceobjectfactory"></a>Método getObjectInstance (SQLServerDataSourceObjectFactory)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma instância do objeto de fonte de dados especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.Object getObjectInstance(java.lang.Object ref,  
                                          javax.naming.Name name,  
                                          javax.naming.Context c,  
                                          java.util.Hashtable h)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ref*  
  
 Um valor **Object**.  
  
 *name*  
  
 O nome do objeto.  
  
 *c*  
  
 O contexto relativo ao nome especificado.  
  
 *h*  
  
 O ambiente usado ao criar o objeto.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor **Object**.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 Esse método getObjectInstance é especificado pelo método getObjectInstance na interface javax.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-methods.md)   
 [Membros de SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [Classe SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)  
  
  
