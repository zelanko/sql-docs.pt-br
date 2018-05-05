---
title: Método getFunctions (SQLServerDatabaseMetaData) | Microsoft Docs
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
ms.assetid: 44335cbd-c84d-4ef3-a6a1-fca7eb7ec768
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2bb2e1bdf12ea8b1c067d53b4d6e7ce35f3ca4b9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
 *catalog*  
  
 O nome de um catálogo no banco de dados. Se for uma cadeia de caracteres vazia "", o resultado incluirá as funções sem um catálogo. Se for **nulo**, o nome do catálogo não é usado para pesquisa.  
  
 *schemaPattern*  
  
 O nome de um esquema. Se for uma cadeia de caracteres vazia "", o resultado incluirá as funções sem um esquema. Se for **nulo**, o nome do esquema não é usado para pesquisa.  
  
 *functionNamePattern*  
  
 O nome de uma função.  
  
## <a name="return-value"></a>Valor de retorno  
 Um [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getFunctions é especificado pelo método getFunctions na interface DatabaseMetadata.  
  
 Esse método retorna apenas as funções de sistema e de usuário que correspondem ao nome de esquema e de função especificados.  
  
> [!IMPORTANT]  
>  O conjunto de resultados retornado pode conter funções que o usuário de chamada não tem permissões para executar.  
  
 Cada descrição de função inclui as seguintes colunas:  
  
|Nome|Tipo|Description|  
|----------|----------|-----------------|  
|FUNCTION_CAT|**String**|O nome do banco de dados no qual a função reside.|  
|FUNCTION_SCHEM|**String**|O nome do esquema no qual a função reside.|  
|FUNCTION_NAME|**String**|O nome da função.|  
|NUM_INPUT_PARAMS|**Int**|Reservado para uso futuro, atualmente retorna um valor -1.|  
|NUM_OUTPUT_PARAMS|**Int**|Reservado para uso futuro, atualmente retorna um valor -1.|  
|NUM_RESULT_SETS|**Int**|Reservado para uso futuro, atualmente retorna um valor -1.|  
|REMARKS|**String**|Os comentários sobre a função.|  
|FUNCTION_TYPE|**short**|O tipo da função. Pode ser um dos seguintes valores:<br /><br /> SQL_PT_UNKNOWN (0)<br /><br /> SQL_PT_PROCEDURE (1)<br /><br /> SQL_PT_FUNCTION (2)|  
  
 Todas as descrições no conjunto de resultados retornado são ordenadas por FUNCTION_CAT, FUNCTION_SCHEM, FUNCTION_NAME e SPECIFIC_NAME.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
