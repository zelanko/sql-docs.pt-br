---
title: Execução de opções de consulta (página avançado) | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.advanced.f1
ms.assetid: 661595ce-99b9-4316-ad80-ed04002d04d5
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: ''
ms.custom: ''
ms.date: 09/03/2019
ms.openlocfilehash: 39a43adeb82b154a076fc7bfc24cc56b54cc8640
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "71199329"
---
# <a name="query-options-execution-advanced-page"></a>Execução de opções de consulta (Página Avançado)

  Estão disponíveis diversas opções usando a instrução **SET** . Use esta página para especificar uma opção **set** para executar Microsoft SQL Server consultas. Para obter informações detalhadas sobre cada uma dessas opções, consulte os manuais online do SQL Server.
  
**definir NOcount** Não retorna a contagem do número de linhas, como uma mensagem com o conjunto de resultados. Essa opção é desmarcada por padrão.

**definir NOexec** Não executa a consulta. Essa opção é desmarcada por padrão.

**definir PARSEONLY** Verifica a sintaxe de cada consulta, mas não executa as consultas. Essa opção é desmarcada por padrão.  

**definir CONCAT_NULL_YIELDS_NULL** Quando essa caixa de seleção é marcada, as consultas que concatenam um valor existente `NULL`com um, sempre `NULL` retornam um como resultado. Quando essa caixa de seleção é desmarcada, um valor existente concatenado com um `NULL`retorna o valor existente. Esta opção é selecionada por padrão.

**definir ARITHABORT** Quando essa caixa de seleção está marcada, quando `INSERT`uma `DELETE` instrução `UPDATE` , ou encontra um erro aritmético (estouro, divisão por zero ou um erro de domínio) durante a avaliação da expressão, a consulta ou o lote é encerrado. Quando essa caixa de seleção estiver desmarcada, se possível, será fornecido `NULL` para esse valor, a consulta continua e é incluída uma mensagem com o resultado. Consulte os manuais online para uma descrição mais ampla sobre esse comportamento. Esta opção é selecionada por padrão.
  
**definir SHOWPLAN_TEXT** Quando essa caixa de seleção é marcada, o plano de consulta é retornado no formulário de texto com cada consulta. Essa opção é desmarcada por padrão.
  
**SET STATISTICS TIME** Quando essa caixa de seleção é marcada, as estatísticas de tempo são retornadas com cada consulta. Essa opção é desmarcada por padrão.
  
**definir estatísticas de e/s** Quando essa caixa de seleção é marcada, as estatísticas sobre entrada/saída (e/s) são retornadas com cada consulta. Essa opção é desmarcada por padrão.
  
**SET TRANSACTION ISOLATION LEVEL** O nível de isolamento da transação READ COMMITTED é definido por padrão. Para obter mais informações, veja [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql). O nível de isolamento da transação de instantâneo não está disponível. Para usar isolamento SNAPSHOT, adicione a seguinte instrução [!INCLUDE[tsql](../includes/tsql-md.md)] :
  
  ```sql
  SET TRANSACTION ISOLATION LEVEL SNAPSHOT;
  GO
  ```

**SET DEADLOCK PRIORITY** O valor padrão **Normal** permite que cada consulta tenha a mesma prioridade quando ocorrer um deadlock. Selecione a prioridade como Baixa da lista suspensa, se você deseja que essa consulta libere qualquer conflito de deadlock e seja selecionado o encerramento da consulta.

**definir tempo limite de bloqueio** O valor padrão de-1 indica que os bloqueios são mantidos até que as transações sejam concluídas. Um valor 0 significa não esperar e retornar uma mensagem assim que for encontrado um bloqueio. Forneça um valor maior que 0 milissegundo para encerrar a transação se os bloqueios para a transação devem ser mantidos por um tempo maior que esse.

**definir QUERY_GOVERNOR_COST_LIMIT** Use a opção de **limite de custo do administrador de consultas** para especificar um limite superior no período de tempo no qual uma consulta pode ser executada. O custo da consulta refere-se ao tempo decorrido estimado, em segundos, necessário para concluir uma consulta em uma configuração de hardware específica. A configuração padrão de 0 indica que não existe limite para o intervalo de tempo que uma consulta executará

**Suprimir cabeçalhos de mensagens do provedor** Quando essa caixa de seleção está marcada, as mensagens de status do provedor (como o provedor de OLE DB) não são exibidas. Esta caixa de seleção fica marcada por padrão. Desmarque essa caixa de seleção para ver as mensagens do provedor ao solucionar problemas com consultas que podem estar falhando no nível do provedor.

**Desconectar depois que a consulta for executada** Quando essa caixa de seleção é marcada, a conexão com SQL Server é encerrada depois que a consulta é completada. Essa opção é desmarcada por padrão.

**Mostrar hora de conclusão** Permite imprimir a hora em que a execução da consulta foi concluída depois dos resultados da consulta ou na guia mensagens.

**Protocolo de atestado para vbs enclaves para Always Encrypted** Permite que você defina um protocolo de atestado para enclaves de segurança baseada em virtualização (VBS) usado pelo Always Encrypted com Secure enclaves.

Os protocolos de atestado com suporte atuais são:

* Serviço guardião de host – um protocolo de atestado usando o serviço guardião de host do Windows (HGS).

Para obter mais informações, consulte [Always Encrypted com Secure enclaves](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-enclaves?view=sqlallproducts-allversions) e [Secure enclave atestation](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-enclaves?view=sqlallproducts-allversions#secure-enclave-attestation).

**Restaurar Padrões** Redefine todos os valores dessa página com os valores padrão originais.
