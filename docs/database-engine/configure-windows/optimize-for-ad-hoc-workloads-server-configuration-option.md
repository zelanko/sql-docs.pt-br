---
title: "Opção de configuração de servidor optimize for ad hoc workloads | Microsoft Docs"
ms.custom: 
ms.date: 11/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: optimize for ad hoc workloads option
ms.assetid: 0972e028-3a8e-454b-a186-e814a1d431f2
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 96e21a0eb32b9aeecabdfeb574d3e793b3ab99d8
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="optimize-for-ad-hoc-workloads-server-configuration-option"></a>Opção de configuração de servidor optimize for ad hoc workloads
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  A opção **otimizar para cargas de trabalho ad hoc** é usada para aperfeiçoar a eficiência do cache de planos para cargas de trabalho que contêm muitos lotes ad hoc de uso exclusivo. Quando essa opção está definida como 1, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] armazena um pequeno stub de plano compilado no cache de planos quando um lote é compilado pela primeira vez, em vez do plano compilado completo. Isso ajuda a aliviar a pressão sobre a memória não permitindo que o cache de planos fique cheio de planos compilados que não serão reutilizados.  
  
 O stub de plano compilado permite que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] reconheça que esse lote ad hoc foi compilado antes, mas somente armazenou um stub de plano compilado, portanto, quando esse lote é invocado (compilado ou executado) novamente, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] compila o lote, remove o stub de plano compilado do cache de planos e adiciona o plano compilado completo ao cache de planos. 
  
 O stub de plano compilado é um dos cacheobjtypes exibidos pela exibição de catálogo sys.dm_exec_cached_plans. Ele tem identificadores sql e de plano exclusivos. O stub de plano compilado não tem um plano de execução associado a ele e a consulta do identificador do plano não retornará um Showplan XML.  
  
 O [sinalizador de rastreamento 8032](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) reverte os parâmetros de limite de cache para a configuração do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] RTM, que, em geral, permite que os caches sejam maiores. Use esta configuração quando entradas de cache reutilizadas com frequência não se ajustarem no cache e quando a opção de configuração do servidor de otimizar para cargas de trabalho ad hoc não tiver resolvido o problema com o cache do plano.  
  
> [!WARNING]  
>  O sinalizador de rastreamento 8032 pode causar baixo desempenho se os caches grandes deixarem menos memória disponível para outros consumidores de memória, como o pool de buffers.  

## <a name="recommendations"></a>Recomendações
Se o número de planos de uso único usar uma parte significativa da memória do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] em um servidor OLTP e esses planos são Ad-hoc, use esta opção de servidor para diminuir o uso de memória com esses objetos.
Para localizar o número de planos de uso único armazenados em cache, execute a seguinte consulta:

```sql
SELECT objtype, cacheobjtype, 
  AVG(usecounts) AS Avg_UseCount, 
  SUM(refcounts) AS AllRefObjects, 
  SUM(CAST(size_in_bytes AS bigint))/1024/1024 AS Size_MB
FROM sys.dm_exec_cached_plans
WHERE objtype = 'Adhoc' AND usecounts = 1
GROUP BY objtype, cacheobjtype;
```

> [!IMPORTANT]
> Configurar a opção **otimizar para cargas de trabalho ad hoc** como 1 afeta apenas os planos novos; os planos que já estão no cache de planos não são afetados.
> Para afetar planos de consulta já armazenados em cache imediatamente, o cache do plano precisa ser limpo usando [ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) ou então [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisa reiniciar.

## <a name="see-also"></a>Consulte Também  
 [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
