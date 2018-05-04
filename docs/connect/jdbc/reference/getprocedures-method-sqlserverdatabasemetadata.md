---
title: Método getProcedures (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getProcedures
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 66c9a8b0-dc4c-4cbb-8004-c7157368cab4
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1591c028ad1f583234f370a6fd94575b2c04a4c6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
#### <a name="parameters"></a>Parâmetros  
 *sCatalog*  
  
 Um **cadeia de caracteres** que contém o nome do catálogo. Fornecer um nulo a esse parâmetro indica que o nome do catálogo não precisa ser usado.  
  
 *SO*  
  
 Um **cadeia de caracteres** que contém o padrão de nome de esquema. Fornecer um nulo a esse parâmetro indica que o nome de esquema não precisa ser usado.  
  
 *proc*  
  
 Um **cadeia de caracteres** que contém o padrão de nome de procedimento.  
  
## <a name="return-value"></a>Valor de retorno  
 Um [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getProcedures é especificado pelo método getProcedures na interface DatabaseMetadata.  
  
 O conjunto de resultados retornado pelo método getProcedures conterá as seguintes informações:  
  
|Nome|Tipo|Description|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**String**|O nome do banco de dados no qual o procedimento armazenado especificado reside.|  
|PROCEDURE_SCHEM|**String**|O esquema para o procedimento armazenado.|  
|PROCEDURE_NAME|**String**|O nome do procedimento armazenado.|  
|NUM_INPUT_PARAMS|**Int**|Reservado para uso futuro, atualmente retorna um valor -1.|  
|NUM_OUTPUT_PARAMS|**Int**|Reservado para uso futuro, atualmente retorna um valor -1.|  
|NUM_RESULT_SETS|**Int**|Reservado para uso futuro, atualmente retorna um valor -1.|  
|REMARKS|**String**|A descrição da coluna de procedimento.<br /><br /> <br /><br /> **Observação:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] não retorna um valor para essa coluna.  |  
|PROCEDURE_TYPE|**smallint**|O tipo do procedimento armazenado. Pode ser um dos seguintes valores:<br /><br /> SQL_PT_UNKNOWN (0)<br /><br /> SQL_PT_PROCEDURE (1)<br /><br /> SQL_PT_FUNCTION (2)|  
  
> [!NOTE]  
>  Para obter mais informações sobre os dados retornados pelo método getProcedures, consulte "sp_stored_procedures (Transact-SQL)" em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Manuais Online.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar o método getProcedures para retornar informações sobre o procedimento armazenado uspGetBillOfMaterials o [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] banco de dados de exemplo.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
