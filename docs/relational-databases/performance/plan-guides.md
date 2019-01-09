---
title: Guias de plano | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- TEMPLATE plan guide
- SQL plan guides
- OPTIMIZE FOR query hint
- RECOMPILE query hint
- OBJECT plan guide
- plan guides [SQL Server], about plan guides
- OPTION clause
- plan guides [SQL Server]
- USE PLAN query hint
ms.assetid: bfc97632-c14c-4768-9dc5-a9c512f6b2bd
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 606778f5505e6ba7e22ade1394a0169fce4a918b
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53375238"
---
# <a name="plan-guides"></a>Guias de plano
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Guias de plano permitem otimizar o desempenho das consultas quando você não pode ou não quer alterar diretamente o texto da consulta real no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. As guias de plano influenciam a otimização das consultas, anexando dicas de consulta ou um plano de consulta fixo. Guias de plano podem ser úteis quando um subconjunto pequeno de consultas em um aplicativo de banco de dados fornecido por um terceiro não estiver executando como esperado. No guia de plano, especifique a instrução Transact-SQL que deve ser otimizada, e uma cláusula OPTION que contenha as dicas de consulta a serem usadas ou um plano de consulta específico a ser usado para otimizar a consulta. Quando a consulta é feita, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] corresponde a instrução Transact-SQL com a guia de plano e anexa a cláusula OPTION à consulta em tempo de execução ou usa o plano de consulta especificado.  
  
 O número total de guias de plano que é possível criar só está limitado através de recursos do sistema disponíveis. De outro modo, guias de plano devem ser limitados para consultas de missão-crítica que são direcionados para aprimorar ou estabilizar o desempenho. Guias de plano não podem ser usados para influenciar a maioria da carga de consulta de um aplicativo implantado.  
  
> [!NOTE]
>  Os guias de plano não podem ser usados em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md). As guias de plano são visíveis em qualquer edição. Também é possível anexar um banco de dados contendo guias de plano a qualquer edição. Os guias de plano permanecem intactos quando o banco de dados é restaurado ou anexado a uma versão atualizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="types-of-plan-guides"></a>Tipos de guias de plano  
 Podem ser criados os tipos de guias de plano a seguir.  
  
 ### <a name="object-plan-guide"></a>Guia de plano OBJECT  
 O guia de plano OBJECT corresponde as consultas executadas no contexto dos procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] , funções escalares definidas pelo usuário, funções com valor de tabela de várias instruções definidas pelo usuário e gatilhos DML.  
  
 Suponha que o procedimento armazenado a seguir, que usa o parâmetro `@Country_region`, esteja em um aplicativo de banco de dados implantado no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]:  
  
