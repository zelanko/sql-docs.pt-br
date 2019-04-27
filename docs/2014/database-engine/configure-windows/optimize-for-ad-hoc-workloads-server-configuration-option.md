---
title: Opção de configuração de servidor optimize for ad hoc workloads | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- optimize for ad hoc workloads option
ms.assetid: 0972e028-3a8e-454b-a186-e814a1d431f2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7edf279b49374823c9083005be9b8d047b003f62
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62781432"
---
# <a name="optimize-for-ad-hoc-workloads-server-configuration-option"></a>Opção de configuração de servidor optimize for ad hoc workloads
  A opção **otimizar para cargas de trabalho ad hoc** é usada para aperfeiçoar a eficiência do cache de planos para cargas de trabalho que contêm muitos lotes ad hoc de uso exclusivo. Quando essa opção está definida como 1, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] armazena um pequeno stub de plano compilado no cache de planos quando um lote é compilado pela primeira vez, em vez do plano compilado completo. Isso ajuda a aliviar a pressão sobre a memória não permitindo que o cache de planos fique cheio de planos compilados que não serão reutilizados.  
  
 O stub de plano compilado permite que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] reconheça que esse lote ad hoc foi compilado antes, mas somente armazenou um stub de plano compilado, portanto, quando esse lote é invocado (compilado ou executado) novamente, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] compila o lote, remove o stub de plano compilado do cache de planos e adiciona o plano compilado completo ao cache de planos.  
  
 Configurar a opção **otimizar para cargas de trabalho ad hoc** como 1 afeta apenas os planos novos; os planos que já estão no cache de planos não são afetados.  
  
 O stub de plano compilado é um dos cacheobjtypes exibidos pela exibição de catálogo sys.dm_exec_cached_plans. Ele tem identificadores sql e de plano exclusivos. O stub de plano compilado não tem um plano de execução associado a ele e a consulta do identificador do plano não retornará um Showplan XML.  
  
 O sinalizador de rastreamento 8032 reverte os parâmetros de limite de cache para a configuração do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] RTM, que, em geral, permite que os caches sejam maiores. Use esta configuração quando entradas de cache reutilizadas com frequência não se ajustarem no cache e quando o *optimize for ad hoc workloads Server Configuration Option* não tiver resolvido o problema com o cache do plano.  
  
> [!WARNING]  
>  O sinalizador de rastreamento 8032 pode causar baixo desempenho se os caches grandes deixarem menos memória disponível para outros consumidores de memória, como o pool de buffers.  
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
