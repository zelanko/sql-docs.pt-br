---
title: Usando uma instrução SQL sem parâmetros | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4b0728bd-059b-4b71-895c-999335bc7427
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 041a0119425e6469a394420469b14f47f3b84a81
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47674834"
---
# <a name="using-an-sql-statement-with-no-parameters"></a>Usando uma instrução SQL sem parâmetros

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para trabalhar usando dados em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com uma instrução SQL sem parâmetros, é possível usar o método [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) a classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) para retornar [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) que conterá os dados solicitados. Para isso, você deve primeiro criar um objeto SQLServerStatement usando o método [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) da classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md).

No exemplo a seguir, uma conexão aberta com o banco de dados de amostra [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] é passada para a função, uma instrução SQL é criada e executada e, em seguida, os resultados são lidos do conjunto de resultados.

[!code[JDBC#UsingSQLWithNoParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_0_1.java)]

Para obter mais informações sobre como usar conjuntos de resultados, consulte [Gerenciando conjuntos de resultados com o Driver JDBC](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md).

## <a name="see-also"></a>Consulte Também

[Usando instruções com SQL](../../connect/jdbc/using-statements-with-sql.md)
