---
title: Método getSchemas () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSchemas
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: adba0ee6-ff6d-4215-b646-62c735be3fe9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c7951e25fd7dfbd089b21be066cfefd9828c231
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80929232"
---
# <a name="getschemas-method-"></a>Método getSchemas ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera os nomes de esquema disponíveis no banco de dados atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getSchemas()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getSchemas é especificado pelo método getSchemas na interface java.sql.DatabaseMetaData.  
  
 O conjunto de resultados retornado pelo método getSchemas contém as seguintes informações:  
  
|Nome|Type|DESCRIÇÃO|  
|----------|----------|-----------------|  
|TABLE_SCHEM|**Cadeia de caracteres**|O nome do esquema.|  
|TABLE_CATALOG|**Cadeia de caracteres**|O nome de catálogo para o esquema.|  
  
 Os resultados são ordenados por TABLE_CATALOG e, em seguida, por TABLE_SCHEM. Cada linha tem TABLE_SCHEM como a primeira coluna e TABLE_CATALOG como a segunda coluna.  
  
> [!NOTE]  
>  Para saber mais sobre os dados retornados pelo método getSchemas, consulte "sys.schemas (Transact-SQL)" nos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar o método getSchemas para retornar informações sobre o catálogo e os nomes de esquemas associados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando o argumento de conexão especificar o banco de dados a ser usado.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
