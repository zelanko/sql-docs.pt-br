---
title: Método getExportedKeys (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getExportedKeys
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 26888e61-b243-4a1b-922c-c0a451dcff4d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f0298e3c933db4887f1270ff60254103a965c7c2
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66767150"
---
# <a name="getexportedkeys-method-sqlserverdatabasemetadata"></a>Método getExportedKeys (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma descrição das colunas de chave estrangeira que referenciam as colunas de chave primária da tabela fornecida.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getExportedKeys(java.lang.String cat,  
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
 Esse método getExportedKeys é especificado pelo método getExportedKeys na interface DatabaseMetadata.  
  
 O conjunto de resultados retornado pelo método getExportedKeys conterá as seguintes informações:  
  
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
>  Para saber mais sobre os dados retornados pelo método getExportedKeys, consulte "sp_fkeys (Transact-SQL)" nos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar o método getExportedKeys para retornar informações sobre todas as chaves estrangeiras que fazem referência às chaves primárias da tabela Person.Contact do banco de dados de exemplo do [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
public static void executeGetExportedKeys(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getExportedKeys("AdventureWorks", "Person", "Contact");  
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
  
  
