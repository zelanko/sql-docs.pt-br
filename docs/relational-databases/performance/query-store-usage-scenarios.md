---
title: Cenários de uso do Repositório de Consultas | Microsoft Docs
description: Saiba como Repositório de Consultas pode ser usado para controlar e garantir um desempenho de carga de trabalho previsível. Considere vários exemplos no SQL Server.
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, usage scenarios
ms.assetid: f5309285-ce93-472c-944b-9014dc8f001d
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||= azure-sqldw-latest||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0d1da7312c338a866b4fb22df94175a7500d8f7c
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86457638"
---
# <a name="query-store-usage-scenarios"></a>Cenários de uso do Repositório de Consultas
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  O Repositório de Consultas pode ser usado em um amplo conjunto de cenários ao rastrear e garantir que o desempenho previsível da carga de trabalho é essencial. Veja alguns exemplos que você pode levar em consideração:  
  
-   Apontar e corrigir consultas com regressões de escolha do plano  
-   Identificar e ajustar as consultas que mais consumem recursos  
-   Testes de A/B  
-   Manter a estabilidade do desempenho durante a atualização para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mais recente  
-   Identifique e melhore as cargas de trabalho ad hoc  
  
## <a name="pinpoint-and-fix-queries-with-plan-choice-regressions"></a>Apontar e corrigir consultas com regressões de escolha do plano  
 Durante a execução da consulta regular, o Otimizador de Consulta pode decidir usar um plano diferente porque entradas importantes foram modificadas: a cardinalidade dos dados mudou, índices foram criados, alterados ou descartados, estatísticas foram recompiladas etc. Na maioria das vezes, o novo plano é melhor ou quase igual ao que estava sendo usado anteriormente. No entanto, há casos em que o novo plano é consideravelmente pior — essa situação é conhecida como regressão de alteração da escolha do plano. Antes do Repositório de Consultas, esse era um problema difícil de identificar e corrigir, pois o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não fornecia armazenamento de dados interno para que os usuários examinassem os planos de execução usados ao longo do tempo.  
  
 Com o Repositório de Consultas, é possível, rapidamente:  
  
-   Identificar todas as consultas cujas métricas de execução foram degradadas no período de interesse (última hora, dia, semana etc.). Use as **Consultas Regredidas** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para agilizar a análise.  
  
-   Entre as consultas regredidas, é fácil encontrar aquelas que tiveram vários planos e que foram degradadas devido à escolha de um plano ruim. Use o painel **Resumo do Plano** em **Consultas Regredidas** para visualizar todos os planos de uma consulta regredida e o respectivo desempenho ao longo do tempo.  
  
-   Forçar o plano anterior no histórico, caso seja provado que ele é melhor. Usar o botão **Forçar plano** em **Consultas Regredidas** para forçar o plano selecionado para a consulta.  
  
 ![query-store-usage-1](../../relational-databases/performance/media/query-store-usage-1.png "query-store-usage-1")  
  
 Para obter uma descrição detalhada do cenário, veja o blog [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/) (Repositório de Consultas: um gravador de dados de voo para seu banco de dados).  
  
## <a name="identify-and-tune-top-resource-consuming-queries"></a>Identificar e ajustar as consultas que mais consumem recursos  
 Embora a carga de trabalho possa gerar milhares de consultas, no geral, apenas algumas delas usam de fato a maioria dos recursos do sistema e, portanto, exigem sua atenção. Entre as consultas que mais consomem recursos, normalmente, você encontrará aquelas que são regredidas ou que podem ser aprimoradas com ajuste adicional.  
  
 A maneira mais fácil de começar a exploração é abrir as **Principais Consultas de Consumo de Recursos** no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. A interface do usuário é separada em três painéis: um histograma que representa as principais consultas de consumo de recursos (esquerdo), um resumo do plano para a consulta selecionada (direito) e o plano de consulta visual para o plano selecionado (inferior). Clique no botão **Configurar** para controlar quantas consultas você deseja analisar e o intervalo de tempo de interesse. Além disso, você pode escolher entre diferentes dimensões de consumo de recursos (duração, CPU, memória, E/S, número de execução) e a linha de base (Média, Mín., Máx., Total, Desvio Padrão).  
  
 ![query-store-usage-2](../../relational-databases/performance/media/query-store-usage-2.png "query-store-usage-2")  
  
 Veja o resumo do plano à direita para analisar o histórico de execução e saber mais sobre os diferentes planos e suas estatísticas de runtime. Use o painel inferior para examinar os diferentes planos ou para compará-los visualmente, renderizados lado a lado (use o botão Comparar).  
  
Ao identificar uma consulta com desempenho abaixo do ideal, sua ação dependerá da natureza do problema:  
  
