---
title: "Método getObject (int, java.util.Map) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerCallableStatement.getObject (int, java.util.Map)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 164532be-7ed6-40fa-a273-dece4c8d72c4
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 71de96500026936d5f734101d3e3712401ea7ac7
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getobject-method-int-javautilmap"></a>Método getObject (int, java.util.Map)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um objeto na linguagem de programação Java considerando o índice do parâmetro, usando o objeto de mapa fornecido.  
  
> [!NOTE]  
>  Esse método não é suportado atualmente pelo [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. O uso deste método sempre retornará o mapeamento padrão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.Object getObject(int index,  
                                  java.util.Map map)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *índice*  
  
 Um **int** que indica o índice do parâmetro.  
  
 *mapa*  
  
 Um objeto de mapa.  
  
## <a name="return-value"></a>Valor de retorno  
 Um **objeto** valor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getObject é especificado pelo método na interface do CallableStatement getObject.  
  
 Esse método retornará o valor da coluna fornecida como um objeto Java. O tipo desse objeto será o tipo de objeto Java padrão correspondente ao tipo SQL da coluna, seguindo o mapeamento para tipos internos constante na especificação do JDBC. Se o valor for um SQL NULL, o driver retornará um Java nulo.  
  
 Esse método também pode ser usado para ler tipos de dados abstratos específicos do banco de dados. Na API do JDBC 2.0, o comportamento do método getObject é estendido para materializar dados de tipos definidos pelo usuário do SQL. Quando uma coluna contém um valor estruturado ou distinto, o comportamento desse método é como se fosse uma chamada para `getObject(columnIndex, this.getStatement().getConnection().getTypeMap())`.  
  
 A partir de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0:  
  
-   Um valor de tipo date será retornado como um objeto java.sql.Date.  
  
-   Um valor de tipo time será retornado como um objeto java.sql.Time.  
  
-   Um valor de datetime2 de tipo será retornado como um objeto java.sql.Timestamp.  
  
-   Um valor de datetimeoffset de tipo será retornado como um objeto microsoft.sql.DateTimeOffset.  
  
## <a name="see-also"></a>Consulte também  
 [Método getObject &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getobject-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

