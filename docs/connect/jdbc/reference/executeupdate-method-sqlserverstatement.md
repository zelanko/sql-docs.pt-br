---
title: Método executeUpdate (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeUpdate
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 10ae662a-ce3c-4b24-875c-5c2df319d93b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9052e28e66e6767a64b392978c6c52a42c24eaec
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66804129"
---
# <a name="executeupdate-method-sqlserverstatement"></a>Método executeUpdate (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Executa a instrução SQL fornecida, que pode ser INSERT, UPDATE ou DELETE; ou uma instrução SQL que não retorne nada, como uma instrução SQL DDL. Por meio do [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0, executeUpdate retornará o número correto de linhas atualizadas em uma operação MERGE.  
  
## <a name="overload-list"></a>Lista de sobrecargas  
  
|Nome|Descrição|  
|----------|-----------------|  
|[executeUpdate (java.lang.String)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-sqlserverstatement.md)|Executa a instrução SQL fornecida, que pode ser INSERT, UPDATE, DELETE ou MERGE ou uma instrução SQL que não retorne nada, como uma instrução SQL DDL.|  
|[executeUpdate (java.lang.String, int)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-int.md)|Executa a instrução SQL fornecida e sinaliza o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] com o sinalizador fornecido que indica se as chaves geradas automaticamente, produzidas pelo objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) em questão, devem ser disponibilizadas para recuperação.|  
|[executeUpdate (java.lang.String, int&#91;&#93;)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string.md)|Executa a instrução SQL fornecida e sinaliza ao driver JDBC que as chave geradas automaticamente indicadas na matriz fornecida devem ser disponibilizadas para recuperação.|  
|[executeUpdate (java.lang.String, java.lang.String&#91;&#93;)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-java-lang-string.md)|Executa a instrução SQL fornecida e sinaliza ao driver JDBC que as chave geradas automaticamente indicadas na matriz fornecida devem ser disponibilizadas para recuperação.|  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