1.  Se a consulta foi executada com vários planos e o último plano foi consideravelmente pior que o plano anterior, você poderá usar o mecanismo para forçar o plano a fim de garantir que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] use o plano ideal para execuções futuras  
  
2.  Verifique se o otimizador está sugerindo algum índice ausente no plano XML. Se sim, crie o índice ausente e use o Repositório de Consultas para avaliar o desempenho da consulta após a criação do índice  
  
3.  Certifique-se de que as estatísticas estejam atualizadas para as tabelas subjacentes usadas pela consulta.  
  
4.  Verifique se os índices usados pela consulta estão desfragmentados.  
  
5.  Pense em reescrever a consulta dispendiosa. Por exemplo, aproveite a parametrização da consulta e reduza o uso do SQL dinâmico. Implemente a lógica ideal ao ler os dados (aplique a filtragem de dados no lado do banco de dados, não do aplicativo).  

## <a name="ab-testing"></a>Testes de A/B  
 Use o Repositório de Consultas para comparar o desempenho da carga de trabalho antes e depois da alteração de aplicativo que você planeja introduzir. A lista a seguir contém vários exemplos em que é possível usar o Repositório de Consultas para avaliar o impacto do ambiente ou a alteração do aplicativo no desempenho da carga de trabalho:  
  
-   Distribuindo a nova versão do aplicativo.  
  
-   Adicionando novo hardware ao servidor.  
  
-   Criando índices ausentes em tabelas referenciadas por consultas caras.  
  
-   Aplicando política de filtragem para segurança no nível de linha. Para obter mais informações, confira [Otimizando a segurança em nível de linha com o Repositório de Consultas](https://blogs.msdn.com/b/sqlsecurity/archive/2015/07/21/optimizing-rls-performance-with-the-query-store.aspx).  
  
-   Adicionando controle de versão do sistema temporal a tabelas que são frequentemente modificadas pelos seus aplicativos OLTP.  
  
Em qualquer um desses cenários, aplique o fluxo de trabalho a seguir:  
  
1.  Execute a carga de trabalho com o Repositório de Consultas antes da alteração planejada para gerar a linha de base de desempenho.  
  
2.  Aplique a alteração do aplicativo no momento determinado.  
  
3.  Continue executando a carga de trabalho por tempo suficiente para gerar a imagem de desempenho do sistema após a mudança  
  
4.  Compare os resultados de 1 a 3.  
  
    1.  Abra **Consumo geral do banco de dados** para determinar o impacto no banco de dados inteiro.  
  
    2.  Abra **Principais Consultas de Consumo de Recursos** (ou execute sua própria análise usando o [!INCLUDE[tsql](../../includes/tsql-md.md)]) para analisar o impacto da alteração nas consultas mais importantes.  
  
5.  Decida se manterá a alteração ou executará a reversão quando o novo desempenho não for aceitável.  
  
A ilustração a seguir mostra a análise do Repositório de Consultas (etapa 4) no caso de criação de índice ausente. Abra o painel **Principais Consultas de Consumo de Recursos** /Resumo do plano para obter essa visão da consulta que deve ser afetada pela criação do índice:  
  
![query-store-usage-3](../../relational-databases/performance/media/query-store-usage-3.png "query-store-usage-3")  
  
Além disso, você pode comparar os planos antes e depois da criação do índice renderizando-os lado a lado. (Opção da barra de ferramentas "Comparar os planos para a consulta selecionada em uma janela separada", que é marcada com um quadrado vermelho.)  
  
![query-store-usage-4](../../relational-databases/performance/media/query-store-usage-4.png "query-store-usage-4")  
  
Planejar antes da criação do índice (plan_id  = 1, acima) tem dica de índice ausente, e como pode ser visto, essa Verificação de Índice Clusterizado foi o operador mais caro na consulta (retângulo vermelho).  
  
Plano depois da criação do índice ausente (plan_id  = 15, abaixo) agora tem Index Seek (Não clusterizado), que reduz o custo geral da consulta e aprimora o desempenho (retângulo verde).  
  
Com base na análise, você provavelmente mantém o índice, uma vez que o desempenho da consulta foi aprimorado.  
  
## <a name="keep-performance-stability-during-the-upgrade-to-newer-ssnoversion"></a><a name="CEUpgrade"></a> Manter a estabilidade do desempenho durante a atualização para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mais recente  
Antes do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], os usuários eram expostos ao risco de regressão de desempenho durante a atualização para a versão mais recente da plataforma. O motivo disso era o fato de que a versão mais recente do Otimizador de Consulta ficava ativa imediatamente assim que novos bits eram instalados.  
  
