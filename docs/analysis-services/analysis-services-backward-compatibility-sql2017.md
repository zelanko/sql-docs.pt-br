---
title: Compatibilidade com versões anteriores do SQL Server 2017 Analysis Services | Microsoft Docs
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: e7903de787a1b63627bca8da23369fbee9014c6e
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685733"
---
# <a name="analysis-services-backward-compatibility-sql-2017"></a>Compatibilidade com versões anteriores do Analysis Services (2017 do SQL)
[!INCLUDE[ssas-appliesto-sql2017](../includes/ssas-appliesto-sql2017.md)]

Este artigo descreve as alterações na disponibilidade de recursos e o comportamento entre a versão atual e a versão anterior.

## <a name="deprecated-features"></a>Recursos preteridos
Um *recurso preterido* será descontinuado do produto em uma versão futura, mas é ainda tem suporte e incluído na versão atual para manter a compatibilidade com versões anteriores. Recomenda-se que você interromper o uso de recursos preteridos em projetos novos e existentes para manter a compatibilidade com versões futuras. Documentação não é atualizada para recursos preteridos.

Os seguintes recursos foram preteridos nessa versão:
  
|||  
|-|-|  
|**Modo/categoria**|**Recurso**|
|Multidimensional|Mineração de dados|
|Multidimensional|Grupos de medidas vinculados remotos|
|Tabular|Modelos no nível de compatibilidade 1100 e 1103|
|Tabular|Propriedades do modelo de objeto tabulares: Column.TableDetailPosition, Column.IsDefaultLabel, Column.IsDefaultImage|
|Ferramentas|SQL Server Profiler para captura de rastreamento<br /><br /> A substituição é usar o Extended Events Profiler interno no SQL Server Management Studio.  <br /> Consulte [Monitor Analysis Services with SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md).|  
|Ferramentas|Server Profiler para reprodução de rastreamento <br />Substituição. Não há nenhuma substituição.|  
|APIs Trace Management Objects e Trace|Objetos Microsoft.AnalysisServices.Trace (contêm as APIs para os objetos Analysis Services Trace e Replay). A substituição é composta por várias partes:<br /><br /> -Configuração de rastreamento: Microsoft.SqlServer.Management.XEvent<br />-Leitura de rastreamento: Microsoft.SqlServer.XEvent.Linq<br />-Reprodução de rastreamento: None|  


## <a name="discontinued-features"></a>Recursos descontinuados
Um *recurso Descontinuado* foi preterido em uma versão anterior. Ele pode continuar a ser incluído na versão atual, mas não é mais suportado. Recursos descontinuados podem ser removidos inteiramente em uma futura versão ou atualizar.

Os seguintes recursos foram preteridos em uma versão anterior e não têm mais suporte nesta versão.
  
|||  
|-|-|  
|**Modo/categoria**|**Recurso**|  
|Tabular|Valor da propriedade VertipaqPagingPolicy memória (2), habilitar paginação para o disco usando memória mapeada arquivos.|
|Multidimensional|Partições remotas|  
|Multidimensional|Grupos de medidas vinculados remotos|  
|Multidimensional|Write-back dimensional|  
|Multidimensional|Dimensões vinculadas|


## <a name="breaking-changes"></a>Alterações significativas
Um *alteração significativa* faz com que um recurso, o modelo de dados, o código do aplicativo ou o script não funcionem depois de atualizar para a versão atual.

Não há nenhuma alteração significativa nesta versão.

## <a name="behavior-changes"></a>Alterações de comportamento
Um *alteração de comportamento* afeta como o mesmo recurso funciona na versão atual em comparação com a versão anterior. Somente as alterações de comportamento significativo são descritas. Alterações na interface do usuário não são incluídas.

Alterações em MDSCHEMA_MEASUREGROUP_DIMENSIONS e DISCOVER_CALC_DEPENDENCY, detalhado na [o que há de novo no SQL Server 2017 CTP 2.1 para o Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2017/05/18/whats-new-in-sql-server-2017-ctp-2-1-for-analysis-services/) comunicado.


## <a name="see-also"></a>Confira também
[Compatibilidade com versões anteriores do Analysis Services (SQL Server 2016)](analysis-services-backward-compatibility.md)
