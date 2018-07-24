---
title: Práticas recomendadas com o repositório de consultas | Microsoft Docs
ms.custom: ''
ms.date: 11/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Query Store, best practices
ms.assetid: 5b13b5ac-1e4c-45e7-bda7-ebebe2784551
caps.latest.revision: 24
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 30a22bd9661ea6b5be5d33fad5a9ce03e4f3b1c1
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38981418"
---
# <a name="best-practice-with-the-query-store"></a>Melhor prática com o Repositório de Consultas
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Este tópico descreve as práticas recomendadas para usar o Repositório de Consultas com sua carga de trabalho.  
  
##  <a name="SSMS"></a> Use a versão mais recente do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] tem um conjunto de interfaces do usuário projetadas para configurar o Repositório de Consultas, bem como para consumir os dados sobre sua carga de trabalho coletados.  
Baixe a versão mais recente do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] [aqui](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).  
  
 Para ver uma descrição rápida sobre como usar o Repositório de Consultas em cenários de solução de problemas, consulte [Repositório de Consultas @Azure Blogs](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).  
  
##  <a name="Insight"></a> Usar a Análise de Desempenho de Consultas no banco de dados SQL do Azure  
 Se você executar o Repositório de Consultas em [!INCLUDE[ssSDS](../../includes/sssds-md.md)] , você poderá usar a **Análise de Desempenho de Consultas** para analisar o consumo de DTU ao longo do tempo.  
Embora você possa usar [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para obter o consumo de recursos detalhado de todas as suas consultas (CPU, memória, E/S, etc.), a Análise de Desempenho de Consultas fornece uma maneira rápida e eficiente para determinar seu impacto sobre o consumo de DTU geral do seu banco de dados.  
Para obter mais informações, consulte [Análise de Desempenho de Consultas do Banco de Dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-query-performance/).    

##  <a name="using-query-store-with-elastic-pool-databases"></a>Usando o Repositório de Consultas com Bancos de Dados de Pools Elásticos
Você pode usar o Repositório de Consultas em todos os bancos de dados sem problemas, mesmo em pools densamente compactados. Todos os problemas relacionados ao uso excessivo de recursos, que podem ter ocorrido quando o Repositório de Consultas foi habilitado para o grande número de bancos de dados nos Pools Elásticos, foram resolvidos.

##  <a name="Configure"></a> Mantenha o Repositório de Consultas ajustado à sua carga de trabalho  
 Configure o Repositório de Consultas com base na sua carga de trabalho e nos requisitos para solução de problemas de desempenho.   
Os parâmetros padrão são bons para um início rápido, mas você deve monitorar o comportamento do Repositório de Consultas ao longo do tempo e ajustar sua configuração adequadamente:  
  
 ![query-store-properties](../../relational-databases/performance/media/query-store-properties.png "query-store-properties")  
  
 Aqui estão as diretrizes a seguir para definir valores de parâmetro:  
  
 **Tamanho Máximo (MB):** especifica o limite para o espaço de dados que o Repositório de Consultas admitirá em seu banco de dados.  Essa é a configuração mais importante, que afeta diretamente o modo de operação do Repositório de Consultas.  
  
 Conforme o Repositório de Consultas coleta consultas, planos de execução e estatísticas, seu tamanho no banco de dados cresce até esse limite ser atingido. Quando isso acontece, o Repositório de Consultas automaticamente altera o modo de operação para somente leitura e para de coletar novos dados, o que significa que a análise de desempenho não é mais precisa.  
  
 O valor padrão (100 MB) pode não ser suficiente se sua carga de trabalho gerar muitos e planos e consultas diferentes, ou caso você deseje manter o histórico de consulta por um período de tempo maior. Controle o uso de espaço atual e aumente o Tamanho Máximo (MB) para impedir que o Repositório de Consultas passe para o modo somente leitura.  Use [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou execute o script a seguir para obter as informações mais recentes sobre o tamanho do Repositório de Consultas:  
  
```sql 
USE [QueryStoreDB];  
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason  
FROM sys.database_query_store_options;  
```  
  
 O script a seguir define um novo Tamanho Máximo (MB):  
  
```sql  
ALTER DATABASE [QueryStoreDB]  
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);  
```  
  
 **Intervalo de Coleta de Estatísticas:** define o nível de granularidade para a estatística de tempo de execução coletada (o padrão é 1 hora). Considere usar o valor mais baixo se você precisar de granularidade mais fina ou menos tempo para detectar e mitigar os problemas, mas tenha em mente que isso afetará diretamente o tamanho dos dados do Repositório de Consultas. Use o SSMS ou Transact-SQL para definir um valor diferente para o Intervalo de Coleta de Estatísticas:  
  
```sql  
ALTER DATABASE [QueryStoreDB] SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 60);  
```  
  
 **Limite de Consulta Obsoleto (Dias):** política de limpeza com base em tempo que controla o período de retenção de estatísticas de tempo de execução persistentes e consultas inativas.  
Por padrão, o Repositório de Consultas está configurado para manter os dados por 30 dias, o que pode ser desnecessariamente longo para seu cenário.  
  
 Evite manter dados históricos que você não planeja usar. Isso reduzirá as alterações para o status somente leitura. O tamanho dos dados do Repositório de Consultas, bem como o tempo para detectar e reduzir o problema, serão mais previsíveis. Use [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou o script a seguir para configurar a política de limpeza com base em tempo:  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 90));  
```  
  
 **Modo de Limpeza com Base no Tamanho:** especifica se a limpeza automática de dados ocorrerá quando o tamanho dos dados no Repositório de Consultas se aproximar do limite.  
  
 É altamente recomendável ativar limpeza com base no tamanho para certificar-se de que o repositório de consultas seja sempre executado no modo de leitura-gravação e colete sempre os dados mais recentes.  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);  
```  
  
 **Modo de Captura do Repositório de Consultas:** Especifica a política de captura de consultas para o repositório de consultas.  
  
-   **All** – captura todas as consultas. Essa é a opção padrão.  
  
-   **Auto** – consultas incomuns e consultas com duração de compilação e execução insignificantes são ignoradas. Os limites para a duração da execução de contagem, da compilação e do tempo de execução são determinados internamente.  
  
-   **None** – o Repositório de Consultas para de capturar novas consultas.  
  
 O script a seguir define o Modo de Captura de Consultas para Auto:  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);  
