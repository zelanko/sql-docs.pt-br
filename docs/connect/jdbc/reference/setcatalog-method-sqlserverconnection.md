---
title: "Método setCatalog (SQLServerConnection) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.setCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 553c0603-c07d-436a-86eb-3ba6b51bd696
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b766c76132bad3f66de98b431ee09d39753c40ab
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="setcatalog-method-sqlserverconnection"></a>Método setCatalog (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o nome de catálogo determinado para selecionar um subespaço deste [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) banco de dados do objeto no qual trabalhar.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setCatalog(java.lang.String catalog)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Catálogo*  
  
 Um **cadeia de caracteres** que contém o nome do catálogo.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setCatalog é especificado pelo método setCatalog na interface Java.SQL.  
  
 O *catálogo* argumento é escapado pelo [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] automaticamente. Usando esse método define a propriedade de catálogo para o objeto de Conexão. Ela não é definida implicitamente de nenhuma outra maneira.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