```sql  
CREATE PROCEDURE Sales.GetSalesOrderByCountry (@Country_region nvarchar(60))  
AS  
BEGIN  
    SELECT *  
    FROM Sales.SalesOrderHeader AS h, Sales.Customer AS c,   
        Sales.SalesTerritory AS t  
    WHERE h.CustomerID = c.CustomerID  
        AND c.TerritoryID = t.TerritoryID  
        AND CountryRegionCode = @Country_region  
END;  
```  
  
 Suponha que esse procedimento armazenado foi compilado e otimizado para `@Country_region = N'AU'` (Austrália). Entretanto, já que há relativamente poucas vendas oriundas da Austrália, o desempenho cai quando a consulta é executada com os valores de parâmetro de países com mais pedidos de vendas. Como a maioria dos pedidos de vendas tem origem nos Estados Unidos, um plano de consulta gerado para `@Country_region = N'US'` provavelmente teria execução melhor para todos os valores possíveis do parâmetro `@Country_region` .  
  
 É possível corrigir esse problema ao modificar o procedimento armazenado para adicionar a dica de consulta `OPTIMIZE FOR` à consulta. Porém, já que o procedimento armazenado está em um aplicativo implantado, não é possível modificar diretamente o código do aplicativo. Ao contrário, é possível criar o guia de plano a seguir no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```sql  
sp_create_plan_guide   
@name = N'Guide1',  
@stmt = N'SELECT *FROM Sales.SalesOrderHeader AS h,  
        Sales.Customer AS c,  
        Sales.SalesTerritory AS t  
        WHERE h.CustomerID = c.CustomerID   
            AND c.TerritoryID = t.TerritoryID  
            AND CountryRegionCode = @Country_region',  
@type = N'OBJECT',  
@module_or_batch = N'Sales.GetSalesOrderByCountry',  
@params = NULL,  
@hints = N'OPTION (OPTIMIZE FOR (@Country_region = N''US''))';  
```  
  
 Quando a consulta especificada na instrução `sp_create_plan_guide` é executada, a consulta é modificada antes da otimização para incluir a cláusula `OPTIMIZE FOR (@Country = N''US'')` .  
  
 ### <a name="sql-plan-guide"></a>Guia de plano SQL  
 O guia de plano SQL correlaciona consultas que são executadas no contexto de instruções e lotes do [!INCLUDE[tsql](../../includes/tsql-md.md)] autônomo que não fazem parte de um objeto do banco de dados. Os guias de plano com base em SQL também podem ser usados para corresponder consultas com parâmetros uma forma especificada. Os guias de plano SQL se aplicam a instruções e lotes [!INCLUDE[tsql](../../includes/tsql-md.md)] autônomos. Frequentemente, essas instruções são submetidas por um aplicativo por meio do procedimento armazenado do sistema [sp_executesql](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md) . Por exemplo, considere o seguinte lote autônomo:  
  
```sql  
SELECT TOP 1 * FROM Sales.SalesOrderHeader ORDER BY OrderDate DESC;  
```  
  
 Para impedir que um plano de execução paralelo seja gerado nessa consulta, crie o guia de plano a seguir e defina a dica de consulta `MAXDOP` como `1` no parâmetro `@hints` .  
  
```sql  
sp_create_plan_guide   
@name = N'Guide2',   
@stmt = N'SELECT TOP 1 * FROM Sales.SalesOrderHeader ORDER BY OrderDate DESC',  
@type = N'SQL',  
@module_or_batch = NULL,   
@params = NULL,   
@hints = N'OPTION (MAXDOP 1)';  
```  
  
> [!IMPORTANT]  
>  Os valores fornecidos para os argumentos `@module_or_batch` e `@params` da instrução `sp_create_plan guide` devem coincidir com o texto correspondente submetido na consulta real. Para obter mais informações, veja [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md) e [Usar o SQL Server Profiler para criar e testar guias de plano](../../relational-databases/performance/use-sql-server-profiler-to-create-and-test-plan-guides.md).  
  
 Os guias de plano SQL também podem ser criados em consultas com parâmetros da mesma forma quando a opção de banco de dados PARAMETERIZATION for SET to FORCED ou quando um guia de plano TEMPLATE for criado especificando uma classe de consulta com parâmetros.  
  
 ### <a name="template-plan-guide"></a>guia de plano TEMPLATE  
 O guia de plano TEMPLATE corresponde consultas autônomas com parâmetros com uma forma especificada. Esses guias de plano são usados para substituir a opção SET do banco de dados PARAMETERIZATION atual de um banco de dados para a classe de consultas.  
  
 É possível criar um guia de plano TEMPLATE em qualquer uma das seguintes situações:  
  
