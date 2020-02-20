---
title: Usar a suspensão | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: aa48306c-e7a0-4dcb-af21-9ebb6898e45a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1c126385955ce6e9fa9098ec5a09ba115b94ffb0
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69026205"
---
# <a name="using-holdability"></a>Como usar a suspensão

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Por padrão, um conjunto de resultados criado dentro de uma transação é mantido em aberto depois que a transação é confirmada no banco de dados, ou quando é revertida. Porém, às vezes é útil que o conjunto de resultados seja fechado, depois que a transação foi confirmada. Para fazer isso, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] dá suporte ao uso de colocação em espera de conjuntos de resultados.

A colocação em espera de conjuntos de resultados pode ser configurada usando o método [setHoldability](../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) da classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). Ao definir a colocação em espera usando o método setHoldability, podem ser usadas as constantes de colocação em espera do conjunto de resultados de `ResultSet.HOLD_CURSORS_OVER_COMMIT` ou `ResultSet.CLOSE_CURSORS_AT_COMMIT`.

O driver JDBC também oferece suporte à colocação em espera ao criar um dos objetos de instrução. Ao criar os objetos de Instrução que têm sobrecargas com parâmetros de colocação em espera do conjunto de resultados, o objeto de instrução de colocação em espera deverá corresponder à colocação em espera da conexão. Quando eles não corresponderem, uma exceção será lançada. Isto acontece porque o SQL Server só oferece suporte à colocação em espera no nível de conexão.

A colocação em espera de um conjunto de resultados é a colocação em espera do objeto SQLServerConnection que está associado ao conjunto de resultados apenas no momento em que ele é criado para cursores do lado de servidor. Isso não se aplica a cursores do lado do cliente. Todos os conjuntos de resultados com cursores do lado do cliente sempre terão o valor de suspensão de `ResultSet.HOLD_CURSORS_OVER_COMMIT`.

Nos cursores de servidor, quando conectados ao SQL Server 2005 ou posterior, a definição da suspensão afetará apenas a suspensão dos novos conjuntos de resultados que ainda serão criados nessa conexão. Isto significa que configurar a colocação em espera não tem nenhum impacto na colocação em espera de nenhum conjunto de resultados que foi criado e que já está aberto previamente naquela conexão.

No exemplo a seguir, a colocação em espera de um conjunto de resultados é definida durante a execução de uma transação local que consiste em duas instruções separadas no bloco `try`. As instruções são executadas em relação à tabela Production.ScrapReason no banco de dados de amostra [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Primeiro, o exemplo alterna para o modo de transação manual definindo a confirmação automática como `false`. Quando o modo de confirmação automática é desabilitado, nenhuma instrução SQL será confirmada até que o aplicativo chame o método [commit](../../connect/jdbc/reference/commit-method-sqlserverconnection.md) explicitamente. O código no bloco catch reverterá a transação se uma exceção for lançada.

[!code[JDBC#UsingHoldability1](../../connect/jdbc/codesnippet/Java/using-holdability_1.java)]

## <a name="see-also"></a>Confira também

[Executando transações com o JDBC Driver](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)
