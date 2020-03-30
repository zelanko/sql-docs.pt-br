---
title: Método getProcedures (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getProcedures
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 66c9a8b0-dc4c-4cbb-8004-c7157368cab4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 054ce4f6f646f873d4aff05fbe1d31aa9903ded9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67980743"
---
# <a name="getprocedures-method-sqlserverdatabasemetadata"></a>Método getProcedures (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma descrição dos procedimentos armazenados disponíveis no catálogo, esquema ou padrão de nome de procedimento armazenado fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getProcedures(java.lang.String sCatalog,  
                                        java.lang.String sSchema,  
                                        java.lang.String proc)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *sCatalog*  
  
 Uma **String** que contém o nome do catálogo. Fornecer um nulo a esse parâmetro indica que o nome do catálogo não precisa ser usado.  
  
 *sSchema*  
  
 Uma **String** que contém o padrão de nome do esquema. Fornecer um nulo a esse parâmetro indica que o nome de esquema não precisa ser usado.  
  
 *proc*  
  
 Uma **String** que contém o padrão de nome do procedimento.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 O método getProcedures é especificado pelo método getProcedures na interface java.sql.DatabaseMetaData.  
  
 O conjunto de resultados retornado pelo método getProcedures conterá as seguintes informações:  
  
|Nome|Type|DESCRIÇÃO|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**Cadeia de caracteres**|O nome do banco de dados no qual o procedimento armazenado especificado reside.|  
|PROCEDURE_SCHEM|**Cadeia de caracteres**|O esquema para o procedimento armazenado.|  
|PROCEDURE_NAME|**Cadeia de caracteres**|O nome do procedimento armazenado.|  
|NUM_INPUT_PARAMS|**int**|Reservado para uso futuro, atualmente retorna um valor -1.|  
|NUM_OUTPUT_PARAMS|**int**|Reservado para uso futuro, atualmente retorna um valor -1.|  
|NUM_RESULT_SETS|**int**|Reservado para uso futuro, atualmente retorna um valor -1.|  
|COMENTÁRIOS|**Cadeia de caracteres**|A descrição da coluna de procedimento.<br /><br /> <br /><br /> **Observação:** o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não retorna um valor para essa coluna.|  
|PROCEDURE_TYPE|**smallint**|O tipo do procedimento armazenado. Pode ser um dos seguintes valores:<br /><br /> SQL_PT_UNKNOWN (0)<br /><br /> SQL_PT_PROCEDURE (1)<br /><br /> SQL_PT_FUNCTION (2)|  
  
> [!NOTE]  
>  Para saber mais sobre os dados retornados pelo método getProcedures, consulte "sp_stored_procedures (Transact-SQL)" nos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar o método getProcedures para retornar informações sobre o procedimento armazenado uspGetBillOfMaterials no banco de dados de exemplo do [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
public static void executeGetProcedures(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getProcedures(null, null, "uspGetBillOfMaterials");  
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
  
  
