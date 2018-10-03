---
title: Método getImportedKeys (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getImportedKeys
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dc8c1a5e-700e-4059-a5ed-5013bbb87fb6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cbb50cd617ba1ce85851c08764f3f80cd90cbe67
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47611624"
---
# <a name="getimportedkeys-method-sqlserverdatabasemetadata"></a>Método getImportedKeys (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma descrição das colunas de chave primária referenciadas pelas colunas de chave estrangeira em uma tabela.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getImportedKeys(java.lang.String cat,  
                                          java.lang.String schema,  
                                          java.lang.String table)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *cat*  
  
 Uma **String** que contém o nome do catálogo.  
  
 *schema*  
  
 Uma **String** que contém o nome do esquema.  
  
 *table*  
  
 Uma **String** que contém o nome da tabela.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getImportedKeys é especificado pelo método getImportedKeys na interface DatabaseMetadata.  
  
 O conjunto de resultados retornado pelo método getImportedKeys conterá as seguintes informações:  
  
|Nome|Tipo|Descrição|  
|----------|----------|-----------------|  
|PKTABLE_CAT|**String**|O nome do catálogo que contém a tabela de chaves primárias.|  
|PKTABLE_SCHEM|**String**|O nome do esquema da tabela de chaves primárias.|  
|PKTABLE_NAME|**String**|O nome da tabela de chaves primárias.|  
|PKCOLUMN_NAME|**String**|O nome da coluna da chave primária.|  
|FKTABLE_CAT|**String**|O nome do catálogo que contém a tabela de chaves estrangeiras.|  
|FKTABLE_SCHEM|**String**|O nome do esquema da tabela de chaves estrangeiras.|  
|FKTABLE_NAME|**String**|O nome da tabela de chaves estrangeiras.|  
|FKCOLUMN_NAME|**String**|O nome da coluna da chave estrangeira.|  
|KEY_SEQ|**short**|O número de sequência da coluna em uma chave primária de várias colunas.|  
|UPDATE_RULE|**short**|A ação aplicada à chave estrangeira quando a operação SQL for uma atualização. Pode ser um dos seguintes valores:<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|DELETE_RULE|**short**|A ação aplicada à chave estrangeira quando a operação SQL for uma exclusão. Pode ser um dos seguintes valores:<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|FK_NAME|**String**|O nome da chave estrangeira.|  
|PK_NAME|**String**|O nome da chave primária.|  
|DEFERRABILITY|**short**|Indica se a avaliação da restrição de chave estrangeira poderá ser adiada até uma confirmação. Pode ser um dos seguintes valores:<br /><br /> importedKeyInitiallyDeferred (5)<br /><br /> importedKeyInitiallyImmediate (6)<br /><br /> importedKeyNotDeferrable (7)|  
  
> [!NOTE]  
>  Para saber mais sobre os dados retornados pelo método getImportedKeys, veja "sp_fkeys (Transact-SQL)" nos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar o método getImportedKeys para retornar informações sobre todas as chaves primárias que fazem referência às chaves estrangeiras da tabela Person.Contact do banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
public static void executeGetImportedKeys(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getImportedKeys("AdventureWorks", "Person", "Address");  
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
  
  
