---
title: Analisar consultas com Resultados do SHOWPLAN
titleSuffix: SQL Server Profiler
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 6a2f7727-141c-4f59-8613-2e452bc78467
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: e0936a3931b574c08e5a58f396d7917eae569078
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75307381"
---
# <a name="analyze-queries-with-showplan-results-in-sql-server-profiler"></a>Analisar consultas com resultados do Plano de Execução no SQL Server Profiler

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Você pode adicionar classes de eventos de Plano de Execução a uma definição de rastreamento para fazer com que o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] reúna e exiba informações do plano de consulta no rastreamento. Também é possível extrair eventos de Plano de Execução de outros eventos coletados no rastreamento e salvá-los em um arquivo XML separado.  
  
 Pode-se extrair eventos de Plano de Execução do rastreamento de uma das seguintes maneiras:  
  
-   No momento da configuração do rastreamento, usando a guia **Configurações de Extração de Eventos** . Observe que essa guia não aparece a menos que você selecione um dos eventos de Plano de Execução na guia **Seleção de Eventos** .  
  
-   Usando a opção **Extrair Eventos do SQL Server** no menu **Arquivo** .  
  
-   Extraindo e salvando eventos individuais, clicando com o botão direito do mouse em um evento específico e escolhendo **Extrair Dados de Eventos**.  
  
## <a name="showplan-events"></a>Eventos de Plano de Execução  
 Os eventos de rastreamento de Plano de Execução são listados e descritos na tabela a seguir.  
  
|Nome do evento|Descrição|  
|----------------|-----------------|  
|**Performance statistics**|Indica a primeira vez em que um Plano de Execução compilado é colocado em cache, quando é recompilado e quando é descartado do cache do plano. A coluna **TextData** contém o Plano de Execução em formato XML. Para obter mais informações, veja [Classe de evento Performance Statistics](../../relational-databases/event-classes/performance-statistics-event-class.md).|  
|**Showplan All**|Exibe o plano de consulta com detalhes completos da compilação da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] executada. Por exemplo, pode exibir estimativas de preço de custo e listas de colunas. Para obter mais informações, consulte [Showplan All Event Class](../../relational-databases/event-classes/showplan-all-event-class.md).|  
|**Showplan All For Query Compile**|Ocorre quando uma consulta é compilada ou recompilada em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta é a contraparte de tempo de compilação do evento **Showplan All** . **Showplan All** ocorre quando uma consulta é executada. O**Showplan All For Query Compile** ocorre quando uma consulta é compilada. Para obter mais informações, consulte [Showplan All for Query Compile Event Class](../../relational-databases/event-classes/showplan-all-for-query-compile-event-class.md).|  
|**Showplan Statistics Profile**|Exibe o plano de consulta com detalhes completos do tempo de execução da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que está sendo executada, inclusive o número real de linhas que passam em cada operação. Para obter mais informações, consulte [Showplan Statistics Profile Event Class](../../relational-databases/event-classes/showplan-statistics-profile-event-class.md).|  
|**Showplan Text**|Exibe a árvore do plano de consulta da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que está sendo executada como dados binários. Para obter mais informações, consulte [Showplan Text Event Class](../../relational-databases/event-classes/showplan-text-event-class.md).|  
|**Showplan Text (Unencoded)**|Exibe a árvore do plano de consulta da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que está sendo executada como texto. Essa classe de evento exibe as mesmas informações que Showplan Text, exibindo-as, porém, como texto, e não como dados binários. Para obter mais informações, veja [Classe de evento Showplan Text &#40;Não codificada&#41;](../../relational-databases/event-classes/showplan-text-unencoded-event-class.md).|  
|**Showplan XML**|Exibe o plano de consulta com os dados completos coletados durante a otimização de consulta. Esse evento só é gerado quando um plano de consulta é otimizado. Para obter mais informações, consulte [Showplan XML Event Class](../../relational-databases/event-classes/showplan-xml-event-class.md).|  
|**Showplan XML For Query Compile**|Exibe o plano de consulta quando a consulta é compilada. Para obter mais informações, consulte [Showplan XML for Query Compile Event Class](../../relational-databases/event-classes/showplan-xml-for-query-compile-event-class.md).|  
|**Showplan XML Statistics Profile**|Exibe o plano de consulta com detalhes completos do tempo de execução em formato XML. Por exemplo, essa classe de evento captura o número de linhas que passam em cada operador da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que está sendo executada. Para obter mais informações, consulte [Showplan XML Statistics Profile Event Class](../../relational-databases/event-classes/showplan-xml-statistics-profile-event-class.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Categoria de evento Performance](../../relational-databases/event-classes/performance-event-category.md)  
  
  
