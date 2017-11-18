---
title: "Método getSchemas () | Microsoft Docs"
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
- SQLServerDatabaseMetaData.getSchemas
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: adba0ee6-ff6d-4215-b646-62c735be3fe9
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6a66767527b1fb7bfe2c3b3f03414ef643676b4e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getschemas-method-"></a>Método getSchemas ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera os nomes de esquema disponíveis no banco de dados atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getSchemas()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getSchemas é especificado pelo método getSchemas na interface DatabaseMetadata.  
  
 O conjunto de resultados retornado pelo método getSchemas contém as seguintes informações:  
  
|Nome|Tipo|Description|  
|----------|----------|-----------------|  
|TABLE_SCHEM|**Cadeia de caracteres**|O nome do esquema.|  
|TABLE_CATALOG|**Cadeia de caracteres**|O nome de catálogo para o esquema.|  
  
 Os resultados são ordenados por TABLE_CATALOG e, em seguida, por TABLE_SCHEM. Cada linha tem TABLE_SCHEM como a primeira coluna e TABLE_CATALOG como a segunda coluna.  
  
> [!NOTE]  
>  Para obter mais informações sobre os dados retornados pelo método getSchemas, consulte "Schemas (Transact-SQL)" em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Manuais Online.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar o método getSchemas para retornar informações sobre o catálogo e seus nomes de esquema associado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] quando o argumento de conexão Especifica o banco de dados a ser usado.  
  
```  
public static void executeGetSchemas(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getSchemas();  
      ResultSetMetaData rsmd = rs.getMetaData();  
  
      // Display the result set data.  
      int cols = rsmd.getColumnCount();  
      while(rs.next()) {  
         for (int i = 1; i <= cols; i++) {  
            System.out.println(rs.getString(i));  
         }  
      }  
      rs.close();  
   }   
  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