A partir do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] todas as alterações do otimizador de consulta são associadas ao [nível de compatibilidade do banco de dados](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) mais recente, portanto, os planos não são alterados diretamente no ponto de atualização, mas sim quando um usuário altera o `COMPATIBILITY_LEVEL` para o mais recente. Esse recurso, em combinação com o Repositório de Consultas, fornece um excelente nível de controle sobre o desempenho da consulta no processo de atualização. O fluxo de trabalho de atualização recomendado é mostrado na figura a seguir:  
  
![query-store-usage-5](../../relational-databases/performance/media/query-store-usage-5.png "query-store-usage-5")  
  
1.  Atualizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem alterar o nível de compatibilidade do banco de dados. Isso não expõe as últimas alterações do otimizador de consulta, mas ainda fornece os recursos mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluindo o Repositório de Consultas.  
  
2.  Habilite o Repositório de Consultas. Para obter mais informações sobre este tópico, consulte [Manter o Repositório de Consultas ajustado à sua carga de trabalho](../../relational-databases/performance/best-practice-with-the-query-store.md#Configure).

3.  Permitir que o Repositório de Consultas capture consultas e planos e estabeleça uma linha de base de desempenho com o nível de compatibilidade do banco de dados original/anterior. Mantenha-se nesta etapa tempo suficiente para capturar todos os planos e uma linha de base estável. Isso pode ter a duração de um ciclo comercial normal de uma carga de trabalho de produção.  
  
4.  Passe para o nível de compatibilidade do banco de dados mais recente: exponha sua carga de trabalho para as últimas alterações do otimizador de consulta e deixe-o possivelmente criar novos planos.  
  
5.  Use o Repositório de Consultas para correções de regressão e análise: geralmente, as novas alterações do otimizador de consulta geram planos melhores. No entanto, o Repositório de Consultas fornecerá uma maneira fácil de identificar as regressões de escolha do plano e corrigi-las usando um mecanismo para forçar plano. Começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)], ao usar o recurso de [Correção automática de plano](../../relational-databases/automatic-tuning/automatic-tuning.md#automatic-plan-correction), essa etapa se torna automática.  

    a.  Nos casos em que há regressões, force o bom plano conhecido anteriormente no repositório de consultas.  
  
    b.  Se houver planos de consulta que falham ao forçar ou se o desempenho ainda for insuficiente, considere reverter o [nível de compatibilidade do banco de dados](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) para a configuração anterior e, então, contatar Suporte ao Cliente Microsoft.  
    
> [!TIP]
> Use a tarefa *Atualizar banco de dados* de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para atualizar o [nível de compatibilidade do banco de dados](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-database-engine-upgrades) do banco de dados. Confira [Atualizando bancos de dados usando o Assistente de Ajuste de Consulta](../../relational-databases/performance/upgrade-dbcompat-using-qta.md) para obter mais detalhes.
  
## <a name="identify-and-improve-ad-hoc-workloads"></a>Identifique e melhore as cargas de trabalho ad hoc  
Algumas cargas de trabalho não possuem consultas dominantes que você pode ajustar para melhorar o desempenho geral do aplicativo. Geralmente, essas cargas de trabalho são caracterizadas por um número relativamente grande de consultas diferentes, cada uma delas consumindo parte dos recursos do sistema. Sendo exclusivas, essas consultas são executadas muito raramente (em geral, apenas uma vez, por isso, ad hoc), de modo que o respectivo consumo do runtime não é crítico. Por outro lado, considerando que esse aplicativo está gerando novas consultas o tempo todo, uma parte significativa dos recursos do sistema é gasto na compilação de consulta, o que não é ideal. Essa não é uma situação ideal para o Repositório de Consultas, uma vez que o número grande de consultas e planos enchem o espaço que você reservou, o que significa que o Repositório de Consultas provavelmente acabará no modo somente leitura muito rapidamente. Se você ativou a **Política de Limpeza Baseada em Tamanho** ([altamente recomendado](best-practice-with-the-query-store.md) para manter o Repositório de Consultas sempre funcionando), o processo em segundo plano limpará as estruturas do Repositório de Consultas na maior parte do tempo, também usando recursos significativos do sistema.  
  
 A exibição**Principais Consultas de Consumo de Recursos** fornece a primeira indicação da natureza ad hoc da carga de trabalho:  
  
![query-store-usage-6](../../relational-databases/performance/media/query-store-usage-6.png "query-store-usage-6")  
  
Use a métrica **Contagem de Execução** para analisar se as consultas principais são ad hoc (isso exige que você execute o Repositório de Consultas com `QUERY_CAPTURE_MODE = ALL`). No diagrama acima, você pode ver que 90% das suas **Principais Consultas de Consumo de Recursos** são executadas apenas uma vez.  
  
Como alternativa, é possível executar o script [!INCLUDE[tsql](../../includes/tsql-md.md)] para obter o número total de textos de consulta, consultas e planos no sistema e determinar o quanto eles são diferentes comparando query_hash e plan_hash:  
  
```sql  
--Do cardinality analysis when suspect on ad hoc workloads
SELECT COUNT(*) AS CountQueryTextRows FROM sys.query_store_query_text;  
SELECT COUNT(*) AS CountQueryRows FROM sys.query_store_query;  
SELECT COUNT(DISTINCT query_hash) AS CountDifferentQueryRows FROM  sys.query_store_query;  
SELECT COUNT(*) AS CountPlanRows FROM sys.query_store_plan;  
SELECT COUNT(DISTINCT query_plan_hash) AS  CountDifferentPlanRows FROM  sys.query_store_plan;  
```  
  
Esse é um resultado potencial que você pode obter em caso de carga de trabalho com consultas ad hoc:  
  
![query-store-usage-7](../../relational-databases/performance/media/query-store-usage-7.png "query-store-usage-7")  
  
O resultado da consulta mostra que, apesar do grande número de consultas e planos no Repositório de Consultas, os respectivos query_hash e query_plan_hash, na verdade, não são diferentes. Uma taxa entre textos de consulta exclusiva e query_hash exclusivo, que é muito maior que 1, é uma indicação de que a carga de trabalho é uma boa candidata à parametrização, pois a única diferença entre as consultas é a constante literal (parâmetro) fornecida como parte do texto de consulta.  
  
Geralmente, essa situação ocorrerá se o aplicativo gerar consultas (em vez de invocar procedimentos armazenados ou consultas parametrizadas) ou se ele depender de estruturas de mapeamento relacional de objeto que gere consultas por padrão.  
  
Se você estiver no controle do código do aplicativo, reescreva a camada de acesso a dados para utilizar procedimentos armazenados ou consultas parametrizadas. No entanto, essa situação também pode ser significativamente aprimorada sem mudanças no aplicativo, forçando a parametrização de consulta em todo o banco de dados (todas as consultas) ou nos modelos de consulta individuais com o mesmo query_hash.  
  
A abordagem com modelos de consulta individuais exige a criação do guia de plano:  
  
```sql  
--Apply plan guide for the selected query template 
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'<your query text goes here>',  
    @stmt OUTPUT,   
    @params OUTPUT;  
  
EXEC sp_create_plan_guide   
    N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION (PARAMETERIZATION FORCED)';  
```  
  
A solução com guias de plano é mais precisa, mas é mais trabalhosa.  
  
Se todas as consultas (ou a maioria delas) forem candidatas à parametrização automática, alterar `FORCED PARAMETERIZATION` para o banco de dados inteiro poderá ser uma opção mais adequada:  
  
```sql  
--Apply forced parameterization for entire database  
ALTER DATABASE <database name> SET PARAMETERIZATION FORCED;  
```  

> [!NOTE]
> Para obter mais informações sobre este tópico, consulte [Diretrizes para uso da parametrização forçada](../../relational-databases/query-processing-architecture-guide.md#ForcedParamGuide).

Depois de aplicar algumas dessas etapas, **Principais Consultas de Consumo de Recursos** mostrará uma imagem diferente da sua carga de trabalho.  
  
![query-store-usage-8](../../relational-databases/performance/media/query-store-usage-8.png "query-store-usage-8")  
  
Em alguns casos, seu aplicativo pode gerar muitas consultas diferentes que não são boas candidatas à parametrização automática. Nesse caso, você vê um grande número de consultas no sistema, mas a taxa entre consultas exclusivas e o `query_hash` exclusivo será, provavelmente, próximo a 1.  
  
Nesse caso talvez você queira habilitar a opção de servidor [**Otimizar para cargas de trabalho ad hoc**](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md) para evitar desperdício de memória de cache em consultas que provavelmente não serão executadas novamente. Para impedir a captura dessas consultas no Repositório de Consultas, defina `QUERY_CAPTURE_MODE` para `AUTO`.  
  
```sql  
EXEC sys.sp_configure N'show advanced options', N'1' RECONFIGURE WITH OVERRIDE
GO
EXEC sys.sp_configure N'optimize for ad hoc workloads', N'1'
GO
RECONFIGURE WITH OVERRIDE
GO 
  
ALTER DATABASE [QueryStoreTest] SET QUERY_STORE CLEAR;  
ALTER DATABASE [QueryStoreTest] SET QUERY_STORE = ON   
    (OPERATION_MODE = READ_WRITE, QUERY_CAPTURE_MODE = AUTO);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Prática recomendada com o Repositório de Consultas](../../relational-databases/performance/best-practice-with-the-query-store.md)         
 [Atualizando bancos de dados usando o Assistente de Ajuste de Consulta](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)           
  
