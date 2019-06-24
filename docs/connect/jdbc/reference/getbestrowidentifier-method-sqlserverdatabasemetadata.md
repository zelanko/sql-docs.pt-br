---
title: Método getBestRowIdentifier (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getBestRowIdentifier
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c19e9ca6-2a53-4a0c-91ab-80090c3f7229
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b08c8ffed61f90260617395f3c4df89b64dd6e0e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66799935"
---
# <a name="getbestrowidentifier-method-sqlserverdatabasemetadata"></a>Método getBestRowIdentifier (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma descrição do conjunto de colunas ideal de uma tabela que identifica exclusivamente uma linha.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getBestRowIdentifier(java.lang.String catalog,  
                                               java.lang.String schema,  
                                               java.lang.String table,  
                                               int scope,  
                                               boolean nullable)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *catalog*  
  
 Uma **String** que contém o nome do catálogo.  
  
 *schema*  
  
 Uma **String** que contém o nome do esquema.  
  
 *table*  
  
 Uma **String** que contém o nome da tabela.  
  
 *escopo*  
  
 Um **int** que indica o escopo de interesse. Valores podem incluir o seguinte:  
  
 bestRowTemporary (0)  
  
 bestRowTransaction (1)  
  
 bestRowSession (2)  
  
 *nullable*  
  
 **True** para incluir colunas que permitem valor nulas. Caso contrário, **false**.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getBestRowIdentifier é especificado pelo método getBestRowIdentifier na interface DatabaseMetadata.  
  
 O conjunto de resultados retornado pelo método getBestRowIdentifier conterá as seguintes informações:  
  
|Nome|Tipo|Descrição|  
|----------|----------|-----------------|  
|SCOPE|short|O escopo dos resultados retornados. Pode ser um dos seguintes valores:<br /><br /> bestRowTemporary (0)<br /><br /> bestRowTransaction (1)<br /><br /> bestRowSession (2)|  
|COLUMN_NAME|Cadeia de caracteres|O nome da coluna.|  
|DATA_TYPE|short|O tipo de dados SQL de java.sql.Types.|  
|TYPE_NAME|Cadeia de caracteres|O nome do tipo de dados.|  
|COLUMN_SIZE|INT|A precisão da coluna.|  
|BUFFER_LENGTH|INT|O comprimento do buffer.|  
|DECIMAL_DIGITS|short|A escala da coluna.|  
|PSEUDO_COLUMN|short|Indica se a coluna é uma pseudocoluna. Pode ser um dos seguintes valores:<br /><br /> bestRowUnknown (0)<br /><br /> bestRowNotPseudo (1)<br /><br /> bestRowPseudo (2)|  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar o método getBestRowIdentifier para retornar informações sobre o melhor identificador de linha para a tabela Person.Contact no banco de dados de exemplo do [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
public static void executeGetBestRowIdentifier(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getBestRowIdentifier(null, "Person", "Contact", 0, true);  
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
  
  
