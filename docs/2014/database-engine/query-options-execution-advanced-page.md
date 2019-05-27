---
title: Opções de consulta de execução (página avançada) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.advanced.f1
ms.assetid: 661595ce-99b9-4316-ad80-ed04002d04d5
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: f08758af9c75e36dbf8c8d4d62ae17352972b79d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66089091"
---
# <a name="query-options-execution-advanced-page"></a>Execução de opções de consulta (Página Avançado)
  Estão disponíveis diversas opções usando a instrução **SET** . Use essa página para especificar uma opção **set** para executar consultas no Microsoft SQL Server. Para obter informações detalhadas sobre cada uma dessas opções, consulte os manuais online do SQL Server.  
  
 **SET NOCOUNT**  
 Não retorna a contagem do número de linhas, como uma mensagem com o conjunto de resultados. Essa opção é desmarcada por padrão.  
  
 **SET NOEXEC**  
 Não executa a consulta. Essa opção é desmarcada por padrão.  
  
 **SET PARSEONLY**  
 Verifica a sintaxe de cada consulta mas não executa as consultas. Essa opção é desmarcada por padrão.  
  
 **SET CONCAT_NULL_YIELDS_NULL**  
 Quando essa caixa de seleção está selecionada, as consultas que concatenam um valor existente com `NULL`sempre retornam `NULL` como resultado. Quando essa caixa de seleção é desmarcada, um valor existente concatenado com um `NULL`retorna o valor existente. Esta opção é selecionada por padrão.  
  
 **SET ARITHABORT**  
 Quando essa caixa de seleção é marcada, quando uma instrução `INSERT`, `DELETE` ou `UPDATE` encontra um erro aritmético (estouro, divisão por zero ou um erro de domínio) durante a avaliação da expressão, a consulta ou lote é encerrado. Quando essa caixa de seleção estiver desmarcada, se possível, será fornecido `NULL` para esse valor, a consulta continua e é incluída uma mensagem com o resultado. Consulte os manuais online para uma descrição mais ampla sobre esse comportamento. Esta opção é selecionada por padrão.  
  
 **SET SHOWPLAN_TEXT**  
 Quando essa caixa de seleção é marcada, o plano de consulta é retornado em formato de texto com cada consulta. Essa opção é desmarcada por padrão.  
  
 **SET STATISTICS TIME**  
 Quando essa caixa de seleção é marcada, as estatísticas de tempo são retornadas com cada consulta. Essa opção é desmarcada por padrão.  
  
 **SET STATISTICS IO**  
 Quando essa caixa de seleção é marcada, são retornadas estatísticas relacionadas a entrada/saída (E/S) com cada consulta. Essa opção é desmarcada por padrão.  
  
 **SET TRANSACTION ISOLATION LEVEL**  
 O nível de isolamento da transação READ COMMITTED é definido por padrão. Para obter mais informações, veja [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql). Nível de isolamento da transação SNAPSHOT não está disponível. Para usar isolamento SNAPSHOT, adicione a seguinte instrução [!INCLUDE[tsql](../includes/tsql-md.md)] :  
  
```  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
GO  
```  
  
 **DEFINIR A PRIORIDADE DE DEADLOCK**  
 O valor padrão **Normal** permite que cada consulta tenha a mesma prioridade quando ocorrer um deadlock. Selecione a prioridade como Baixa da lista suspensa, se você deseja que essa consulta libere qualquer conflito de deadlock e seja selecionado o encerramento da consulta.  
  
 **DEFINIR TEMPO LIMITE DE BLOQUEIO**  
 O valor padrão -1 indica que os bloqueios sejam mantidos até que as transações sejam completadas. Um valor 0 significa não esperar e retornar uma mensagem assim que for encontrado um bloqueio. Forneça um valor maior que 0 milissegundo para encerrar a transação se os bloqueios para a transação devem ser mantidos por um tempo maior que esse.  
  
 **SET QUERY_GOVERNOR_COST_LIMIT**  
 Use a opção **query governor cost limit** para especificar um limite máximo no intervalo de tempo durante o qual poderá ser executada uma consulta. O custo da consulta refere-se ao tempo decorrido estimado, em segundos, necessário para concluir uma consulta em uma configuração de hardware específica. A configuração padrão de 0 indica que não existe limite para o intervalo de tempo que uma consulta executará  
  
 **Suprimir cabeçalhos de mensagem do provedor**  
 Quando esta caixa de seleção é marcada, não são exibidas mensagens de status do provedor (como o provedor OLE DB). Esta caixa de seleção fica marcada por padrão. Desmarque essa caixa de seleção para ver as mensagens do provedor ao solucionar problemas com consultas que podem estar falhando no nível do provedor.  
  
 **Desconectar depois que a consulta é executada**  
 Quando essa caixa de seleção é marcada, a conexão com SQL Server é encerrada depois que a consulta é completada. Essa opção é desmarcada por padrão.  
  
 **Restaurar Padrões**  
 Redefine todos os valores dessa página com os valores padrão originais.  
  
  
