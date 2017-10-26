---
title: "Método getFunctions (SQLServerDatabaseMetaData) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 44335cbd-c84d-4ef3-a6a1-fca7eb7ec768
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b0482197b706ac4e604fe6e4402bebbe1bc793fc
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getfunctions-method-sqlserverdatabasemetadata"></a>Método getFunctions (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma descrição das funções de sistema e de usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public ResultSet getFunctions(java.lang.String catalog,  
                       java.lang.String schemaPattern,  
                       java.lang.String functionNamePattern)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Catálogo*  
  
 O nome de um catálogo no banco de dados. Se for uma cadeia de caracteres vazia "", o resultado incluirá as funções sem um catálogo. Se for **nulo**, o nome do catálogo não é usado para pesquisa.  
  
 *schemaPattern*  
  
 O nome de um esquema. Se for uma cadeia de caracteres vazia "", o resultado incluirá as funções sem um esquema. Se for **nulo**, o nome do esquema não é usado para pesquisa.  
  
 *functionNamePattern*  
  
 O nome de uma função.  
  
## <a name="return-value"></a>Valor de retorno  
 Um [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getFunctions é especificado pelo método getFunctions na interface DatabaseMetadata.  
  
 Esse método retorna apenas as funções de sistema e de usuário que correspondem ao nome de esquema e de função especificados.  
  
> [!IMPORTANT]  
>  O conjunto de resultados retornado pode conter funções que o usuário de chamada não tem permissões para executar.  
  
 Cada descrição de função inclui as seguintes colunas:  
  
|Nome|Tipo|Description|  
|----------|----------|-----------------|  
|FUNCTION_CAT|**Cadeia de caracteres**|O nome do banco de dados no qual a função reside.|  
|FUNCTION_SCHEM|**Cadeia de caracteres**|O nome do esquema no qual a função reside.|  
|FUNCTION_NAME|**Cadeia de caracteres**|O nome da função.|  
|NUM_INPUT_PARAMS|**int**|Reservado para uso futuro, atualmente retorna um valor -1.|  
|NUM_OUTPUT_PARAMS|**int**|Reservado para uso futuro, atualmente retorna um valor -1.|  
|NUM_RESULT_SETS|**int**|Reservado para uso futuro, atualmente retorna um valor -1.|  
|REMARKS|**Cadeia de caracteres**|Os comentários sobre a função.|  
|FUNCTION_TYPE|**curto**|O tipo da função. Pode ser um dos seguintes valores:<br /><br /> SQL_PT_UNKNOWN (0)<br /><br /> SQL_PT_PROCEDURE (1)<br /><br /> SQL_PT_FUNCTION (2)|  
  
 Todas as descrições no conjunto de resultados retornado são ordenadas por FUNCTION_CAT, FUNCTION_SCHEM, FUNCTION_NAME e SPECIFIC_NAME.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

