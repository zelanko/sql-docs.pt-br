---
title: Método executeUpdate (java.lang.String) (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeUpdate (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 85e7c3a2-f2da-49bf-9d90-5fd246fd60e1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6432cd0d09dac50857a0bd1da16a3ded92bb09c5
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924260"
---
# <a name="executeupdate-method-javalangstring-sqlserverstatement"></a>Método executeUpdate (java.lang.String) (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Executa a instrução SQL fornecida, que pode ser INSERT, UPDATE ou DELETE; ou uma instrução SQL que não retorne nada, como uma instrução SQL DDL. Por meio do [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0, executeUpdate retornará o número correto de linhas atualizadas em uma operação MERGE.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int executeUpdate(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *sql*  
  
 Uma **String** que contém a instrução SQL.  
  
## <a name="return-value"></a>Valor retornado  
 Um **int** que indica o número de linhas afetadas ou 0 se uma instrução DDL estiver sendo usada.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método executeUpdate é especificado pelo método executeUpdate na interface java.sql.Statement.  
  
 Se a execução de um procedimento armazenado resultar em uma contagem de atualização maior que um, ou que gere mais de um conjunto de resultados, use o método [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) para executar o procedimento armazenado.  
  
## <a name="see-also"></a>Consulte Também  
 [Método executeUpdate &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
