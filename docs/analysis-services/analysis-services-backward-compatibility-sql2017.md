---
title: "Compatibilidade com versões anteriores do SQL Server de 2017 Analysis Services | Microsoft Docs"
ms.date: 07/11/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing Analysis Services, backward compatibility
- backward compatibility [Analysis Services]
- compatibility [Analysis Services]
- Analysis Services, backward compatibility
- upgrading Analysis Services
- SSAS, backward compatibility
- SQL Server Analysis Services, backward compatibility
ms.assetid: 
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 972ab981eccb6271dfa2f18e0b482f43020ff36b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="analysis-services-backward-compatibility-sql-2017"></a>Compatibilidade com versões anteriores do Analysis Services (SQL 2017)
[!INCLUDE[ssas-appliesto-sql2017](../includes/ssas-appliesto-sql2017.md)]

Este artigo descreve as alterações na disponibilidade do recurso e comportamento entre a versão atual e a versão anterior.

## <a name="deprecated-features"></a>Recursos preteridos
Um *recurso preterido* será descontinuado do produto em uma versão futura, mas há ainda suporte e incluído na versão atual para manter a compatibilidade com versões anteriores. É recomendável que você pare de usar recursos preteridos em projetos novos e existentes para manter a compatibilidade com versões futuras.

Os recursos a seguir estão obsoletas nesta versão:
  
|||  
|-|-|  
|**Modo/categoria**|**Recurso**|
|Tabular|Grupos de medidas vinculados remotos|
|Tabular|Modelos no nível de compatibilidade 1100 e 1103|
|Tabular|Propriedades do modelo de objeto de tabela: Column.TableDetailPosition, Column.IsDefaultLabel, Column.IsDefaultImage|
|Multidimensional|Mineração de dados|

## <a name="discontinued-features"></a>Recursos descontinuados
Um *recurso Descontinuado* foi substituído em uma versão anterior. Ele pode continuar a ser incluído na versão atual, mas não é mais suportado. Recursos descontinuados podem ser removidos inteiramente em um futuro versão ou atualizar.

Os recursos a seguir foram preteridos em uma versão anterior e não têm mais suporte nesta versão.
  
|||  
|-|-|  
|**Modo/categoria**|**Recurso**|  
|Tabular|Valor da propriedade VertipaqPagingPolicy memória (2), habilitar paginação em disco usando memória mapeada arquivos.|
|Multidimensional|Partições remotas|  
|Multidimensional|Grupos de medidas vinculados remotos|  
|Multidimensional|Write-back dimensional|  
|Multidimensional|Dimensões vinculadas|
|Ferramentas|SQL Server Profiler para captura de rastreamento<br /><br /> A substituição é usar o Extended Events Profiler interno no SQL Server Management Studio.  <br /> Consulte [Monitor Analysis Services with SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md).|  
|Ferramentas|Server Profiler para reprodução de rastreamento <br />Substituição. Não há nenhuma substituição.|  
|APIs Trace Management Objects e Trace|Objetos Microsoft.AnalysisServices.Trace (contêm as APIs para os objetos Analysis Services Trace e Replay). A substituição é composta por várias partes:<br /><br /> -   Configuração de rastreamento: Microsoft.SqlServer.Management.XEvent<br />-   Leitura de rastreamento: Microsoft.SqlServer.XEvent.Linq<br />-   Reprodução de rastreamento: nenhuma|  

## <a name="breaking-changes"></a>Alterações mais recentes
Um *alteração significativa* faz com que um recurso, o modelo de dados, o código do aplicativo ou script não funcionem depois de atualizar para a versão atual.

Não há nenhuma alteração de quebra nesta versão.

## <a name="behavior-changes"></a>Alterações de comportamento
Um *alteração de comportamento* afeta como o mesmo recurso funciona na versão atual em comparação com a versão anterior. Somente as alterações de comportamento significativa descritas. Alterações na interface do usuário não são incluídas.

Não há nenhuma alteração de comportamento nesta versão.


## <a name="see-also"></a>Consulte também
[Compatibilidade com versões anteriores do Analysis Services (SQL Server 2016)](analysis-services-backward-compatibility.md)