```  
  
## <a name="how-to-start-with-query-performance-troubleshooting"></a>Como começar a solução de problemas de desempenho de consulta  
 Solucionar problemas de fluxo de trabalho com o Repositório de Consultas é simples, conforme mostrado no diagrama a seguir:  
  
 ![query-store-troubleshooting](../../relational-databases/performance/media/query-store-troubleshooting.png "query-store-troubleshooting")  
  
 Habilite o Repositório de Consultas usando [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] conforme descrito na seção anterior, ou execute a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir:  
  
```sql  
ALTER DATABASE [DatabaseOne] SET QUERY_STORE = ON;  
```  
  
 Levará algum tempo até que o Repositório de Consultas colete o conjunto de dados que representa com precisão a sua carga de trabalho. Geralmente, um dia é suficiente até mesmo para cargas de trabalho muito complexas. No entanto, você pode começar a explorar os dados e identificar as consultas que exigem atenção imediatamente após a habilitação do recurso.   
Navegue até a subpasta do Repositório de Consultas sob o nó do banco de dados no Pesquisador de Objetos de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para abrir modos de exibição de solução de problemas para cenários específicos.   
[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] Os modos de exibição do Repositório de Consultas operam com o conjunto de métricas de execução, cada uma expressa em qualquer uma das seguintes funções de estatística:  
  
|Versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Métrica de execução|Função estatística|  
|----------------------|----------------------|------------------------|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|Tempo de CPU, Duração, Contagem de Execução, Leituras Lógicas, Gravações Lógicas, Consumo de memória, Leituras Físicas, tempo de CLR, DOP (Grau de Paralelismo) e Contagem de Linhas|Média, Máximo, Mínimo, Desvio Padrão, Total|
|[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|Tempo de CPU, Duração, Contagem de Execução, Leituras Lógicas, Gravações Lógicas, Consumo de memória, Leituras Físicas, tempo de CLR, DOP (Grau de Paralelismo), Contagem de Linhas, Memória de log, Memória TempDB e Tempos de espera|Média, Máximo, Mínimo, Desvio Padrão, Total|
  
 O gráfico a seguir mostra como localizar os modos de exibição do Repositório de Consultas:  
  
 ![query-store-views](../../relational-databases/performance/media/query-store-views.png "query-store-views")  
  
 A tabela a seguir explica quando usar cada um dos modos de exibição do Repositório de Consultas:  
  
|Exibição do SSMS|Cenário|  
|---------------|--------------|  
|Consultas regredidas|Identifique as consultas para as quais as métricas de execução regrediram recentemente (isto é, mudaram para pior). <br />Use esta exibição para correlacionar os problemas de desempenho observados em seu aplicativo com as consultas reais que precisam ser corrigidas ou melhoradas.|  
|Consumo geral de recursos|Analise o consumo de recursos total do banco de dados para qualquer uma das métricas de execução.<br />Use esta exibição para identificar padrões de recurso (diariamente em vez de cargas de trabalho noturnas) e otimizar o consumo geral do seu banco de dados.|  
|Consultas com maior consumo de recursos|Escolha uma métrica de execução de seu interesse e identifique as consultas que tinham os valores mais extremos em um intervalo de tempo fornecido. <br />Use esse modo de exibição para concentrar sua atenção nas consultas mais relevantes, as que apresentam o maior impacto no consumo de recursos do banco de dados.|  
|Consultas com planos forçados|Listas de planos forçados anteriormente usando o Repositório de Consultas. <br />Use esta exibição para acessar rapidamente todos os planos forçados no momento.|  
|Consultas com alta variação|Analise consultas com alta variação de execução relacionadas a qualquer dimensão disponível, como Duração, Tempo de CPU, E/S e Uso de memória no intervalo de tempo desejado.<br />Use esta exibição para identificar consultas com desempenho amplamente variável que possam afetar a experiência do usuário em seus aplicativos.|  
|Consultas rastreadas|Acompanhe a execução das consultas mais importantes em tempo real. Normalmente, você usa este modo de exibição quando você tem consultas com planos forçados e você deseja certificar-se de que o desempenho de consultas é estável.|
  
> [!TIP]  
>  Para obter uma descrição detalhada como usar o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para identificar as consultas com maior consumo de recursos e corrigir as que regrediram devido à alteração de uma opção de plano, confira [Repositório de Consultas @Azure Blogs](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).  
  
 Ao identificar uma consulta com desempenho abaixo do ideal, sua ação dependerá da natureza do problema.  
  
-   Se a consulta foi executada com vários planos e o último plano é consideravelmente pior que o anterior, você pode usar o mecanismo de imposição de plano para forçar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a usar sempre o plano ideal para execuções futuras.  
  
     ![query-store-force-plan](../../relational-databases/performance/media/query-store-force-plan.png "query-store-force-plan")  

> [!NOTE]  
> O gráfico acima pode conter formas diferentes para planos de consulta específicos, com os seguintes significados para cada status possível:<br />  
> |Forma|Significado|  
> |-------------------|-------------|
> |Circle|Consulta Concluída (Execução Regular concluída com êxito)|
> |Square|Cancelado (Execução iniciada pelo cliente anulada)|
> |Triangle|Falha (Execução anulada pela exceção)|
> Além disso, o tamanho da forma reflete a contagem de execução de consulta dentro do intervalo de tempo especificado, aumentando de tamanho com um número maior de execuções.  

-   Você pode concluir que há um índice ausente na consulta, impedindo a execução ideal. Essas informações são expostas no plano de execução de consulta. Crie o índice ausente e verifique o desempenho da consulta usando o Repositório de Consultas.  
  
     ![query-store-show-plan](../../relational-databases/performance/media/query-store-show-plan.png "query-store-show-plan")  
  
     Se você executar sua carga de trabalho em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], inscreva-se no Index Advisor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] para receber automaticamente as recomendações de índice.  
  
-   Em alguns casos, você pode aplicar a recompilação de estatística se você vir que a diferença entre o número de linhas estimado e o real no plano de execução é significativa.  
  
-   Reescreva consultas problemáticas. Por exemplo, para obter todos os benefícios da parametrização de consulta ou para implementar mais lógica ideal.  
  
##  <a name="Verify"></a> Verificar se o Repositório de Consultas está coletando dados de consulta continuamente  
 O Repositório de Consultas pode alterar o modo de operação silenciosamente. Você deve monitorar regularmente o estado do Repositório de Consultas para garantir que o repositório de consultas esteja operando, e agir para evitar falhas devido a causas previsíveis. Execute a consulta a seguir para determinar o modo de operação e exibir os parâmetros mais relevantes:  
  
```sql
USE [QueryStoreDB];  
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason, interval_length_minutes,   
    stale_query_threshold_days, size_based_cleanup_mode_desc,   
    query_capture_mode_desc  
