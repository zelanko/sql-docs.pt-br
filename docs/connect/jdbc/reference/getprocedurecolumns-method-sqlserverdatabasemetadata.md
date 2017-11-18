---
title: "Método getProcedureColumns (SQLServerDatabaseMetaData) | Microsoft Docs"
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
- SQLServerDatabaseMetaData.getProcedureColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4f0df8fe-3cd6-46e4-ae3c-dc23c35676b2
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 847a037a1721e6ecd517d78f99d96b0ef2754aba
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getprocedurecolumns-method-sqlserverdatabasemetadata"></a>Método getProcedureColumns (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma descrição dos parâmetros de procedimento armazenado e das colunas de resultado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getProcedureColumns(java.lang.String sCatalog,  
                                              java.lang.String sSchema,  
                                              java.lang.String proc,  
                                              java.lang.String col)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sCatalog*  
  
 Um **cadeia de caracteres** que contém o nome do catálogo. Fornecer um nulo a esse parâmetro indica que o nome do catálogo não precisa ser usado.  
  
 *SO*  
  
 Um **cadeia de caracteres** que contém o padrão de nome de esquema. Fornecer um nulo a esse parâmetro indica que o nome de esquema não precisa ser usado.  
  
 *proc*  
  
 Um **cadeia de caracteres** que contém o padrão de nome de procedimento.  
  
 *col*  
  
 Um **cadeia de caracteres** que contém o padrão de nome de coluna. Fornecer um nulo a este parâmetro retorna uma linha para cada coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Um [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getProcedureColumns é especificado pelo método getProcedureColumns na interface DatabaseMetadata.  
  
 O conjunto de resultados retornado pelo método getProcedureColumns conterá as seguintes informações:  
  
|Nome|Tipo|Description|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**Cadeia de caracteres**|O nome do banco de dados no qual o procedimento armazenado especificado reside.|  
|PROCEDURE_SCHEM|**Cadeia de caracteres**|O esquema para o procedimento armazenado.|  
|PROCEDURE_NAME|**Cadeia de caracteres**|O nome do procedimento armazenado.|  
|COLUMN_NAME|**Cadeia de caracteres**|O nome da coluna.|  
|COLUMN_TYPE|**curto**|O tipo da coluna. Pode ser um dos seguintes valores:<br /><br /> procedureColumnUnknown (0)<br /><br /> procedureColumnIn (1)<br /><br /> procedureColumnInOut (2)<br /><br /> procedureColumnOut (4)<br /><br /> procedureColumnReturn (5)<br /><br /> procedureColumnResult (3)|  
|DATA_TYPE|**smallint**|O tipo de dados SQL de java.sql.Types.|  
|TYPE_NAME|**Cadeia de caracteres**|O nome do tipo de dados.|  
|PRECISION|**int**|O número total de dígitos significativos.|  
|LENGTH|**int**|O comprimento dos dados em bytes.|  
|SCALE|**curto**|O número de dígitos à direita da vírgula decimal.|  
|RADIX|**curto**|A base para tipos numéricos.|  
|NULLABLE|**curto**|Indica se a coluna pode conter um valor nulo. Pode ser um dos seguintes valores:<br /><br /> procedureNoNulls (0)<br /><br /> procedureNullable (1)<br /><br /> procedureNullableUnknown (2)|  
|REMARKS|**Cadeia de caracteres**|A descrição da coluna de procedimento.<br /><br /> <br /><br /> **Observação:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] não retorna um valor para essa coluna.|  
|COLUMN_DEF|**Cadeia de caracteres**|O valor padrão da coluna.|  
|SQL_DATA_TYPE|**smallint**|Essa coluna é o mesmo que o **DATA_TYPE** coluna, exceto para o **datetime** e ISO **intervalo** tipos de dados.|  
|SQL_DATETIME_SUB|**smallint**|O **datetime** ISO **intervalo** subcódigo se o valor de **SQL_DATA_TYPE** é **SQL_DATETIME** ou **SQL_INTERVAL**. Para tipos de dados diferente de **datetime** e ISO **intervalo**, essa coluna será NULL.|  
|CHAR_OCTET_LENGTH|**int**|O número máximo de bytes na coluna.|  
|ORDINAL_POSITION|**int**|O índice da coluna na tabela.|  
|IS_NULLABLE|**Cadeia de caracteres**|Indica se a coluna permite valores nulos.|  
|SS_TYPE_CATALOG_NAME|**Cadeia de caracteres**|O nome do catálogo que contém o tipo definido pelo usuário (UDT).|  
|SS_TYPE_SCHEMA_NAME|**Cadeia de caracteres**|O nome do esquema que contém o UDT (tipo definido pelo usuário).|  
|SS_UDT_CATALOG_NAME|**Cadeia de caracteres**|O UDT (tipo definido pelo usuário) do nome totalmente qualificado.|  
|SS_UDT_SCHEMA_NAME|**Cadeia de caracteres**|O nome do catálogo em que é definido um nome da coleção de esquemas XML. Se o nome do catálogo não pode ser encontrado, essa variável conterá uma cadeia de caracteres vazia.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**Cadeia de caracteres**|O nome do esquema no qual é definido um nome da coleção de esquemas XML. Se não for possível localizar o nome do esquema, essa cadeia de caracteres estará vazia.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**Cadeia de caracteres**|O nome de uma coleção de esquemas XML. Se não for possível localizar o nome, essa cadeia de caracteres estará vazia.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**Cadeia de caracteres**|O nome do catálogo que contém o tipo definido pelo usuário (UDT).|  
|SS_XML_SCHEMACOLLECTION_NAME|**Cadeia de caracteres**|O nome do esquema que contém o UDT (tipo definido pelo usuário).|  
|SS_DATA_TYPE|**tinyint**|O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de dados que é usado pelos procedimentos armazenados estendidos.<br /><br /> <br /><br /> **Observação:** para obter mais informações sobre os tipos de dados retornado por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], consulte "Tipos de dados (Transact-SQL)" em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Manuais Online.|  
  
> [!NOTE]  
>  Para obter mais informações sobre os dados retornados pelo método getProcedureColumns, consulte "sp_sproc_columns (Transact-SQL)" em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Manuais Online.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar o método getProcedureColumns para retornar informações sobre o procedimento armazenado uspGetBillOfMaterials o [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] banco de dados de exemplo.  
  
```  
public static void executeGetProcedureColumns(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getProcedureColumns(null, null, "uspGetBillOfMaterials", null);  
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
 [Membros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

