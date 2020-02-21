---
title: Método getCatalogs (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getCatalogs
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7f8bd0f1-f340-4bb9-b559-0a6176124033
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 786f55e436b9582eaed875f8c7cd265b1d3e2cc5
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67953451"
---
# <a name="getcatalogs-method-sqlserverdatabasemetadata"></a>Método getCatalogs (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera os nomes de catálogo disponíveis no servidor conectado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getCatalogs()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 O método getCatalogs é especificado pelo método getCatalogs na interface java.sql.DatabaseMetaData.  
  
> [!NOTE]  
>  No SQL Azure, você deve se conectar ao banco de dados mestre para chamar **SQLServerDatabaseMetaData.getCatalogs**. O SQL Azure não é compatível com o retorno de todo o conjunto de catálogos de um banco de dados do usuário. **SQLServerDatabaseMetaData.getCatalogs** usa a exibição sys.databases para obter os catálogos. Veja a discussão de permissões em [sys.database_usage (Banco de Dados SQL do Azure)](../../../relational-databases/system-catalog-views/sys-database-usage-azure-sql-database.md) para entender o comportamento de **SQLServerDatabaseMetaData.getCatalogs** no SQL Azure.  
  
 O conjunto de resultados retornado pelo método getCatalogs conterá as seguintes informações:  
  
|Nome|Type|Descrição|  
|----------|----------|-----------------|  
|TABLE_CAT|**Cadeia de caracteres**|O nome do catálogo, inclusive bancos de dados do sistema no [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar o método getCatalogs para retornar os nomes de todos os bancos de dados contidos no [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], inclusive os bancos de dados do sistema.  
  
```  
public static void executeGetCatalogs(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getCatalogs();  
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
  
  
