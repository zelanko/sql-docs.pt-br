---
title: "Usando colocação em espera | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: aa48306c-e7a0-4dcb-af21-9ebb6898e45a
caps.latest.revision: "25"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c59212d8e0ebdf6eb57ecdc737582d73998124a5
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="using-holdability"></a>Usando colocação em espera
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Por padrão, um conjunto de resultados criado dentro de uma transação é mantido em aberto depois que a transação é confirmada no banco de dados, ou quando é revertida. Porém, às vezes é útil que o conjunto de resultados seja fechado, depois que a transação foi confirmada. Para fazer isso, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] suporta o uso de resultado de suspensão do conjunto.  
  
 Suspensão do conjunto de resultados pode ser definida usando o [setHoldability](../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) método o [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) classe. Ao definir a colocação em espera usando o método setHoldability, o conjunto de resultados constantes de colocação em espera de Hold_cursors_over_commit ou ResultSet.CLOSE_CURSORS_AT_COMMIT pode ser usado.  
  
 O driver JDBC também oferece suporte à colocação em espera ao criar um dos objetos de instrução. Ao criar os objetos de Instrução que têm sobrecargas com parâmetros de colocação em espera do conjunto de resultados, o objeto de instrução de colocação em espera deverá corresponder à colocação em espera da conexão. Quando eles não corresponderem, uma exceção será lançada. Isto acontece porque o SQL Server só oferece suporte à colocação em espera no nível de conexão.  
  
 A suspensão de um conjunto de resultados é a colocação em espera do objeto SQLServerConnection que está associado com o resultado definido no momento em que o conjunto de resultados é criado para cursores do lado do servidor apenas. Isso não se aplica a cursores do lado do cliente. Todos os conjuntos de resultados com cursores do lado do cliente sempre terá o valor de suspensão de Hold_cursors_over_commit.  
  
 Nos cursores de servidor, quando conectados ao SQL Server 2005 ou posterior, a definição da suspensão afetará apenas a suspensão dos novos conjuntos de resultados que ainda serão criados nessa conexão. Isto significa que configurar a colocação em espera não tem nenhum impacto na colocação em espera de nenhum conjunto de resultados que foi criado e que já está aberto previamente naquela conexão. Porém, com o SQL Server 2000, a definição da colocação em espera afetará a colocação em espera dos conjuntos de resultados existentes e dos novos conjuntos de resultados que ainda serão criados nessa conexão.  
  
 No exemplo a seguir, a suspensão do conjunto de resultados é definida durante a execução de uma transação local que consiste em duas instruções separadas no `try` bloco. As instruções são executadas em relação à tabela scrapreason no [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo. Primeiro, o exemplo alterna para o modo de transação manual definindo a confirmação automática como **false**. Quando o modo de confirmação automática está desabilitado, nenhuma instrução SQL será confirmada até que o aplicativo chama o [confirmação](../../connect/jdbc/reference/commit-method-sqlserverconnection.md) método explicitamente. O código no bloco catch reverterá a transação se uma exceção for lançada.  
  
 [!code[JDBC#UsingHoldability1](../../connect/jdbc/codesnippet/Java/using-holdability_1.java)]  
  
## <a name="see-also"></a>Consulte também  
 [Executando transações com o JDBC Driver](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
