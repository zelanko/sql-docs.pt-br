---
title: Método getTablePrivileges (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTablePrivileges
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0610d667-a16d-4201-a14b-0a40048911e1
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 43bd46b81a6df2193181e4384b3b19d8d32c2929
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
 Um **cadeia de caracteres** que contém o nome do catálogo. Fornecer um nulo a esse parâmetro indica que o nome do catálogo não precisa ser usado.  
  
 *schema*  
  
 Um **cadeia de caracteres** que contém o padrão de nome de esquema. Fornecer um nulo a esse parâmetro indica que o nome de esquema não precisa ser usado.  
  
 *table*  
  
 Um **cadeia de caracteres** que contém o padrão de nome de tabela.  
  
## <a name="return-value"></a>Valor de retorno  
 Um [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getTablePrivileges é especificado pelo método getTablePrivileges na interface DatabaseMetadata.  
  
 O conjunto de resultados retornado pelo método getTablePrivileges conterá as seguintes informações:  
  
|Nome|Tipo|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|O nome do catálogo.|  
|TABLE_SCHEM|**String**|O nome do esquema da tabela.|  
|TABLE_NAME|**String**|O nome da tabela.|  
|GRANTOR|**String**|O objeto que concede o acesso.|  
|GRANTEE|**String**|O objeto que recebe o acesso.|  
|PRIVILEGE|**String**|O tipo de acesso concedido.|  
|IS_GRANTABLE|**String**|Indica se o usuário autorizado tem permissão para conceder acesso a outros usuários.|  
  
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
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
