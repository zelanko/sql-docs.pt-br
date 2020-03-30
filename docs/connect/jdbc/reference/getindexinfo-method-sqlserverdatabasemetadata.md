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
ms.openlocfilehash: 8dd512236aa3070ce299756d4e4294c79ac2e94a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67982794"
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
  
#### <a name="parameters"></a>parâmetros  
 *cat*  
  
 Uma **String** que contém o nome do catálogo.  
  
 *schema*  
  
 Uma **String** que contém o nome do esquema.  
  
 *table*  
  
 Uma **String** que contém o nome da tabela.  
  
 *unique*  
  
 **true** se forem retornados apenas os índices para valores exclusivos. **false** se forem retornados todos os índices.  
  
 *approximate*  
  
 **true** se os resultados refletirem valores aproximados ou desatualizados. **false** se os resultados forem precisos.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getIndexInfo é especificado pelo método getIndexInfo na interface java.sql.DatabaseMetaData.  
  
 O conjunto de resultados retornado pelo método getIndexInfo conterá as seguintes informações:  
  
|Nome|Type|DESCRIÇÃO|  
|----------|----------|-----------------|  
|TABLE_CAT|**Cadeia de caracteres**|O nome do banco de dados no qual a tabela especificada reside.|  
|TABLE_SCHEM|**Cadeia de caracteres**|O esquema da tabela.|  
|TABLE_NAME|**Cadeia de caracteres**|O nome da tabela.|  
|NON_UNIQUE|**booleano**|Indica se os valores de índice podem ser não exclusivos.|  
|INDEX_QUALIFIER|**Cadeia de caracteres**|O nome do proprietário do índice. Ele será nulo quando TYPE for tableIndexStatistic.|  
|INDEX_NAME|**Cadeia de caracteres**|O nome do índice.|  
|TYPE|**short**|O tipo do índice. Pode ser um dos seguintes valores:<br /><br /> tableIndexStatistic (0)<br /><br /> tableIndexClustered (1)<br /><br /> tableIndexHashed (2)<br /><br /> tableIndexOther (3)|  
|ORDINAL_POSITION|**short**|A posição ordinal da coluna no índice. A primeira coluna no índice é 1.|  
|COLUMN_NAME|**Cadeia de caracteres**|O nome da coluna.|  
|ASC_OR_DESC|**Cadeia de caracteres**|A ordem usada na ordenação do índice. Pode ser um dos seguintes valores:<br /><br /> A (crescente)<br /><br /> D (decrescente)<br /><br /> NULL (não aplicável)<br /><br /> **Observação:** o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sempre retorna "A".|  
|CARDINALITY|**int**|O número de linhas na tabela ou os valores exclusivos no índice.|  
|PAGES|**int**|O número de páginas usadas para armazenar o índice ou a tabela.|  
|FILTER_CONDITION|**Cadeia de caracteres**|A condição do filtro.<br /><br /> **Observação:** o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sempre retorna nulo.|  
  
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
  
  
