---
title: Usando vários conjuntos de resultados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ab6a3cfa-073b-44e9-afca-a8675cfe5fd1
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 08f1f202ded4c9e0053cfc6c315b87c6f4616eee
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42786768"
---
# <a name="using-multiple-result-sets"></a>Usando vários conjuntos de resultados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Ao trabalhar com o SQL embutido ou procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que retornam mais de um conjunto de resultados, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece o método [getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) na classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) para recuperar cada conjunto de dados retornado. Além disso, ao executar uma instrução que retorna mais de um conjunto de resultados, você pode usar o método [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) da classe SQLServerStatement, pois ele retornará um valor **booliano** que indica se o valor retornado é um conjunto de resultados ou uma contagem de atualização.

Se o método execute retorna **true**, isso significa que a instrução executada retornou um ou mais conjuntos de resultados. Você pode acessar o primeiro conjunto de resultados chamando o método getResultSet. Para determinar se mais conjuntos de resultados estão disponíveis, você pode chamar o método [getMoreResults](../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md), que retornará um valor **booliano** de **true** se mais conjuntos de resultados estiverem disponíveis. Se mais conjuntos de resultados estiverem disponíveis, você poderá chamar o método getResultSet novamente para acessá-los, continuando o processo até que todos os conjuntos de resultados tenham sido processados. Se o método getMoreResults retornar **falsos**, há nenhum mais conjuntos de resultados ao processo.

Se o método execute retorna **false**, a instrução executada retornou um valor de contagem de atualização que você pode recuperar chamando o método [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md).

> [!NOTE]  
> Para obter mais informações sobre contagens de atualização, consulte [usando um procedimento armazenado com uma contagem de atualização](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md).

No exemplo a seguir, uma conexão aberta para o banco de dados de amostra [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] é passada para a função e uma instrução SQL é construída que, quando executada, retorna dois conjuntos de resultados:

[!code[JDBC#UsingMultipleResultSets1](../../connect/jdbc/codesnippet/Java/using-multiple-result-sets_1.java)]

Neste caso, o número de conjuntos de resultados retornado é conhecido para ser dois. Porém, o código é escrito de forma que, se um número desconhecido de conjuntos de resultados fosse retornado, como ao chamar um procedimento armazenado, todos eles seriam processados. Para ver um exemplo de chamada de procedimento armazenado que retorna vários conjuntos de resultados junto com valores de atualização, consulte [Como tratar instruções complexas](../../connect/jdbc/handling-complex-statements.md).

> [!NOTE]  
> Quando você faz a chamada para o método getMoreResults da classe SQLServerStatement, o conjunto de resultados previamente retornado será fechado implicitamente.

## <a name="see-also"></a>Consulte Também

[Usando instruções com o JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)
