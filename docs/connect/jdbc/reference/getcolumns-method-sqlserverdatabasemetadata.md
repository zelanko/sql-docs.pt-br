---
title: Método getColumns (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f173fa5d-e114-4a37-a5c4-2baad9ff3af1
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e1268316bb7a2038eb04da91fa438ebba88d0525
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32833681"
---
# <a name="getcolumns-method-sqlserverdatabasemetadata"></a>Método getColumns (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma descrição das colunas da tabela que estão disponíveis no catálogo especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getColumns(java.lang.String catalog,  
                                     java.lang.String schema,  
                                     java.lang.String table,  
                                     java.lang.String col)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *catalog*  
  
 Um **cadeia de caracteres** que contém o nome do catálogo.  
  
 *schema*  
  
 Um **cadeia de caracteres** que contém o padrão de nome de esquema.  
  
 *table*  
  
 Um **cadeia de caracteres** que contém o padrão de nome de tabela.  
  
 *col*  
  
 Um **cadeia de caracteres** que contém o padrão de nome de coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Um [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getColumns é especificado pelo método getColumns na interface DatabaseMetadata.  
  
 O conjunto de resultados retornado pelo método getColumns conterá as seguintes informações:  
  
|Nome|Tipo|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|O nome do catálogo.|  
|TABLE_SCHEM|**String**|O nome do esquema da tabela.|  
|TABLE_NAME|**String**|O nome da tabela.|  
|COLUMN_NAME|**String**|O nome da coluna.|  
|DATA_TYPE|**smallint**|O tipo de dados SQL de java.sql.Types.|  
|TYPE_NAME|**String**|O nome do tipo de dados.|  
|COLUMN_SIZE|**Int**|A precisão da coluna.|  
|BUFFER_LENGTH|**smallint**|Tamanho da transferência dos dados.|  
|DECIMAL_DIGITS|**smallint**|A escala da coluna.|  
|NUM_PREC_RADIX|**smallint**|A base da coluna.|  
|NULLABLE|**smallint**|Indica se a coluna é anulável. Pode ser um dos seguintes valores:<br /><br /> columnNoNulls (0)<br /><br /> columnNullable (1)|  
|REMARKS|**String**|Os comentários associados à coluna.<br /><br /> **Observação:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] sempre retorna null para essa coluna.  |  
|COLUMN_DEF|**String**|O valor padrão da coluna.|  
|SQL_DATA_TYPE|**smallint**|Valor do tipo de dados SQL conforme exibido no campo TYPE do descritor. Esta coluna é igual à coluna DATA_TYPE, com exceção dos tipos de dados datetime e interval do SQL-92. Esta coluna sempre retorna um valor.|  
|SQL_DATETIME_SUB|**smallint**|Código de subtipo para os tipos de dados datetime e interval do SQL-92. Para outros tipos de dados, esta coluna retorna NULL.|  
|CHAR_OCTET_LENGTH|**Int**|O número máximo de bytes na coluna.|  
|ORDINAL_POSITION|**Int**|O índice da coluna na tabela.|  
|IS_NULLABLE|**String**|Indica se a coluna permite valores nulos.|  
|SS_IS_SPARSE|**smallint**|Se a coluna for uma coluna esparsa, isso tem o valor 1; Caso contrário, 0. <sup>1</sup>|  
|SS_IS_COLUMN_SET|**smallint**|Se a coluna for a coluna esparsa column_set, seu valor será 1; caso contrário, será 0. <sup>1</sup>|  
|SS_IS_COMPUTED|**smallint**|Indica se uma coluna em um TABLE_TYPE é uma coluna computada. <sup>1</sup>|  
|IS_AUTOINCREMENT|**String**|"YES" se a coluna for incrementada automaticamente. "NO" se a coluna não for incrementada automaticamente. " "(cadeia de caracteres vazia) se o driver não puder determinar se a coluna foi incrementada automaticamente. <sup>1</sup>|  
|SS_UDT_CATALOG_NAME|**String**|O nome do catálogo que contém o tipo definido pelo usuário (UDT). <sup>1</sup>|  
|SS_UDT_SCHEMA_NAME|**String**|O nome do esquema que contém o UDT (tipo definido pelo usuário). <sup>1</sup>|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**String**|O UDT (tipo definido pelo usuário) do nome totalmente qualificado. <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**String**|O nome do catálogo em que é definido um nome da coleção de esquemas XML. Se o nome do catálogo não pode ser encontrado, essa variável conterá uma cadeia de caracteres vazia. <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**String**|O nome do esquema no qual é definido um nome da coleção de esquemas XML. Se não for possível localizar o nome do esquema, essa cadeia de caracteres estará vazia. <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_NAME|**String**|O nome de uma coleção de esquemas XML. Se não for possível localizar o nome, essa cadeia de caracteres estará vazia. <sup>1</sup>|  
|SS_DATA_TYPE|**tinyint**|O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de dados que é usado pelos procedimentos armazenados estendidos.<br /><br /> **Observação** para obter mais informações sobre os tipos de dados retornado por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], consulte "Tipos de dados (Transact-SQL)" em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Manuais Online.|  
  
 (1) essa coluna não estará presente se você estiver se conectando [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)].  
  