FROM sys.database_query_store_options;  
```  
  
 A diferença entre o `actual_state_desc` e `desired_state_desc` indica que uma alteração do modo de operação ocorreu automaticamente. A alteração mais comum é a alternância silenciosa do Repositório de Consultas para o modo somente leitura. Em circunstâncias muito raras, o Repositório de Consultas pode terminar no estado de ERRO devido a erros internos.  
  
 Quando o estado real for somente leitura, use a coluna **readonly_reason** para determinar a causa raiz. Normalmente, você descobrirá que o Repositório de Consultas realizou a transição para o modo somente leitura porque a cota de tamanho foi excedida. Nesse caso, **readonly_reason** é definida como 65536. Para outras razões, veja [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md).  
  
 Considere as etapas a seguir para realizar a transição do Repositório de Consultas para o modo de leitura-gravação e ativar a coleta de dados:  
  
-   Aumente o tamanho máximo de armazenamento usando a opção **MAX_STORAGE_SIZE_MB** de **ALTER DATABASE**.  
  
-   Limpe os dados do Repositório de Consultas usando a instrução a seguir:  
  
    ```sql  
    ALTER DATABASE [QueryStoreDB] SET QUERY_STORE CLEAR;  
    ```  
  
Você pode aplicar uma destas etapas ou ambas executando a seguinte instrução que altera explicitamente o modo de operação para leitura-gravação:  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);  
```  
  
 Execute as etapas a seguir para ser proativo:  
  
