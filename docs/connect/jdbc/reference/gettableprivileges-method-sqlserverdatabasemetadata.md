---
title: Método getTablePrivileges (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTablePrivileges
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0610d667-a16d-4201-a14b-0a40048911e1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 26c1630042b4f33230f37ec979de7bfa643b283b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802606"
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
 *catalog*  
  
 Uma **String** que contém o nome do catálogo. Fornecer um nulo a esse parâmetro indica que o nome do catálogo não precisa ser usado.  
  
 *schema*  
  
 Uma **String** que contém o padrão de nome do esquema. Fornecer um nulo a esse parâmetro indica que o nome de esquema não precisa ser usado.  
  
 *table*  
  
 Uma **String** que contém o padrão de nome de tabela.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getTablePrivileges é especificado pelo método getTablePrivileges na interface java.sql.DatabaseMetaData.  
  
 O conjunto de resultados retornado pelo método getTablePrivileges conterá as seguintes informações:  
  
|Nome|Tipo|Descrição|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|O nome do catálogo.|  
|TABLE_SCHEM|**String**|O nome do esquema da tabela.|  
|TABLE_NAME|**String**|O nome da tabela.|  
|GRANTOR|**String**|O objeto que concede o acesso.|  
|GRANTEE|**String**|O objeto que recebe o acesso.|  
|PRIVILEGE|**String**|O tipo de acesso concedido.|  
|IS_GRANTABLE|**String**|Indica se o usuário autorizado tem permissão para conceder acesso a outros usuários.|  
  
> [!NOTE]  
>  Para saber mais sobre os dados retornados pelo método getTablePrivileges, consulte "sp_table_privileges (Transact-SQL)" nos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar o método getTablePrivileges para retornar os direitos de acesso para a tabela Person.Contact no banco de dados de exemplo do [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
