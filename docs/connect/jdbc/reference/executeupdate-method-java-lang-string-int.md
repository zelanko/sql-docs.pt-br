---
title: Método executeUpdate (Java, int) | Microsoft Docs
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
- SQLServerStatement.executeUpdate (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c52a20e-527e-4d14-9a5a-4cd195aac8ed
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 680ea0bdf3a12f8d3d32caec3c37a32753188bbc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="executeupdate-method-javalangstring-int"></a>Método executeUpdate (java.lang.String, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Executa a instrução SQL fornecida e sinaliza o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] com o sinalizador fornecido sobre se o gerado automaticamente chaves que são produzidos por este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto deve ser disponibilizado para recuperação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final int executeUpdate(java.lang.String sql,  
                               int flag)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sql*  
  
 Um **cadeia de caracteres** que contém uma instrução SQL.  
  
 *flag*  
  
 Um **int** valor que indica se as chaves geradas automaticamente devem ser disponibilizadas. Deve ser uma das seguintes constantes:  
  
 RETURN_GENERATED_KEYS  
  
 NO_GENERATED_KEYS  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** que indica o número de linhas afetadas ou 0 se usando uma instrução DDL.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método executeUpdate é especificado pelo método executeUpdate na interface Java.SQL. Statement.  
  
 Se executar um procedimento armazenado resulta em uma contagem de atualização que é maior do que um, ou que gera mais de um conjunto de resultados, use o [executar](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) método para executar o procedimento armazenado.  
  
## <a name="see-also"></a>Consulte também  
 [Método executeUpdate &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