-   Você pode evitar alterações silenciosas do modo de operação aplicando as práticas recomendadas. Se você assegurar que o tamanho do Repositório de Consultas esteja sempre abaixo do valor máximo permitido, isso reduzirá drasticamente a chance de ocorrer transição para o modo somente leitura. Ative a política com base no tamanho conforme descrito na seção [Configurar Repositório de Consultas](#Configure) , para que o Repositório de Consultas limpe automaticamente os dados quando o tamanho se aproximar do limite.  
  
-   Para certificar-se de que os dados mais recentes sejam mantidos, configure a política com base em tempo para remover informações obsoletas regularmente.  
  
-   Por fim, considere definir o Modo de Captura de Consultas como Auto, já seu filtro desconsidera consultas que são geralmente menos relevantes para sua carga de trabalho.  
  
### <a name="error-state"></a>Estado de erro  
 Para recuperar o Repositório de Consultas, tente definir explicitamente o modo de leitura-gravação e verifique o estado real novamente.  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);    
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason, interval_length_minutes,   
    stale_query_threshold_days, size_based_cleanup_mode_desc,   
    query_capture_mode_desc  
FROM sys.database_query_store_options;  
```  
  
 Se o problema persistir, isso indicará corrupção dos dados do Repositório de Consultas que estão persistidos no disco.
 
 O Repositório de Consultas poderia ser recuperado executando o procedimento armazenado **sp_query_store_consistency_check** no banco de dados afetado.
 
 Se isso não ajudar, você poderá tentar limpar o Repositório de Consultas antes de solicitar o modo de leitura/gravação.  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE CLEAR;  
GO  
  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);    
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason, interval_length_minutes,   
    stale_query_threshold_days, size_based_cleanup_mode_desc,   
    query_capture_mode_desc  
FROM sys.database_query_store_options;  
```  
  
