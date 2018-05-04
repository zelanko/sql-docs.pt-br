---
title: Usando vários conjuntos de resultados | Microsoft Docs
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
ms.assetid: ab6a3cfa-073b-44e9-afca-a8675cfe5fd1
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba12e749d6fe8131b0e2a1183f20a9d9101d7e53
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="using-multiple-result-sets"></a>Usando vários conjuntos de resultados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Ao trabalhar com SQL embutido ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] procedimentos armazenados que retornam mais de um conjunto de resultados, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece o [getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) método o [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) de classe para recuperar cada conjunto de dados retornado. Além disso, quando executar uma instrução que retorna mais de um conjunto de resultados, você pode usar o [executar](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) método de SQLServerStatement classe, porque retornará um **booliano** valor que indica se a valor retornado é um conjunto de resultados ou uma contagem de atualização.  
  
 Se o método execute retorna **true**, a instrução que foi executada retornou um ou mais conjuntos de resultados. Você pode acessar o primeiro resultado definido ao chamar o método getResultSet. Para determinar se mais conjuntos de resultados estiverem disponíveis, você pode chamar o [getMoreResults](../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md) método, que retorna um **booliano** valor **true** se houver mais conjuntos de resultados. Se houver mais conjuntos de resultados, você pode chamar o método getResultSet novamente para acessá-los, continuando o processo até que todos os conjuntos de resultados tenham sido processados. Se o método getMoreResults retorna **false**, não há nenhum mais conjuntos de resultados para o processo.  
  
 Se o método execute retorna **false**, a instrução que foi executada retornou um valor de contagem de atualização que você pode recuperar chamando o [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) método.  
  
> [!NOTE]  
>  Para obter mais informações sobre contagens de atualização, consulte [usando um procedimento armazenado com uma contagem de atualização](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md).  
  
 No exemplo a seguir, uma conexão aberta para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passado para a função e uma instrução SQL é construída que, quando executado, retorna dois conjuntos de resultados:  
  
 [!code[JDBC#UsingMultipleResultSets1](../../connect/jdbc/codesnippet/Java/using-multiple-result-sets_1.java)]  
  
 Neste caso, o número de conjuntos de resultados retornado é conhecido para ser dois. Porém, o código é escrito de forma que, se um número desconhecido de conjuntos de resultados fosse retornado, como ao chamar um procedimento armazenado, todos eles seriam processados. Para ver um exemplo de como chamar um procedimento armazenado que retorna vários conjuntos de resultados junto com os valores de atualização, consulte [tratar instruções complexas](../../connect/jdbc/handling-complex-statements.md).  
  
> [!NOTE]  
>  Quando você fizer a chamada ao método getMoreResults da classe SQLServerStatement, o conjunto de resultados previamente retornado será fechado implicitamente.  
  
## <a name="see-also"></a>Consulte também  
 [Usando instruções com o JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
