---
title: "Método getTablePrivileges (SQLServerDatabaseMetaData) | Microsoft Docs"
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
- SQLServerDatabaseMetaData.getTablePrivileges
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0610d667-a16d-4201-a14b-0a40048911e1
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2c075e59e1e5ea26bb1f2649076429c5a31df393
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="gettableprivileges-method-sqlserverdatabasemetadata"></a>Método getTablePrivileges (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma descrição dos direitos de acesso de cada tabela, disponível no padrão de nome de catálogo, esquema ou tabela fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getTablePrivileges(java.lang.String catalog,  
                                             java.lang.String schema,  
                                             java.lang.String table)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Catálogo*  
  
 Um **cadeia de caracteres** que contém o nome do catálogo. Fornecer um nulo a esse parâmetro indica que o nome do catálogo não precisa ser usado.  
  
 *esquema*  
  
 Um **cadeia de caracteres** que contém o padrão de nome de esquema. Fornecer um nulo a esse parâmetro indica que o nome de esquema não precisa ser usado.  
  
 *table*  
  
 Um **cadeia de caracteres** que contém o padrão de nome de tabela.  
  
## <a name="return-value"></a>Valor de retorno  
 Um [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getTablePrivileges é especificado pelo método getTablePrivileges na interface DatabaseMetadata.  
  
 O conjunto de resultados retornado pelo método getTablePrivileges conterá as seguintes informações:  
  
|Nome|Tipo|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**Cadeia de caracteres**|O nome do catálogo.|  
|TABLE_SCHEM|**Cadeia de caracteres**|O nome do esquema da tabela.|  
|TABLE_NAME|**Cadeia de caracteres**|O nome da tabela.|  
|GRANTOR|**Cadeia de caracteres**|O objeto que concede o acesso.|  
|GRANTEE|**Cadeia de caracteres**|O objeto que recebe o acesso.|  
|PRIVILEGE|**Cadeia de caracteres**|O tipo de acesso concedido.|  
|IS_GRANTABLE|**Cadeia de caracteres**|Indica se o usuário autorizado tem permissão para conceder acesso a outros usuários.|  
  
> [!NOTE]  
>  Para obter mais informações sobre os dados retornados pelo método getTablePrivileges, consulte "sp_table_privileges (Transact-SQL)" em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Manuais Online.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar o método getTablePrivileges para retornar os direitos de acesso para a tabela Person. Contact o [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] banco de dados de exemplo.  
  
```  
public static void executeGetTablePrivileges(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTablePrivileges("AdventureWorks", "Person", "Contact");  
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
  
  

