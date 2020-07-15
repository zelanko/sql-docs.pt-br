---
title: Opção de configuração de servidor optimize for ad hoc workloads | Microsoft Docs
description: Saiba mais sobre a opção "optimize for ad hoc workloads". Use-a para aprimorar a eficiência do cache de planos do SQL Server quando as cargas de trabalho contiverem muitos lotes ad hoc de uso único.
ms.custom: ''
ms.date: 11/17/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- optimize for ad hoc workloads option
ms.assetid: 0972e028-3a8e-454b-a186-e814a1d431f2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d93df848459f003fa4e2c2be0b88ddd9973422c5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85781858"
---
# <a name="optimize-for-ad-hoc-workloads-server-configuration-option"></a>Opção de configuração de servidor optimize for ad hoc workloads
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A opção **otimizar para cargas de trabalho ad hoc** é usada para aperfeiçoar a eficiência do cache de planos para cargas de trabalho que contêm muitos lotes ad hoc de uso exclusivo. Quando essa opção está definida como 1, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] armazena um pequeno stub de plano compilado no cache de planos quando um lote é compilado pela primeira vez, em vez do plano compilado completo. Isso ajuda a aliviar a pressão sobre a memória não permitindo que o cache de planos fique cheio de planos compilados que não serão reutilizados. 
  
  O stub de plano compilado permite que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] reconheça que esse lote ad hoc foi compilado antes, mas somente armazenou um stub de plano compilado, portanto, quando esse lote é invocado (compilado ou executado) novamente, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] compila o lote, remove o stub de plano compilado do cache de planos e adiciona o plano compilado completo ao cache de planos. 
  
 O stub de plano compilado é um dos cacheobjtypes exibidos pela exibição de catálogo sys.dm_exec_cached_plans. Ele tem identificadores sql e de plano exclusivos. O stub de plano compilado não tem um plano de execução associado a ele e a consulta do identificador do plano não retornará um Showplan XML.  
  
 O [sinalizador de rastreamento 8032](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) reverte os parâmetros de limite de cache para a configuração do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] RTM, que, em geral, permite que os caches sejam maiores. Use esta configuração quando entradas de cache reutilizadas com frequência não se ajustarem no cache e quando a opção de configuração do servidor de otimizar para cargas de trabalho ad hoc não tiver resolvido o problema com o cache do plano.  
  
> [!WARNING]  
>  O sinalizador de rastreamento 8032 pode causar baixo desempenho se os caches grandes deixarem menos memória disponível para outros consumidores de memória, como o pool de buffers.  

## <a name="recommendations"></a>Recomendações
Evite ter um grande número de planos de uso único no cache de planos. Uma causa comum desse problema é quando os tipos de dados de parâmetros de consulta não estão definidos de maneira consistente. Particularmente, isso se aplica ao comprimento de cadeias de caracteres, mas pode se aplicar a qualquer tipo de dados que tenha um maxlength, uma precisão ou uma escala. Por exemplo, se um parâmetro chamado @Greeting for passado como um nvarchar(10) em uma chamada e um nvarchar(20) na próxima chamada, serão criados planos separados para cada tamanho de parâmetro. Se uma consulta tiver vários parâmetros e eles não estiverem consistentemente definidos quando chamados, poderá existir um grande número de planos de consulta para cada consulta. Os planos poderiam existir para cada combinação de tipos de dados de parâmetro de consulta e comprimentos que foram usados.

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
  
  
