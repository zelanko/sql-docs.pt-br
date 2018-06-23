---
title: Migrar planos de consulta | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- query plans [SQL Server], migrating
- upgrading SQL Server, migrating query plans
- plan guides [SQL Server], migrating query plans
ms.assetid: 7e02a137-6867-4f6a-a45a-2b02674f7e65
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 66b481ab27af87a20f1a509cb10749c9f2ca1c15
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019419"
---
# <a name="migrate-query-plans"></a>Migrar planos de consulta
  Na maioria dos casos, a atualização de um banco de dados para a versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resultará em melhoria do desempenho de consulta. No entanto, se você tiver consultas essenciais que foram cuidadosamente ajustadas para desempenho, pode desejar preservar os planos dessas consultas antes da atualização através da criação de um guia de plano para cada consulta. Se depois da atualização o otimizador de consultas escolher um plano menos eficiente para uma ou mais consultas, você pode habilitar os guias de plano e forçar o otimizador de consulta a usar planos anteriores à atualização.  
  
 Para criar guias de plano antes da atualização siga estas etapas:  
  
1.  Registre o plano atual para cada consulta crítica usando o [sp_create_plan_guide](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql) procedimento armazenado e especificar o plano de consulta na dica de consulta USE PLAN.  
  
2.  Verifique se o guia de plano foi aplicado à consulta.  
  
3.  Atualize o banco de dados para a versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Os planos permanecem no banco de dados atualizado nos guias de plano e servem como sistema de apoio no caso de regressões de plano após a atualização.  
  
     Recomendamos que os guias de plano não sejam habilitados depois da atualização por que você pode perder oportunidades de planos melhores na versão nova ou recompilações vantajosas devido a estatísticas atualizadas.  
  
4.  Se planos menos eficientes forem escolhidos após a atualização, habilite todos ou um subconjunto dos guias de planos para substituir os planos novos.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como registrar um plano anterior à atualização para uma consulta através da criação de um guia de plano.  
  
### <a name="step-1-collect-the-plan"></a>Etapa 1: Colete o plano  
 O plano de consulta registrado no guia de plano deve estar em formato XML. Planos de consulta em formato XML podem ser produzidos das seguintes formas:  
  
-   [SET SHOWPLAN_XML](/sql/t-sql/statements/set-showplan-xml-transact-sql)  
  
-   [SET STATISTICS XML](/sql/t-sql/statements/set-statistics-xml-transact-sql)  
  
-   Consultando a coluna query_plan do [sys.DM exec_query_plan](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql) função de gerenciamento dinâmico.  
  
-   O [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] [Showplan XML](../../relational-databases/event-classes/showplan-xml-event-class.md), [Showplan XML Statistics Profile](../../relational-databases/event-classes/showplan-xml-statistics-profile-event-class.md), e [Showplan XML para Query Compile](../../relational-databases/event-classes/showplan-xml-for-query-compile-event-class.md) classes de evento.  
  
 O exemplo a seguir coleta o plano de consulta para a instrução `SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;` examinando exibições de gerenciamento dinâmico.  
  
```  
USE AdventureWorks;  
GO  
SELECT query_plan  
    FROM sys.dm_exec_query_stats AS qs   
    CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
    CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, DEFAULT, DEFAULT) AS qp  
    WHERE st.text LIKE N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;%';  
GO  
```  
  
### <a name="step-2-create-the-plan-guide-to-force-the-plan"></a>Etapa 2: Crie a guia de plano para forçar o plano  
 Usando o plano de consulta com formato XML (obtido através de qualquer um dos métodos anteriormente descritos) no guia de plano, copie e cole o plano de consulta como uma literal de cadeia de caracteres dentro da dica de consulta USE PLAN especificada na cláusula OPTION de sp_create_plan_guide.  
  
 No próprio plano XML, faça a saída das aspas (') que aparecem no plano com um segundo sinal de aspas antes de criar o guia de plano. Por exemplo, a saída de um plano que contenha `WHERE A.varchar = 'This is a string'` deve ser feita modificando-se o código para `WHERE A.varchar = ''This is a string''`.  
  
 O exemplo a seguir cria um guia de plano para o plano da consulta coletado na etapa 1 e insere o Plano de Execução XML para a consulta no parâmetro `@hints`. Para ser breve, apenas uma saída parcial do Plano de Execução é incluída no exemplo.  
  
```  
EXECUTE sp_create_plan_guide   
@name = N'Guide1',  
@stmt = N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;',  
@type = N'SQL',  
@module_or_batch = NULL,  
@params = NULL,  
@hints = N'OPTION(USE PLAN N''<ShowPlanXML xmlns=''''http://schemas.microsoft.com/sqlserver/2004/07/showplan''''   
    Version=''''0.5'''' Build=''''9.00.1116''''>  
    <BatchSequence><Batch><Statements><StmtSimple>  
    …  
    </StmtSimple></Statements></Batch>  
    </BatchSequence></ShowPlanXML>'')';  
GO  
```  
  
### <a name="step-3-verify-that-the-plan-guide-is-applied-to-the-query"></a>Etapa 3: Verifique se o guia de plano foi aplicado à consulta.  
 Execute a consulta novamente e examine o plano de consulta produzido. Você deve verificar se o plano corresponde ao que você especificou no guia de plano.  
  
## <a name="see-also"></a>Consulte também  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Dicas de consulta &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [Guias de plano](../../relational-databases/performance/plan-guides.md)  
  
  