-   A opção de banco de dados PARAMETERIZATION é SET to FORCED, mas há consultas que devem ser compiladas de acordo com as regras de [Parametrização Simples](../../relational-databases/query-processing-architecture-guide.md#SimpleParam).  
  
-   A opção de banco de dados PARAMETERIZATION é SET to SIMPLE (configuração padrão), mas é preciso que a [Parametrização Forçada](../../relational-databases/query-processing-architecture-guide.md#ForcedParam) seja testada em uma classe de consultas.  
  
## <a name="plan-guide-matching-requirements"></a>Guia de plano correspondente a requisitos  
 Guias de plano são aplicados ao banco de dados no qual eles são criados. Portanto, somente os guias de plano presentes no banco de dados se tornam atuais quando uma consulta pode ser combinada com outra. Por exemplo, se [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] for o banco de dados atual e a consulta seguinte executa:  
  
 ```sql
 SELECT FirstName, LastName FROM Person.Person;
 ```  
  
 Somente guias de plano do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] são elegíveis para corresponderem a essa consulta. Porém, se [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] for o banco de dados atual e as instruções seguintes são executadas:  
  
 ```sql
 USE DB1; 
 SELECT FirstName, LastName FROM Person.Person;
 ```  
  
 Somente os guias de plano no `DB1` são elegíveis para combinar com a consulta porque ela é executada no contexto de `DB1`.  
  
 Para guias de plano baseados em SQL ou em MODELO, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] faz a correspondência dos valores dos argumentos @module_or_batch and @params com uma consulta, comparando os dois valores, caractere por caractere. Isso significa você deve fornecer o texto exatamente como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recebe no lote atual.  
  
 Quando @type = 'SQL' e @module_or_batch forem definidos como NULL, o valor @module_or_batch será definido com o valor @stmt. Isso significa que o valor de *statement_text* deve ser fornecido exatamente no mesmo formato, caractere a caractere, como enviado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nenhuma conversão interna é executada para facilitar essa correspondência.  
  
 Quando um guia de plano normal (SQL ou OBJECT) e um guia de plano de MODELO puderem ser aplicados a uma instrução, somente o guia de plano normal será usado.  
  
> [!NOTE]  
>  O lote que contém a instrução na qual se quer criar o guia de plano não pode conter uma instrução de USE *database* .  
  
## <a name="plan-guide-effect-on-the-plan-cache"></a>Efeito do guia de plano no cache do esquema  
 Criar um guia de plano em um módulo remove o plano de consulta desse módulo do cache do esquema. Criar um guia de plano do tipo OBJECT ou SQL em um lote remove o plano de consulta de um lote que tem o mesmo valor de hash. Criar um guia de plano do tipo TEMPLATE remove todos os lotes da instrução única do cache do esquema dentro desse banco de dados.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tarefa|Tópico|  
|----------|-----------|  
|Descreve como criar um guia de plano.|[Criar um novo guia de plano](../../relational-databases/performance/create-a-new-plan-guide.md)|  
|Descreve como criar uma guia de plano para consultas parametrizadas.|[Criar um guia de plano para consultas parametrizadas](../../relational-databases/performance/create-a-plan-guide-for-parameterized-queries.md)|  
|Descreve como controlar o comportamento de parametrização da consulta usando guias de plano.|[Especificar comportamento de parametrização de consulta usando guias de plano](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)|  
|Descreve como incluir um plano de consulta fixo em um guia de plano.|[Aplicar um plano de consulta fixo a um guia de plano](../../relational-databases/performance/apply-a-fixed-query-plan-to-a-plan-guide.md)|  
|Descreve como especificar dicas de consulta em um guia de plano.|[Anexar dicas de consulta para um guia de plano](../../relational-databases/performance/attach-query-hints-to-a-plan-guide.md)|  
|Descreve como exibir propriedades do guia de plano.|[Exibir propriedades de guia de plano](../../relational-databases/performance/view-plan-guide-properties.md)|  
|Descreve como usar o SQL Server Profiler para criar e testar guias de plano.|[Usar o SQL Server Profiler para criar e testar guias de plano](../../relational-databases/performance/use-sql-server-profiler-to-create-and-test-plan-guides.md)|  
|Descreve como validar guias de plano.|[Validar guias de plano depois da atualização](../../relational-databases/performance/validate-plan-guides-after-upgrade.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)   
 [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)   
 [sys.plan_guides &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md)   
 [sys.fn_validate_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md)  
  
  
