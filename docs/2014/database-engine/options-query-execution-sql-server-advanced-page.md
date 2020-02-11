---
title: 'Opções (execução da consulta: SQL Server: página avançado) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionAdvanced
ms.assetid: 3ec788c7-22c3-4216-9ad0-81a168d17074
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 5323054b77ed26a3ada816f44c1bf6764ded931d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089369"
---
# <a name="options-query-executionsql-serveradvanced-page"></a>Opções (página Execução da consulta/SQL Server/Avançado)
  Várias opções estão disponíveis usando o comando SET. Use essa página para especificar uma opção **set** para executar consultas do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Editor de Consultas do SQL Server. Elas não têm nenhum efeito em outros editores de códigos. As alterações feitas nessas opções são aplicadas apenas a novas consultas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para alterar as opções para as consultas atuais, clique em **Opções de Consulta** no menu **Consulta** ou no menu de atalho da janela de Consulta do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Em **Execução**, clique em **Avançado**. Para obter informações sobre cada um, consulte os Manuais Online do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>Opções  
 **DEFINIR NOCOUNT**  
 Não retorna a contagem do número de linhas, como uma mensagem com o conjunto de resultados. Essa caixa de seleção é desmarcada por padrão.  
  
 **DEFINIR NOEXEC**  
 Não executa a consulta. Essa caixa de seleção é desmarcada por padrão.  
  
 **DEFINIR PARSEONLY**  
 Verifica a sintaxe de cada consulta mas não executa as consultas. Essa caixa de seleção é desmarcada por padrão.  
  
 **SET CONCAT_NULL_YIELDS_NULL**  
 Quando essa caixa de seleção está marcada, as consultas que concatenam um valor existente com NULL sempre retornam NULL como resultado. Quando essa caixa de seleção é desmarcada, um valor existente concatenado com um NULL retorna o valor existente. Esta caixa de seleção fica marcada por padrão.  
  
 **SET ARITHABORT**  
 Quando essa caixa de seleção é marcada, quando uma instrução INSERT, DELETE ou UPDATE encontra um erro aritmético (estouro, divisão por zero ou um erro de domínio) durante a avaliação da expressão, a consulta ou lote é finalizado. Quando essa caixa de seleção estiver desmarcada, se possível, será fornecido um NULL para esse valor, a consulta continuará e será incluída uma mensagem com o resultado. Para obter mais informações, veja [SET ARITHABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-arithabort-transact-sql). Esta caixa de seleção fica marcada por padrão.  
  
 **DEFINIR SHOWPLAN_TEXT**  
 Quando essa caixa de seleção está marcada, o plano de consulta é retornado em formato de texto com cada consulta. Essa caixa de seleção está desmarcada por padrão.  
  
 **DEFINIR TEMPO DE ESTATÍSTICAS**  
 Quando essa caixa de seleção é marcada, as estatísticas de tempo são retornadas com cada consulta. Essa caixa de seleção é desmarcada por padrão.  
  
 **DEFINIR ESTATÍSTICAS DE E/S**  
 Quando essa caixa de seleção está marcada, as estatísticas relacionadas com a entrada e saída são retornadas com cada consulta. Essa caixa de seleção é desmarcada por padrão.  
  
 **SET TRANSACTION ISOLATION LEVEL**  
 O nível de isolamento da transação READ COMMITTED é definido por padrão. Para obter mais informações, veja [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql). Nível de isolamento da transação SNAPSHOT não está disponível. Para usar isolamento SNAPSHOT, adicione a seguinte instrução [!INCLUDE[tsql](../includes/tsql-md.md)] :  
  
```  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
GO  
```  
  
 **SET DEADLOCK PRIORITY**  
 O valor padrão Normal permite que cada consulta tenha a mesma prioridade quando ocorrer um deadlock. Selecione uma prioridade Baixa se você deseja que essa consulta perca qualquer conflito de deadlock e seja selecionada como a consulta a ser finalizada.  
  
 **SET LOCK TIMEOUT**  
 O valor padrão -1 indica que os bloqueios sejam mantidos até que as transações sejam completadas. Um valor 0 significa não esperar e retornar uma mensagem assim que for encontrado um bloqueio. Forneça um valor maior que 0 milissegundo para encerrar a transação se os bloqueios para a transação devem ser mantidos por um tempo maior que esse.  
  
 **SET QUERY_GOVERNOR_COST_LIMIT**  
 Use a opção **QUERY_GOVERNOR_COST_LIMIT** para especificar um limite superior para o tempo durante o qual uma consulta pode ser executada. O custo da consulta refere-se ao tempo decorrido estimado, em segundos, necessário para concluir uma consulta em uma configuração de hardware específica. A configuração padrão 0 indica que não existe limite para o intervalo de tempo no qual uma consulta será executada.  
  
 **Suprimir cabeçalhos de mensagem do provedor**  
 Quando essa caixa de seleção está marcada, as mensagens de status do provedor (como o provedor SQLClient) não são exibidas. Esta caixa de seleção fica marcada por padrão. Desmarque essa caixa de seleção para ver as mensagens do provedor ao solucionar problemas com consultas que podem estar falhando no nível do provedor.  
  
 **Desconectar depois que a consulta for executada**  
 Quando essa caixa de seleção está marcada, a conexão com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é finalizada após a conclusão da consulta. Essa caixa de seleção é desmarcada por padrão.  
  
 **Redefinir para padrão**  
 Redefine todos os valores dessa página com os valores padrão originais.  
  
  
