---
title: Método (Java) (SQLServerResultSet) getBoolean | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBoolean (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ba98a27b-722d-4904-ac65-0f082fde1fe6
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d4b2af268b3d38566c2f1d4110c93171767f8e1b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32832391"
---
# <a name="getboolean-method-javalangstring-sqlserverresultset"></a>getBoolean método (Java) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do nome da coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de objeto como um **booliano** na linguagem de programação Java.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean getBoolean(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnName*  
  
 Um **cadeia de caracteres** que contém o nome da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Um valor **booliano**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getBoolean é especificado pelo método getBoolean na interface Java.SQL. resultset.  
  
 Esse método tem suporte apenas em tipos de dados numéricos e de caractere. Ele converte os valores "1", 1, e "**true**" para **true**e os valores "0", 0, e "**false**" para **false**. Para todos os outros valores o comportamento é indefinido.  
  
## <a name="see-also"></a>Consulte também  
 [Método getBoolean &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getboolean-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
