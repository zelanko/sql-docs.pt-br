---
title: Método getFunctions (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 44335cbd-c84d-4ef3-a6a1-fca7eb7ec768
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cafef140d505197bfe1993f65ef17d4cb53e19f5
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920327"
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
  
#### <a name="parameters"></a>parâmetros  
 *catalog*  
  
 O nome de um catálogo no banco de dados. Se for uma cadeia de caracteres vazia "", o resultado incluirá as funções sem um catálogo. Se for **null**, o nome do catálogo não será usado para pesquisa.  
  
 *schemaPattern*  
  
 O nome de um esquema. Se for uma cadeia de caracteres vazia "", o resultado incluirá as funções sem um esquema. Se for **null**, o nome do esquema não será usado para pesquisa.  
  
 *functionNamePattern*  
  
 O nome de uma função.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getFunctions é especificado pelo método getFunctions na interface java.sql.DatabaseMetaData.  
  
 Esse método retorna apenas as funções de sistema e de usuário que correspondem ao nome de esquema e de função especificados.  
  
> [!IMPORTANT]  
>  O conjunto de resultados retornado pode conter funções que o usuário de chamada não tem permissões para executar.  
  
 Cada descrição de função inclui as seguintes colunas:  
  
|Nome|Type|DESCRIÇÃO|  
|----------|----------|-----------------|  
|FUNCTION_CAT|**Cadeia de caracteres**|O nome do banco de dados no qual a função reside.|  
|FUNCTION_SCHEM|**Cadeia de caracteres**|O nome do esquema no qual a função reside.|  
|FUNCTION_NAME|**Cadeia de caracteres**|O nome da função.|  
|NUM_INPUT_PARAMS|**int**|Reservado para uso futuro, atualmente retorna um valor -1.|  
|NUM_OUTPUT_PARAMS|**int**|Reservado para uso futuro, atualmente retorna um valor -1.|  
|NUM_RESULT_SETS|**int**|Reservado para uso futuro, atualmente retorna um valor -1.|  
|COMENTÁRIOS|**Cadeia de caracteres**|Os comentários sobre a função.|  
|FUNCTION_TYPE|**short**|O tipo da função. Pode ser um dos seguintes valores:<br /><br /> SQL_PT_UNKNOWN (0)<br /><br /> SQL_PT_PROCEDURE (1)<br /><br /> SQL_PT_FUNCTION (2)|  
  
 Todas as descrições no conjunto de resultados retornado são ordenadas por FUNCTION_CAT, FUNCTION_SCHEM, FUNCTION_NAME e SPECIFIC_NAME.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
