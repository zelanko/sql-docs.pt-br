---
title: Método getIndexInfo (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getIndexInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8a677cc6-8e33-4e57-8678-0849345aa8d0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d7d66a175522cd89cf4bd0aca567779244b0a385
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789804"
---
# <a name="getindexinfo-method-sqlserverdatabasemetadata"></a>Método getIndexInfo (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma descrição de índices e estatísticas da tabela fornecida.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getIndexInfo(java.lang.String cat,  
                                       java.lang.String schema,  
                                       java.lang.String table,  
                                       boolean unique,  
                                       boolean approximate)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *cat*  
  
 Uma **String** que contém o nome do catálogo.  
  
 *schema*  
  
 Uma **String** que contém o nome do esquema.  
  
 *table*  
  
 Uma **String** que contém o nome da tabela.  
  
 *unique*  
  
 **True** se apenas índices valores exclusivos serão retornados. **False** se todos os índices são retornados.  
  
 *approximate*  
  
 **True** se os resultados refletem os valores aproximados ou desatualizados. **False** se os resultados são precisos.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getIndexInfo é especificado pelo método getIndexInfo na interface DatabaseMetadata.  
  
 O conjunto de resultados retornado pelo método getIndexInfo conterá as seguintes informações:  
  
|Nome|Tipo|Descrição|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|O nome do banco de dados no qual a tabela especificada reside.|  
|TABLE_SCHEM|**String**|O esquema da tabela.|  
|TABLE_NAME|**String**|O nome da tabela.|  
|NON_UNIQUE|**booleano**|Indica se os valores de índice podem ser não exclusivos.|  
|INDEX_QUALIFIER|**String**|O nome do proprietário do índice. Ele será nulo quando TYPE for tableIndexStatistic.|  
|INDEX_NAME|**String**|O nome do índice.|  
|TYPE|**short**|O tipo do índice. Pode ser um dos seguintes valores:<br /><br /> tableIndexStatistic (0)<br /><br /> tableIndexClustered (1)<br /><br /> tableIndexHashed (2)<br /><br /> tableIndexOther (3)|  
|ORDINAL_POSITION|**short**|A posição ordinal da coluna no índice. A primeira coluna no índice é 1.|  
|COLUMN_NAME|**String**|O nome da coluna.|  
|ASC_OR_DESC|**String**|A ordem usada no agrupamento do índice. Pode ser um dos seguintes valores:<br /><br /> A (crescente)<br /><br /> D (decrescente)<br /><br /> NULL (não aplicável)<br /><br /> **Observação:** o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sempre retorna "A".|  
|CARDINALITY|**int**|O número de linhas na tabela ou os valores exclusivos no índice.|  
|PAGES|**int**|O número de páginas usadas para armazenar o índice ou a tabela.|  
|FILTER_CONDITION|**String**|A condição do filtro.<br /><br /> **Observação:** o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sempre retorna nulo.|  
  
> [!NOTE]  
>  Para saber mais sobre os dados retornados pelo método getIndexInfo, consulte "sp_indexes (Transact-SQL)" nos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar o método getIndexInfo para retornar informações sobre os índices e as estatísticas da tabela Person.Contact no banco de dados de exemplo do [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
public static void executeGetIndexInfo(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getIndexInfo("AdventureWorks", "Person", "Contact", false, true);  
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
  
  
