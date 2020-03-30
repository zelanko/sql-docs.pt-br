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
ms.openlocfilehash: de25e608c9fbdbdf6ff91d08e7a6502765bb590e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67981055"
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
  
#### <a name="parameters"></a>parâmetros  
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
  
## <a name="remarks"></a>Comentários  
 Esse método getObjectInstance é especificado pelo método getObjectInstance na interface javax.naming.spi.ObjectFactory.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-methods.md)   
 [Membros de SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [Classe SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)  
  
  
