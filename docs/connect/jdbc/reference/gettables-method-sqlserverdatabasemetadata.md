---
title: Método getTables (SQLServerDatabaseMetaData) | Microsoft Docs
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
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getTables
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a7514673-3457-4541-9560-28a8284ad9e3
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2b020065a3285cb93f3230e75a929b85f1c9a3ff
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="gettables-method-sqlserverdatabasemetadata"></a>Método getTables (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma descrição das tabelas disponíveis no padrão de nome de catálogo, esquema ou tabela fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getTables(java.lang.String catalog,  
                                    java.lang.String schema,  
                                    java.lang.String table,  
                                    java.lang.String[] types)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *catalog*  
  
 Um **cadeia de caracteres** que contém o nome do catálogo. Fornecer um nulo a esse parâmetro indica que o nome do catálogo não precisa ser usado.  
  
 *schema*  
  
 Um **cadeia de caracteres** que contém o padrão de nome de esquema. Fornecer um nulo a esse parâmetro indica que o nome de esquema não precisa ser usado.  
  
 *nome de tabela*  
  
 Um **cadeia de caracteres** que contém o padrão de nome de tabela.  
  
 *Tipos de*  
  
 Uma matriz de cadeia de caracteres que contém os tipos de tabelas a serem incluídos. Nulo indica que todos os tipos de tabelas devem ser incluídos.  
  
## <a name="return-value"></a>Valor de retorno  
 Um [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getTables é especificado pelo método getTables na interface DatabaseMetadata.  
  
 O conjunto de resultados retornado pelo método getTables conterá as seguintes informações:  
  
|Nome|Tipo|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|O nome do banco de dados no qual a tabela especificada reside.|  
|TABLE_SCHEM|**String**|O nome do esquema da tabela.|  
|TABLE_NAME|**String**|O nome da tabela.|  
|TABLE_TYPE|**String**|O tipo de tabela.|  
|REMARKS|**String**|A descrição da tabela.<br /><br /> **Observação:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] não retorna um valor para essa coluna.  |  
|TYPE_CAT|**String**|Não há suporte do JDBC Driver.|  
|TYPE_SCHEM|**String**|Não há suporte do JDBC Driver.|  
|TYPE_NAME|**String**|Não há suporte do JDBC Driver.|  
|SELF_REFERENCING_COL_NAME|**String**|Não há suporte do JDBC Driver.|  
|REF_GENERATION|**String**|Não há suporte do JDBC Driver.|  
  
> [!NOTE]  
>  Para obter mais informações sobre os dados retornados pelo método getTables, consulte "sp_tables (Transact-SQL)" em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Manuais Online.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar o método getTables para retornar as informações de descrição de tabela para a tabela Person. Contact o [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] banco de dados de exemplo.  
  
```  
public static void executeGetTables(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTables("AdventureWorks", "Person", "Contact", null);  
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
  
  
