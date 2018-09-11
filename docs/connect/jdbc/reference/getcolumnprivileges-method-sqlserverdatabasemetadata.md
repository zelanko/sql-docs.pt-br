---
title: Método getColumnPrivileges (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getColumnPrivileges
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4ab6a671-9573-4b95-8c23-364306c60d25
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16c0b0314d4e0e3b2b28e81c118ef0533ba55768
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785044"
---
# <a name="getcolumnprivileges-method-sqlserverdatabasemetadata"></a>Método getColumnPrivileges (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma descrição dos direitos de acesso das colunas de uma tabela.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getColumnPrivileges(java.lang.String catalog,  
                                              java.lang.String schema,  
                                              java.lang.String table,  
                                              java.lang.String col)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *catalog*  
  
 Uma **String** que contém o nome do catálogo.  
  
 *schema*  
  
 Uma **String** que contém o nome do esquema.  
  
 *table*  
  
 Uma **String** que contém o nome da tabela.  
  
 *col*  
  
 Uma **String** que contém o nome da coluna.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getColumnPrivileges é especificado pelo método getColumnPrivileges na interface DatabaseMetadata.  
  
 O conjunto de resultados retornado pelo método getColumnPrivileges conterá as seguintes informações:  
  
|Nome|Tipo|Descrição|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|O nome do catálogo.|  
|TABLE_SCHEM|**String**|O nome do esquema da tabela.|  
|TABLE_NAME|**String**|O nome da tabela.|  
|COLUMN_NAME|**String**|O nome da coluna.|  
|GRANTOR|**String**|O objeto que concede o acesso.|  
|GRANTEE|**String**|O objeto que recebe o acesso.|  
|PRIVILEGE|**String**|O tipo de acesso concedido.|  
|IS_GRANTABLE|**String**|Indica se o usuário autorizado tem permissão para conceder acesso a outros usuários.|  
  
> [!NOTE]  
>  Para saber mais sobre os dados retornados pelo método getColumnPrivileges, consulte "sp_column_privileges (Transact-SQL)" nos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar o método getColumnPrivileges a fim de retornar direitos de acesso para a coluna FirstName na tabela Person.Contact no banco de dados de exemplo do [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
public static void executeGetColumnPrivileges(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getColumnPrivileges("AdventureWorks", "Person", "Contact", "FirstName");  
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
  
  
