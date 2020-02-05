---
title: Criar e testar guias de plano
titleSuffix: SQL Server Profiler
description: Como criar e testar guias de plano no SQL Server Profiler.
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- checking plan guides
- plan guides [SQL Server], testing
- plan guides [SQL Server], SQL Server Profiler
- matching queries to plan guides [SQL Server]
- testing plan guides
- SQL Server Profiler, plan guides
- plan guides [SQL Server], creating
- capturing query text [SQL Server]
- verifying plan guides
- Profiler [SQL Server Profiler], plan guides
- query-to-plan guide matching [SQL Server]
ms.assetid: 7018dbf0-1a1a-411a-88af-327bedf9cfbd
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 2879807d7eb64446a26ea5857f33c52fe7b78970
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74165931"
---
# <a name="use-sql-server-profiler-to-create-and-test-plan-guides"></a>Usar o SQL Server Profiler para criar e testar guias de plano
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Ao criar um guia de plano, você poderá usar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para capturar o texto de consulta exato para usar no argumento *statement_text* do procedimento armazenado **sp_create_plan_guide** . Isto ajuda a certificar que o guia de plano será correspondido à consulta no tempo de compilação. Depois que o guia de plano é criado, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] também pode ser usado para testar se o guia de plano está, de fato, sendo correspondido à consulta. De maneira geral, você deve testar guias de plano usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para verificar se a sua consulta está sendo correspondida ao guia de plano.  
  
## <a name="capturing-query-text-by-using-sql-server-profiler"></a>Como capturar texto de consulta usando o SQL Server Profiler  
 Se você executar uma consulta e capturar o texto exatamente como foi submetido ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], será possível criar um guia de plano do tipo SQL ou TEMPLATE que corresponderá exatamente ao texto de consulta. Isto certifica que o guia de plano seja usado pelo otimizador de consulta.  
  
 Considere a seguinte consulta, que é submetida por um aplicativo como um lote autônomo:  
  
```  
SELECT COUNT(*) AS c  
FROM Sales.SalesOrderHeader AS h  
INNER JOIN Sales.SalesOrderDetail AS d  
  ON h.SalesOrderID = d.SalesOrderID  
WHERE h.OrderDate BETWEEN '20000101' and '20050101';  
```  
  
 Suponha que você queira que essa consulta execute uma operação de mescla de junção, mas SHOWPLAN indica que a consulta não está usando uma mescla de junção. Você não pode alterar a consulta diretamente no aplicativo, então, em vez disso, cria um guia de plano para especificar que a dica de consulta MERGE JOIN seja acrescentada à consulta no tempo de compilação.  
  
 Para capturar o texto da consulta exatamente como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o recebe, execute as seguintes etapas:  
  
1.  Inicie um rastreamento de [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] , certificando-se de que o tipo de evento **do SQL:BatchStarting** esteja selecionado.  
  
2.  Faça com que o aplicativo execute a consulta.  
  
3.  Pause o rastreamento do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] .  
  
4.  Clique no evento **SQL:BatchStarting** que corresponde à consulta.  
  
5.  Clique com o botão direito do mouse e selecione **Extrair Dados de Eventos**.  
  
    > [!IMPORTANT]  
    >  Não tente copiar o texto em lote selecionando-o no painel inferior da janela de rastreamento do Profiler. Isto pode fazer com que o guia de plano que você criou não corresponda ao lote original.  
  
6.  Salve os dados de evento em um arquivo. Este é o texto em lote.  
  
7.  Abra o arquivo de texto em lote no Bloco de Notas e copie o texto no buffer copiar e colar.  
  
8.  Crie o guia de plano e cole o texto copiado dentro das aspas ( **''** ) especificadas para o argumento **\@stmt**. Você deve escapar todas as aspas únicas no argumento **\@stmt**, precedendo-as com outra aspa única. Tenha cuidado para não adicionar ou remover nenhum outro caractere quando você inserir essas aspas individuais. Por exemplo, a literal de data **'** 20000101 **'** deve ser delimitada como **20000101**" **.**  
  
 Aqui está o guia de plano:  
  
```  
EXEC sp_create_plan_guide   
    @name = N'MyGuide1',  
    @stmt = N'<paste the text copied from the batch text file here>',  
    @type = N'SQL',  
    @module_or_batch = NULL,  
    @params = NULL,  
    @hints = N'OPTION (MERGE JOIN)';  
```  
  
## <a name="testing-plan-guides-by-using-sql-server-profiler"></a>Como testar guias de plano usando o SQL Server Profiler  
 Para verificar se um guia de plano está sendo correspondido a uma consulta, execute as seguintes etapas:  
  
1.  Inicie um novo rastreamento [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e verifique se o tipo de evento **Showplan XML** está selecionado (localizado abaixo do nó **Desempenho** ).  
  
2.  Faça com que o aplicativo execute a consulta.  
  
3.  Pause o rastreamento do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] .  
  
4.  Localize o evento **Plano de Execução XML** para a consulta afetada.  
  
    > [!NOTE]  
    >  O evento **Showplan XML for Query Compile** não pode ser usado. **PlanGuideDB** não existe nesse evento.  
  
5.  Se o guia de plano for do tipo OBJECT ou SQL, verifique se o evento **Plano de Execução XML** contém os atributos **PlanGuideDB** e **PlanGuideName** para o guia de plano que você espera que corresponda à consulta. Ou, no caso de um guia de plano de TEMPLATE, verifique se o evento **Plano de Execução XML** contém os atributos **TemplatePlanGuideDB** e **TemplatePlanGuideName** para o guia de plano esperada. Isto verifica se o guia de plano está funcionando. Esses atributos estão contidos no elemento do plano **\<StmtSimple>** .  
  
## <a name="see-also"></a>Consulte Também  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
  
  
