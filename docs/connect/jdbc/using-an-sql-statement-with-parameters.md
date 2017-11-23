---
title: "Usando uma instrução SQL com parâmetros | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3202b88f-ce13-44dd-982c-c6a3b0260378
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8475ea4917ffcc0d9226933b29e81b99f89345c2
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="using-an-sql-statement-with-parameters"></a>Usando uma instrução SQL com parâmetros
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para trabalhar com dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados usando uma instrução SQL contendo parâmetros IN, você pode usar o [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) método o [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) classe para retornar um [ SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) que conterá os dados solicitados. Para fazer isso, você deve primeiro criar um objeto SQLServerPreparedStatement usando o [prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md) método o [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) classe.  
  
 Quando você constrói a instrução SQL, os parâmetros IN são especificados usando-se o caractere ? (ponto de interrogação), que funciona como um espaço reservado para os valores de parâmetro que, posteriormente, serão passados para a instrução SQL. Para especificar um valor para um parâmetro, você pode usar um dos métodos setter da classe SQLServerPreparedStatement. O método setter que é possível pode usar é determinado pelo tipo de valor que você deseja passar para a instrução SQL.  
  
 Ao passar um valor para o método setter, você deve especificar não somente o valor real a ser usado na instrução SQL, mas também o posicionamento ordinal do parâmetro na instrução SQL. Por exemplo, se a instrução SQL contiver um único parâmetro, seu valor ordinal será 1. Se a instrução contiver dois parâmetros, o primeiro valor ordinal será 1, e o segundo valor ordinal será 2.  
  
 No exemplo a seguir, uma conexão aberta para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passado para a função, uma instrução SQL preparada é criada e executada com um único valor de parâmetro de cadeia de caracteres e, em seguida, os resultados são lidos do conjunto de resultados.  
  
 [!code[JDBC#UsingSQLWithParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_1_1.java)]  
  
## <a name="see-also"></a>Consulte também  
 [Usando instruções com SQL](../../connect/jdbc/using-statements-with-sql.md)  
  
  

