---
title: "Método getBestRowIdentifier (SQLServerDatabaseMetaData) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getBestRowIdentifier
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c19e9ca6-2a53-4a0c-91ab-80090c3f7229
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 09dee13a9a71b606aa630aac1716d43f6d38a1f2
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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
 *Catálogo*  
  
 Um **cadeia de caracteres** que contém o nome do catálogo.  
  
 *esquema*  
  
 Um **cadeia de caracteres** que contém o nome do esquema.  
  
 *table*  
  
 Um **cadeia de caracteres** que contém o nome da tabela.  
  
 *escopo*  
  
 Um **int** que indica o escopo de interesse. Valores podem incluir o seguinte:  
  
 bestRowTemporary (0)  
  
 bestRowTransaction (1)  
  
 bestRowSession (2)  
  
 *permite valor nulo*  
  
 **True** para incluir colunas anuláveis. Caso contrário, **false**.  
  
## <a name="return-value"></a>Valor de retorno  
 Um [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getBestRowIdentifier é especificado pelo método getBestRowIdentifier na interface DatabaseMetadata.  
  
 O conjunto de resultados retornado pelo método getBestRowIdentifier conterá as seguintes informações:  
  
|Nome|Tipo|Description|  
|----------|----------|-----------------|  
|SCOPE|short|O escopo dos resultados retornados. Pode ser um dos seguintes valores:<br /><br /> bestRowTemporary (0)<br /><br /> bestRowTransaction (1)<br /><br /> bestRowSession (2)|  
|COLUMN_NAME|Cadeia de caracteres|O nome da coluna.|  
|DATA_TYPE|short|O tipo de dados SQL de java.sql.Types.|  
|TYPE_NAME|Cadeia de caracteres|O nome do tipo de dados.|  
|COLUMN_SIZE|int|A precisão da coluna.|  
|BUFFER_LENGTH|int|O comprimento do buffer.|  
|DECIMAL_DIGITS|short|A escala da coluna.|  
|PSEUDO_COLUMN|short|Indica se a coluna é uma pseudocoluna. Pode ser um dos seguintes valores:<br /><br /> bestRowUnknown (0)<br /><br /> bestRowNotPseudo (1)<br /><br /> bestRowPseudo (2)|  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar o método getBestRowIdentifier para retornar informações sobre o melhor identificador de linha para a tabela Person. Contact o [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] banco de dados de exemplo.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