## <a name="set-the-optimal-query-capture-mode"></a>Definir o modo de captura de consulta ideal  
 Mantenha os dados mais relevantes no Repositório de Consultas. A tabela a seguir descreve os cenários típicos para cada Modo de Captura de Consulta:  
  
|Modo de Captura de Consulta|Cenário|  
|------------------------|--------------|  
|All|Analise sua carga de trabalho plenamente em termos de todas as formas de consultas, suas frequências de execução e outras estatísticas.<br /><br /> Identifique novas consultas na carga de trabalho.<br /><br /> Detecte se consultas ad hoc são usadas para identificar oportunidades de parametrização automática ou pelo usuário.|  
|Auto|Concentre sua atenção nas consultas relevantes e acionáveis; as consultas que são executadas regularmente ou que apresentam consumo significativo de recursos.|  
|None|Você já capturou o conjunto de consultas que deseja monitorar no tempo de execução e você deseja eliminar as distrações que outras consultas podem causar.<br /><br /> Nenhuma é adequado para teste e benchmark de ambientes.<br /><br /> Nenhuma também é adequado para fornecedores de software que entregam o Repositório de Consultas configurado para monitorar a sua carga de trabalho do aplicativo.<br /><br /> Nenhuma deve ser usada com cuidado, pois você poderá perder a oportunidade de acompanhar e otimizar consultas novas importantes. Evite usar Nenhuma, a menos que tenha um cenário específico que precise desse modo.|  
  
## <a name="keep-the-most-relevant-data-in-query-store"></a>Manter os dados mais relevantes no Repositório de Consultas  
 Configure o Repositório de Consultas para conter somente os dados relevantes e ele será executado continuamente, fornecendo uma ótima experiência de solução de problemas com um impacto mínimo sobre a sua carga de trabalho regular.  
A tabela a seguir fornece as práticas recomendadas:  
  
|Prática recomendada|Configuração|  
|-------------------|-------------|  
|Limite dados históricos retidos.|Configure a política com base em tempo para ativar a limpeza automática.|  
|Por filtragem, desconsidere consultas não relevantes.|Configure o Modo de Captura de Consulta como Auto.|  
|Exclua consultas menos relevantes quando o tamanho máximo for atingido.|Ative a política de limpeza com base em tamanho.|  
  
