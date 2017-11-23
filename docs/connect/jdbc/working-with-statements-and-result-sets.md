---
title: "Trabalhando com instruções e conjuntos de resultados | Microsoft Docs"
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
ms.assetid: cc917534-f5f8-4844-87c8-597c48b4e06d
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ce65afcf2086b4b3383f45fd6f0174668eeb1e1a
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="working-with-statements-and-result-sets"></a>Trabalhando com instruções e conjuntos de resultados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Quando você trabalha com o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] e a instrução e objetos de conjunto de resultados que ela fornece, há várias técnicas que você pode usar para melhorar o desempenho e confiabilidade de seus aplicativos.  
  
## <a name="use-the-appropriate-statement-object"></a>Use o objeto de instrução apropriado  
 Quando você usar um dos objetos de instrução JDBC driver, como o [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), ou o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) objeto Certifique-se de que você estiver usando o objeto apropriado para o trabalho.  
  
-   Se você não tiver parâmetros OUT, você não precisa usar o objeto SQLServerCallableStatement. Em vez disso, use o SQLServerStatement ou o objeto SQLServerPreparedStatement.  
  
-   Se você não tiver a intenção de executar a instrução mais de uma vez ou não possuem IN ou os parâmetros de saída, você não precisa usar o objeto SQLServerPreparedStatement ou SQLServerCallableStatement. Em vez disso, use o objeto SQLServerStatement.  
  
## <a name="use-the-appropriate-concurrency-for-resultset-objects"></a>Use a simultaneidade apropriada para objetos ResultSet  
 Não peça simultaneidade atualizável ao criar instruções que geram conjuntos de resultados a menos que você realmente pretenda atualizar os resultados. O modelo de cursor padrão somente avanço, somente leitura é o mais rápido para ler conjuntos de resultados pequenos.  
  
## <a name="limit-the-size-of-your-result-sets"></a>Limitar o tamanho dos seus conjuntos de resultados  
 Considere o uso de [setMaxRows](../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md) método (ou sintaxe SQL SET ROWCOUNT ou SELECT TOP N) para limitar o número de linhas retornado de conjuntos de resultados potencialmente grandes. Se você precisa lidar com conjuntos de resultados grandes, use um buffer de resposta adaptável configurando a propriedade da cadeia de conexão responseBuffering=adaptive, que é o modo padrão. Esta abordagem permite que o aplicativo processe conjuntos de resultados grandes sem exigir cursores do lado do servidor e minimiza o uso de memória de aplicativo. Para obter mais informações, consulte [buffer adaptável usando](../../connect/jdbc/using-adaptive-buffering.md).  
  
## <a name="use-the-appropriate-fetch-size"></a>Use o tamanho da busca apropriado  
 Para cursores de servidor somente leitura, é preciso haver equilíbrio entre as viagens de ida e volta ao servidor e a quantidade de memória usada no driver. Para cursores de servidor atualizáveis, o tamanho da busca influencia também a sensibilidade do conjunto de resultados a alterações e simultaneidade no servidor. As atualizações para linhas no buffer de busca atual não são visíveis até explícito [refreshRow](../../connect/jdbc/reference/refreshrow-method-sqlserverresultset.md) método é emitido ou até que o cursor deixe o buffer de busca. Os buffers de busca grandes terão melhor desempenho (menos viagens de ida e volta ao servidor), mas são menos sensíveis a alterações e reduzirão a simultaneidade no servidor se CONCUR_SS_SCROLL_LOCKS (1009) for usado. Para obter sensibilidade máxima a alterações, use um tamanho da busca de 1. Porém, observe que isto implicará uma viagem de ida e volta ao servidor para cada linha buscada.  
  
## <a name="use-streams-for-large-in-parameters"></a>Usar fluxos para parâmetros IN grandes  
 Use fluxos ou BLOBs e CLOBs que são materializados incrementalmente para gerenciar atualização de valores de coluna grandes ou enviar parâmetros IN grandes. O driver JDBC "corta" essas partes para o servidor em várias viagens de ida e volta, permitindo definir e atualizar valores maiores que o que caberá na memória.  
  
## <a name="see-also"></a>Consulte também  
 [Melhorando o desempenho e a confiabilidade com o JDBC Driver](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
