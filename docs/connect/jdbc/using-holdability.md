---
title: Usando colocação em espera | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: aa48306c-e7a0-4dcb-af21-9ebb6898e45a
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0bf10226926d3c5df21d546de042095defbbe812
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37982088"
---
# <a name="using-holdability"></a>Usando colocação em espera
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Por padrão, um conjunto de resultados criado dentro de uma transação é mantido em aberto depois que a transação é confirmada no banco de dados, ou quando é revertida. Porém, às vezes é útil que o conjunto de resultados seja fechado, depois que a transação foi confirmada. Para fazer isso, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] dá suporte ao uso de colocação em espera de conjuntos de resultados.  
  
 A colocação em espera de conjuntos de resultados pode ser configurada usando o método [setHoldability](../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) da classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). Ao definir a colocação em espera usando o método setHoldability, o conjunto de resultados constantes de colocação em espera de Hold_cursors_over_commit ou ResultSet.CLOSE_CURSORS_AT_COMMIT pode ser usado.  
  
 O driver JDBC também oferece suporte à colocação em espera ao criar um dos objetos de instrução. Ao criar os objetos de Instrução que têm sobrecargas com parâmetros de colocação em espera do conjunto de resultados, o objeto de instrução de colocação em espera deverá corresponder à colocação em espera da conexão. Quando eles não corresponderem, uma exceção será lançada. Isto acontece porque o SQL Server só oferece suporte à colocação em espera no nível de conexão.  
  
 A colocação em espera de um conjunto de resultados é a colocação em espera do objeto SQLServerConnection que está associado ao conjunto de resultados apenas no momento em que ele é criado para cursores do lado de servidor. Isso não se aplica a cursores do lado do cliente. Todos os conjuntos de resultados com cursores do lado do cliente sempre terá o valor de suspensão de Hold_cursors_over_commit.  
  
 Nos cursores de servidor, quando conectados ao SQL Server 2005 ou posterior, a definição da suspensão afetará apenas a suspensão dos novos conjuntos de resultados que ainda serão criados nessa conexão. Isto significa que configurar a colocação em espera não tem nenhum impacto na colocação em espera de nenhum conjunto de resultados que foi criado e que já está aberto previamente naquela conexão. Porém, com o SQL Server 2000, a definição da colocação em espera afetará a colocação em espera dos conjuntos de resultados existentes e dos novos conjuntos de resultados que ainda serão criados nessa conexão.  
  
 No exemplo a seguir, a colocação em espera de um conjunto de resultados é definida durante a execução de uma transação local que consiste em duas instruções separadas no bloco `try`. As instruções são executadas em relação à tabela Production.ScrapReason no banco de dados de amostra [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Primeiro, o exemplo alterna para o modo de transação manual definindo a confirmação automática como **false**. Quando o modo de confirmação automática é desabilitado, nenhuma instrução SQL será confirmada até que o aplicativo chame o método [commit](../../connect/jdbc/reference/commit-method-sqlserverconnection.md) explicitamente. O código no bloco catch reverterá a transação se uma exceção for lançada.  
  
 [!code[JDBC#UsingHoldability1](../../connect/jdbc/codesnippet/Java/using-holdability_1.java)]  
  
## <a name="see-also"></a>Consulte Também  
 [Executando transações com o JDBC Driver](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
