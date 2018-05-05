---
title: Método getVersionColumns (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getVersionColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6dd275d3-d9b2-4db7-938a-d4406c940a7a
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 722fd20c9210b14cb503ab3a0189815fa3cc83dd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getversioncolumns-method-sqlserverdatabasemetadata"></a>Método getVersionColumns (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma descrição das colunas de uma tabela que é atualizada automaticamente quando qualquer valor em uma linha é atualizado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getVersionColumns(java.lang.String catalog,  
                                            java.lang.String schema,  
                                            java.lang.String table)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *catalog*  
  
 Um **cadeia de caracteres** que contém o nome do catálogo.  
  
 *schema*  
  
 Um **cadeia de caracteres** que contém o padrão de nome de esquema.  
  
 *table*  
  
 Um **cadeia de caracteres** que contém o nome da tabela.  
  
## <a name="return-value"></a>Valor de retorno  
 Um [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getVersionColumns é especificado pelo método getVersionColumns na interface DatabaseMetadata.  
  
 O conjunto de resultados retornado pelo método getVersionColumns conterá as seguintes informações:  
  
|Nome|Tipo|Description|  
|----------|----------|-----------------|  
|SCOPE|**short**|Não há suporte do JDBC Driver.|  
|COLUMN_NAME|**String**|O nome da coluna.|  
|DATA_TYPE|**short**|O tipo de dados SQL de java.sql.Types.|  
|TYPE_NAME|**String**|O nome do tipo de dados.|  
|COLUMN_SIZE|**Int**|A precisão da coluna.|  
|BUFFER_LENGTH|**Int**|O comprimento da coluna em bytes.|  
|DECIMAL_DIGITS|**short**|A escala da coluna.|  
|PSEUDO_COLUMN|**short**|Indica se a coluna é uma pseudocoluna. Pode ser um dos seguintes valores:<br /><br /> versionColumnUnknown (0)<br /><br /> versionColumnNotPseudo (1)<br /><br /> versionColumnPseudo (2)|  
  
> [!NOTE]  
>  Para obter mais informações sobre os dados retornados pelo método getVersionColumns, consulte "sp_datatype_info (Transact-SQL)" em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Manuais Online.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar o método getVersionColumns para retornar informações sobre as colunas que são atualizados automaticamente na tabela Person. Contact o [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] banco de dados de exemplo.  
  
```  
public static void executeGetVersionColumns(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getVersionColumns("AdventureWorks", "Person", "Contact");  
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
  
  