##  <a name="Parameterize"></a> Evite usar consultas não parametrizadas  
 O uso de consultas não parametrizadas, quando isso não é absolutamente necessário (por exemplo, em caso análise ad hoc), não é uma melhor prática.  Planos em cache não podem ser reutilizados, o que força o Otimizador de Consulta a compilar consultas para cada texto da consulta exclusivo. Para obter mais informações sobre este tópico, consulte [Diretrizes para uso da parametrização forçada](../../relational-databases/query-processing-architecture-guide.md#ForcedParamGuide).  
  Além disso, o Repositório de Consultas pode rapidamente exceder a cota de tamanho devido a um número potencialmente grande de textos da consulta diferentes e, consequentemente, um grande número de planos de execução diferentes com forma semelhante.  
Como resultado, o desempenho da carga de trabalho será abaixo do ideal e o Repositório de Consultas poderá alternar para o modo somente leitura ou excluir dados constantemente, tentando acompanhar as consultas em entrada.  
  
 Considere a as opções a seguir:  

  -   Parametrize consultas quando aplicável, por exemplo, encapsule consultas dentro de um procedimento armazenado ou sp_executesql. Para obter mais informações sobre este tópico, consulte [Reutilização de parâmetros e plano de execução](../../relational-databases/query-processing-architecture-guide.md#PlanReuse).    
  
-   Use a opção [**Otimizar para Cargas de Trabalho Ad Hoc**](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md) se sua carga de trabalho contiver muitos lotes ad hoc de uso único com planos de consulta diferentes.  
  
    -   Compare o número de valores query_hash distintos ao número total de entradas em sys.query_store_query. Se o índice estiver próximo de 1, a carga de trabalho ad hoc gerará consultas diferentes.  
  
-   Aplique [**parametrização forçada**](../../relational-databases/query-processing-architecture-guide.md#ForcedParam) ao banco de dados ou a um subconjunto de consultas se o número de planos de consulta diferentes não for grande.  
  
    -   Use o [guia de plano](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md) para forçar a parametrização somente para a consulta selecionada.  
  
    -   Configure a parametrização forçada como usando o comando [opção banco de dados de Parametrização](../../relational-databases/databases/database-properties-options-page.md#miscellaneous) se houver um número pequeno de planos de consulta diferentes na sua carga de trabalho: quando a proporção entre a contagem de query_hash distintos e o número total de entradas no sys.query_store_query for muito menor que 1.  
  
-   Defina o **Modo de Captura de Consulta** como AUTO para filtrar automaticamente, desconsiderando consultas ad hoc com consumo de recursos pequeno.  
  
##  <a name="Drop"></a> Evite um padrão de DROP e CREATE durante a manutenção de objetos recipientes para as consultas  
 O Repositório de Consultas associa a entrada da consulta com um objeto recipiente (procedimento armazenado, função e gatilho).  Ao recriar um objeto recipiente, uma nova entrada da consulta será gerada para o mesmo texto da consulta. Isso impedirá você de acompanhar estatísticas de desempenho para essa consulta ao longo do tempo e de usar o mecanismo de imposição de plano. Para evitar isso, use o processo `ALTER <object>` para alterar uma definição de objeto recipiente sempre que possível.  
  
##  <a name="CheckForced"></a> Verifique o status de Planos Forçados regularmente  

 A imposição de plano é um mecanismo prático para corrigir o desempenho das consultas críticas e torná-las mais previsíveis. No entanto, assim como ocorre com as dicas de plano e guias de plano, impor um plano não é uma garantia de que ele será usado em execuções futuras. Normalmente, quando o esquema de banco de dados é alterado de forma que os objetos referenciados pelo plano de execução são alterados ou removidos, a imposição de plano passará a falhar. Nesse caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] voltará à recompilação de consultas, enquanto o motivo real da falha da imposição será exposto em [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md). A consulta a seguir retorna informações sobre planos impostos:  
  
```sql  
USE [QueryStoreDB];  
GO  
  
SELECT p.plan_id, p.query_id, q.object_id as containing_object_id,  
    force_failure_count, last_force_failure_reason_desc  
FROM sys.query_store_plan AS p  
JOIN sys.query_store_query AS q on p.query_id = q.query_id  
WHERE is_forced_plan = 1;  
```  
  
 Para obter uma lista completa dos motivos, consulte [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md). Você também pode usar o XEvent **query_store_plan_forcing_failed** para acompanhar a solução de problemas de falhas de imposição de plano.  
  
##  <a name="Renaming"></a> Evite renomear bancos de dados se você tiver consultas com Planos Forçados  

 Planos de execução fazem referência a objetos usando nomes de três partes `database.schema.object`.   

Se você renomear um banco de dados, a imposição de plano falhará, causando recompilação em todas as execuções de consulta subsequentes.  

##  <a name="Recovery"></a> Use sinalizadores de rastreamento em servidores de missão crítica para melhorar a recuperação de desastre
 
  Os sinalizadores de rastreamento global 7745 e 7752 podem ser usados para melhorar o desempenho do Repositório de Consultas durante cenários de recuperação de desastres e alta disponibilidade. Para obter mais informações, consulte [Sinalizadores de rastreamento](../..//t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  O sinalizador de rastreamento 7745 impedirá o comportamento padrão em que o Repositório de Consultas grava dados em disco antes que o SQL Server possa ser desligado.
  
  O sinalizador de rastreamento 7752 habilita o carregamento assíncrono do Repositório de Consultas e também permite que o SQL Server execute consultas antes que o Repositório de Consultas seja totalmente carregado. O comportamento padrão do Repositório de Consultas impede que consultas sejam executadas antes que o Repositório de Consultas tenha sido recuperado.

## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do Repositório de Consultas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [Procedimentos armazenados do Repositório de Consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [Usar o Repositório de Consultas com OLTP na memória](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)   
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
 [Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md)  
  
