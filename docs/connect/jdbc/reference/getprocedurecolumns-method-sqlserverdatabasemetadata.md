---
title: Método getProcedureColumns (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getProcedureColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4f0df8fe-3cd6-46e4-ae3c-dc23c35676b2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1767519cc2f36bac4a70da84efeb8da9e2a1ec3c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67980756"
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
  
#### <a name="parameters"></a>parâmetros  
 *sCatalog*  
  
 Uma **String** que contém o nome do catálogo. Fornecer um nulo a esse parâmetro indica que o nome do catálogo não precisa ser usado.  
  
 *sSchema*  
  
 Uma **String** que contém o padrão de nome do esquema. Fornecer um nulo a esse parâmetro indica que o nome de esquema não precisa ser usado.  
  
 *proc*  
  
 Uma **String** que contém o padrão de nome do procedimento.  
  
 *col*  
  
 Uma **String** que contém o nome da coluna. Fornecer um nulo a este parâmetro retorna uma linha para cada coluna.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getProcedureColumns é especificado pelo método getProcedureColumns na interface java.sql.DatabaseMetaData.  
  
 O conjunto de resultados retornado pelo método getProcedureColumns conterá as seguintes informações:  
  
|Nome|Type|Descrição|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**Cadeia de caracteres**|O nome do banco de dados no qual o procedimento armazenado especificado reside.|  
|PROCEDURE_SCHEM|**Cadeia de caracteres**|O esquema para o procedimento armazenado.|  
|PROCEDURE_NAME|**Cadeia de caracteres**|O nome do procedimento armazenado.|  
|COLUMN_NAME|**Cadeia de caracteres**|O nome da coluna.|  
|COLUMN_TYPE|**short**|O tipo da coluna. Pode ser um dos seguintes valores:<br /><br /> procedureColumnUnknown (0)<br /><br /> procedureColumnIn (1)<br /><br /> procedureColumnInOut (2)<br /><br /> procedureColumnOut (4)<br /><br /> procedureColumnReturn (5)<br /><br /> procedureColumnResult (3)|  
|DATA_TYPE|**smallint**|O tipo de dados SQL de java.sql.Types.|  
|TYPE_NAME|**Cadeia de caracteres**|O nome do tipo de dados.|  
|PRECISION|**int**|O número total de dígitos significativos.|  
|LENGTH|**int**|O comprimento dos dados em bytes.|  
|SCALE|**short**|O número de dígitos à direita da vírgula decimal.|  
|RADIX|**short**|A base para tipos numéricos.|  
|NULLABLE|**short**|Indica se a coluna pode conter um valor nulo. Pode ser um dos seguintes valores:<br /><br /> procedureNoNulls (0)<br /><br /> procedureNullable (1)<br /><br /> procedureNullableUnknown (2)|  
|COMENTÁRIOS|**Cadeia de caracteres**|A descrição da coluna de procedimento.<br /><br /> <br /><br /> **Observação:** o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não retorna um valor para essa coluna.|  
|COLUMN_DEF|**Cadeia de caracteres**|O valor padrão da coluna.|  
|SQL_DATA_TYPE|**smallint**|Esta coluna é igual à coluna **DATA_TYPE**, com exceção dos tipos de dados **datetime** e **interval** ISO.|  
|SQL_DATETIME_SUB|**smallint**|O subcódigo de **interval** ISO de **datetime**, se o valor de **SQL_DATA_TYPE** for **SQL_DATETIME** ou **SQL_INTERVAL**. Para tipos de dados diferentes de **datetime** e **intervalo** ISO, essa coluna é NULL.|  
|CHAR_OCTET_LENGTH|**int**|O número máximo de bytes na coluna.|  
|ORDINAL_POSITION|**int**|O índice da coluna na tabela.|  
|IS_NULLABLE|**Cadeia de caracteres**|Indica se a coluna permite valores nulos.|  
|SS_TYPE_CATALOG_NAME|**Cadeia de caracteres**|O nome do catálogo que contém o UDT (tipo definido pelo usuário).|  
|SS_TYPE_SCHEMA_NAME|**Cadeia de caracteres**|O nome do esquema que contém o UDT (tipo definido pelo usuário).|  
|SS_UDT_CATALOG_NAME|**Cadeia de caracteres**|O UDT (tipo definido pelo usuário) do nome totalmente qualificado.|  
|SS_UDT_SCHEMA_NAME|**Cadeia de caracteres**|O nome do catálogo em que é definido um nome da coleção de esquemas XML. Se não for possível localizar o nome do catálogo, essa variável conterá uma cadeia de caracteres vazia.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**Cadeia de caracteres**|O nome do esquema no qual é definido um nome da coleção de esquemas XML. Se não for possível localizar o nome do esquema, essa cadeia de caracteres estará vazia.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**Cadeia de caracteres**|O nome de uma coleção de esquemas XML. Se não for possível localizar o nome, essa cadeia de caracteres estará vazia.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**Cadeia de caracteres**|O nome do catálogo que contém o UDT (tipo definido pelo usuário).|  
|SS_XML_SCHEMACOLLECTION_NAME|**Cadeia de caracteres**|O nome do esquema que contém o UDT (tipo definido pelo usuário).|  
|SS_DATA_TYPE|**tinyint**|O tipo de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usado por procedimentos armazenados estendidos.<br /><br /> <br /><br /> **Observação:** Para obter mais informações sobre os tipos de dados retornados pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], confira "Tipos de dados (Transact-SQL)" nos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
  
> [!NOTE]  
>  Para saber mais sobre os dados retornados pelo método getProcedureColumns, consulte "sp_sproc_columns (Transact-SQL)" nos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar o método getProcedureColumns para retornar informações sobre o procedimento armazenado uspGetBillOfMaterials no banco de dados de exemplo do [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