> [!NOTE]  
>  Para obter mais informações sobre os dados retornados pelo método getColumns, consulte "sp_columns (Transact-SQL)" em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Manuais Online.  
  
 No [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0, você verá o seguinte comportamento muda de versões anteriores do Driver JDBC:  
  
 A coluna DATA_TYPE tem as seguintes alterações:  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Tipo de dados|Tipo de retorno no JDBC Driver 2.0 (ou, se conectado a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)]) e constante numérica associada|Tipo de retorno no JDBC Driver 3.0 quando conectado a [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)] ou posterior|  
|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|  
|tipo definido pelo usuário superior a 8 KB|LONGVARBINARY (-4)|VARBINARY (-3)|  
|geografia|LONGVARBINARY (-4)|VARBINARY (-3)|  
|geometria|LONGVARBINARY (-4)|VARBINARY (-3)|  
|varbinary(max)|LONGVARBINARY (-4)|VARBINARY (-3)|  
|nvarchar(max)|LONGVARCHAR (-1) ou LONGNVARCHAR (JDBC 4) (-16)|VARCHAR (12) ou NVARCHAR (JDBC 4) (-9)|  
|varchar(max)|LONGVARCHAR (-1)|VARCHAR (12)|  
|time|VARCHAR (12) ou NVARCHAR (JDBC 4) (-9)|TIME (-154)|  
|date|VARCHAR (12) ou NVARCHAR (JDBC 4) (-9)|DATA (91)|  
|datetime2|VARCHAR (12) ou NVARCHAR (JDBC 4) (-9)|TIMESTAMP (93)|  
|datetimeoffset|VARCHAR (12) ou NVARCHAR (JDBC 4) (-9)|microsoft.sql.Types.DATETIMEOFFSET  (-155)|  
  
 A coluna COLUMN_SIZE tem as seguintes alterações:  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Tipo de dados|Tipo de retorno no JDBC Driver 2.0|Tipo de retorno no JDBC Driver 3.0|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|nvarchar(max)|1073741823|2147483647 (metadados do banco de dados)|  
|xml|1073741823|2147483647 (metadados do banco de dados)|  
|tipo definido pelo usuário com menos de ou igual a 8 KB|8 KB (conjunto de resultados e metadados de parâmetro)|Tamanho real retornado pelo procedimento armazenado.|  
|time||O comprimento em caracteres da representação de cadeia de caracteres do tipo, supondo a precisão máxima permitida do componente de segundos fracionais.|  
|date||igual à hora|  
|datetime2||igual à hora|  
|datetimeoffset||igual à hora|  
  
 A coluna BUFFER_LENGTH tem a seguinte alteração:  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Tipo de dados|Tipo de retorno no JDBC Driver 2.0|Tipo de retorno no JDBC Driver 3.0|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|tipo definido pelo usuário superior a 8 KB||2147483647|  
  
 A coluna TYPE_NAME tem as seguintes alterações:  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Tipo de dados|Tipo de retorno no JDBC Driver 2.0|Tipo de retorno no JDBC Driver 3.0|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|varchar(max)|text|varchar|  
|varbinary(max)|image|varbinary|  
  
 A coluna DECIMAL_DIGITS tem as seguintes alterações:  
  
|Tipo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]|JDBC Driver 2.0|JDBC Driver 3.0|  
|--------------------------------------------------------------|---------------------|---------------------|  
|time|nulo|7 (ou menor se especificado)|  
|date|nulo|nulo|  
|datetime2|nulo|7 (ou menor se especificado)|  
|datetimeoffset|nulo|7 (ou menor se especificado)|  
  
 A coluna SQL_DATA_TYPE tem as seguintes alterações:  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Tipo de dados|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 2008 valor de dados em Driver JDBC 2.0|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 2008 valor de dados no JDBC Driver 3.0|  
|-------------------------------------------------------------------|--------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|  
|varchar(max)|-10|-9|  
|nvarchar(max)|-1|-9|  
|xml|-10|-152|  
|tipo definido pelo usuário com menos de ou igual a 8 KB|-3|-151|  
|tipo definido pelo usuário superior a 8 KB|Não disponível no JDBC Driver 2.0|-151|  
|geografia|-4|-151|  
|geometria|-4|-151|  
|hierarchyid|-4|-151|  
|time|-9|92|  
|date|-9|91|  
|datetime2|-9|93|  
|datetimeoffset|-9|-155|  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar o método getColumns para retornar informações para a tabela Person. Contact o [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] banco de dados de exemplo.  
  
```  
import java.sql.*;  
public class c1 {  
   public static void main(String[] args) {  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;databaseName=AdventureWorks;integratedsecurity=true";  
  
      Connection con = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
         DatabaseMetaData dbmd = con.getMetaData();  
         rs = dbmd.getColumns("AdventureWorks", "Person", "Contact", "FirstName");  
  
         ResultSet r = dbmd.getColumns(null, null, "Contact", null);  
         ResultSetMetaData rm = r.getMetaData();   
         int noofcols = rm.getColumnCount();  
  
         if (r.next())  
            for (int i = 0 ; i < noofcols ; i++ )  
            System.out.println(rm.getColumnName( i + 1 ) + ": \t\t" + r.getString( i + 1 ));  
      }  
  
      catch (Exception e) {}  
      finally {}  
   }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
