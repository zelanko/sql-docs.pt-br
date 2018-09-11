---
title: Método getObject (java.lang.String) (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.getObject (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 59a975e8-bea8-42fe-8f34-5f18f2bbd415
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2698843e68dcb745098753e2dd618096ac3a195
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42786040"
---
# <a name="getobject-method-javalangstring-sqlserverresultset"></a>Método getObject (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Obtém o valor do nome da coluna designada na linha atual do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como um objeto na linguagem de programação Java.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.Object getObject(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnName*  
  
 Uma **Cadeia de Caracteres** que contém o nome da coluna.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor **Object**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getObject é especificado pelo método getObject na interface do resultset.  
  
 Esse método retornará o valor da coluna fornecida como um objeto Java. O tipo desse objeto será o tipo de objeto Java padrão correspondente ao tipo SQL da coluna, seguindo o mapeamento para tipos internos constante na especificação do JDBC. Se o valor for um SQL NULL, o driver retornará um Java nulo.  
  
 Esse método também pode ser usado para ler tipos de dados abstratos específicos do banco de dados. Na API do JDBC 2.0, o comportamento do método getObject é estendido para materializar dados de tipos definidos pelo usuário do SQL. Quando uma coluna contiver um valor estruturado ou distinto, o comportamento desse método será como se fosse uma chamada para `getObject(columnIndex, this.getStatement().getConnection().getTypeMap())`.  
  
 A partir do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0:  
  
-   Um valor de tipo date será retornado como um objeto java.sql.Date.  
  
-   Um valor de tipo time será retornado como um objeto java.sql.Time.  
  
-   Um valor de datetime2 de tipo será retornado como um objeto java.sql.Timestamp.  
  
-   Um valor de datetimeoffset de tipo será retornado como um objeto microsoft.sql.DateTimeOffset.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getObject &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
