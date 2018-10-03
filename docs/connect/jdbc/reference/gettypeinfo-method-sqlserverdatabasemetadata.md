---
title: Método getTypeInfo (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTypeInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 23208f01-c1bf-4235-b29c-9051d3df59a3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 40ca58f33dec39a1ec6d39979c7f6f0103acf8b2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47682714"
---
# <a name="gettypeinfo-method-sqlserverdatabasemetadata"></a>Método getTypeInfo (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma descrição de todos os tipos SQL padrão que têm o suporte do banco de dados atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getTypeInfo()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getTypeInfo é especificado pelo método getTypeInfo na interface DatabaseMetadata.  
  
 O conjunto de resultados retornado pelo método getTypeInfo conterá as seguintes informações:  
  
|Nome|Tipo|Descrição|  
|----------|----------|-----------------|  
|TYPE_NAME|**String**|O nome do tipo de dados.|  
|DATA_TYPE|**short**|O tipo de dados SQL de java.sql.Types.|  
|PRECISION|**int**|O número total de dígitos significativos.|  
|LITERAL_PREFIX|**String**|Um ou mais caracteres usados antes de uma constante.|  
|LITERAL_SUFFIX|**String**|Um ou mais caracteres usados para terminar uma constante.|  
|CREATE_PARAMS|**String**|A descrição dos parâmetros de criação do tipo de dados.|  
|NULLABLE|**short**|Indica se a coluna pode conter um valor nulo. Pode ser um dos seguintes valores:<br /><br /> typeNoNulls (0)<br /><br /> typeNullable (1)<br /><br /> typeNullableUnknown (2)|  
|CASE_SENSITIVE|**booleano**|Indica se o tipo de dados diferencia maiúsculas de minúsculas. "**true**" se o tipo diferenciar maiúsculas de minúsculas; caso contrário, "**false**".|  
|SEARCHABLE|**short**|Indica se a coluna pode ser usada em uma cláusula SQL WHERE. Pode ser um dos seguintes valores:<br /><br /> typePredNone (0)<br /><br /> typePredChar (1)<br /><br /> typePredBasic (2)<br /><br /> typeSeachable (3)|  
|UNSIGNED_ATTRIBUTE|**booleano**|Indica o sinal do tipo de dados. "**true**" se o tipo não tiver sinal; caso contrário, "**false**".|  
|FIXED_PREC_SCALE|**booleano**|Indica que o tipo de dados pode ser um valor money. "**true**" se o tipo de dados for money; caso contrário, "**false**".|  
|AUTO_INCREMENT|**booleano**|Indica que o tipo de dados pode ser incrementado automaticamente. "**true**" se o tipo puder ser incrementado automaticamente; caso contrário, "**false**".|  
|LOCAL_TYPE_NAME|**String**|O nome localizado do tipo de dados.|  
|MINIMUM_SCALE|**short**|O número máximo de dígitos à direita da vírgula decimal.|  
|MAXIMUM_SCALE|**short**|O número mínimo de dígitos à direita da vírgula decimal.|  
|SQL_DATA_TYPE|**int**|Não há suporte do JDBC Driver.|  
|SQL_DATETIME_SUB|**int**|Não há suporte do JDBC Driver.|  
|NUM_PREC_RADIX|**int**|O número de bits ou dígitos para calcular o número máximo que uma coluna pode conter.|  
|INTERVAL_PRECISION|**smallint**|O valor de precisão do intervalo à esquerda.|  
|USERTYPE|**smallint**|O valor **usertype** da tabela **systypes**. Para obter mais informações, consulte os Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
  
> [!NOTE]  
>  Para saber mais sobre os dados retornados pelo método getTypeInfo, consulte "sp_datatype_info (Transact-SQL)" nos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar o método getTypeInfo para retornar informações sobre os tipos de dados usados em um banco de dados do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (ou posteriores).  
  
```  
public static void executeGetTypeInfo(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTypeInfo();  
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
  
  
