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
ms.openlocfilehash: d0fe3b01fd02bf48fb5f38707530e3b3344133e6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67979222"
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
  
#### <a name="parameters"></a>parâmetros  
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
  
## <a name="remarks"></a>Comentários  
 Esse método getTablePrivileges é especificado pelo método getTablePrivileges na interface java.sql.DatabaseMetaData.  
  
 O conjunto de resultados retornado pelo método getTablePrivileges conterá as seguintes informações:  
  
|Nome|Type|DESCRIÇÃO|  
|----------|----------|-----------------|  
|TABLE_CAT|**Cadeia de caracteres**|O nome do catálogo.|  
|TABLE_SCHEM|**Cadeia de caracteres**|O nome do esquema da tabela.|  
|TABLE_NAME|**Cadeia de caracteres**|O nome da tabela.|  
|GRANTOR|**Cadeia de caracteres**|O objeto que concede o acesso.|  
|GRANTEE|**Cadeia de caracteres**|O objeto que recebe o acesso.|  
|PRIVILEGE|**Cadeia de caracteres**|O tipo de acesso concedido.|  
|IS_GRANTABLE|**Cadeia de caracteres**|Indica se o usuário autorizado tem permissão para conceder acesso a outros usuários.|  
  
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
  
  
