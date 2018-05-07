---
title: Compatibilidade com versões anteriores do SQL Server 2016 Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- installing Analysis Services, backward compatibility
- backward compatibility [Analysis Services]
- compatibility [Analysis Services]
- Analysis Services, backward compatibility
- upgrading Analysis Services
- SSAS, backward compatibility
- SQL Server Analysis Services, backward compatibility
ms.assetid: 618b6c3a-e20d-47a9-b2c6-6d848dfba05a
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bbd33812f2fe78fe50dfddc85c23bd24852b1035
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="analysis-services-backward-compatibility-sql-server-2016"></a>Compatibilidade com versões anteriores do Analysis Services (SQL Server 2016)
[!INCLUDE[ssas-appliesto-sql2016](../includes/ssas-appliesto-sql2016.md)]

Este artigo descreve as alterações na disponibilidade do recurso e comportamento entre a versão atual e a versão anterior.

## <a name="deprecated-features"></a>Recursos preteridos
Um *recurso preterido* será descontinuado do produto em uma versão futura, mas há ainda suporte e incluído na versão atual para manter a compatibilidade com versões anteriores. É recomendável que você pare de usar recursos preteridos em projetos novos e existentes para manter a compatibilidade com versões futuras.
  
Os recursos a seguir estão obsoletas nesta versão:
  
|||  
|-|-|  
|**Modo/categoria**|**Recurso**|  
|Multidimensional|Partições remotas|  
|Multidimensional|Grupos de medidas vinculados remotos|  
|Multidimensional|Write-back dimensional|  
|Multidimensional|Dimensões vinculadas|   
|Multidimensional|Notificações de tabela do SQL Server para o cache pró-ativo.  <br />A substituição é usar a sondagem para o cache pró-ativo. <br />Consulte [Cache pró-ativo &#40;Dimensões&#41;](../analysis-services/multidimensional-models-olap-logical-dimension-objects/proactive-caching-dimensions.md) e [Cache pró-ativo e &#40;Partições&#41;](../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).|  
|Multidimensional|Cubos de sessão. Não há nenhuma substituição.|  
|Multidimensional|Cubos locais. Não há substituições.|  
|Tabular|Os níveis de compatibilidade de modelo de tabela 1100 e 1103 não terão suporte em uma versão futura. A substituição é definir modelos de nível de compatibilidade 1200 ou superior, convertendo definições de modelo para metadados tabulares. Consulte [Nível de compatibilidade para modelos de tabela no Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).|  
|Ferramentas|SQL Server Profiler para captura de rastreamento<br /><br /> A substituição é usar o Extended Events Profiler interno no SQL Server Management Studio.  <br /> Consulte [Monitorar o Analysis Services com Eventos Estendidos do SQL Server](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)|  
|Ferramentas|Server Profiler para reprodução de rastreamento <br />Substituição. Não há nenhuma substituição.|  
|APIs Trace Management Objects e Trace|Objetos Microsoft.AnalysisServices.Trace (contêm as APIs para os objetos Analysis Services Trace e Replay). A substituição é composta por várias partes:<br /><br /> -Configuração de rastreamento: Microsoft.SqlServer.Management.XEvent<br />-Leitura de rastreamento: Microsoft.SqlServer.XEvent.Linq<br />-   Reprodução de rastreamento: nenhuma|  
  
> [!NOTE]  
>  Os anúncios anteriores de recursos preteridos do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] permanecem em vigor. Como o código de suporte a esses recursos ainda não foi retirado do produto, muitos desses recursos ainda estão presentes nesta versão. Enquanto os recursos anteriormente preteridos possam ser acessados, que eles ainda são considerados preteridos e podem ser fisicamente removidos do produto a qualquer momento.  

## <a name="discontinued-features"></a>Recursos descontinuados
Um *recurso Descontinuado* foi substituído em uma versão anterior. Ele pode continuar a ser incluído na versão atual, mas não é mais suportado. Recursos descontinuados podem ser removidos inteiramente em um futuro versão ou atualizar.

Os recursos a seguir foram preteridos em uma versão anterior e não têm mais suporte nesta versão.

|||  
|-|-|  
|**Recurso**|**Substituição ou solução alternativa**|  
|[CalculationPassValue &#40;MDX&#41;](../mdx/calculationpassvalue-mdx.md)|Nenhuma. Esse recurso foi preterido no SQL Server 2005.|  
|[CalculationCurrentPass &#40;MDX&#41;](../mdx/calculationcurrentpass-mdx.md)|Nenhuma. Esse recurso foi preterido no SQL Server 2005.|  
|Dica do otimizador de consulta NON_EMPTY_BEHAVIOR|Nenhuma. Esse recurso foi preterido no SQL Server 2008.|  
|Assemblies COM|Nenhuma. Esse recurso foi preterido no SQL Server 2008.|  
|Propriedade de célula intrínseca CELL_EVALUATION_LIST|Nenhuma. Esse recurso foi preterido no SQL Server 2005.|  
  
> [!NOTE]  
>  Os anúncios anteriores de recursos preteridos do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] permanecem em vigor. Como o código de suporte a esses recursos ainda não foi retirado do produto, muitos desses recursos ainda estão presentes nesta versão. Enquanto os recursos anteriormente preteridos possam ser acessados, que eles ainda são considerados preteridos e podem ser fisicamente removidos do produto a qualquer momento.  

## <a name="breaking-changes"></a>Alterações mais recentes
Um *alteração interruptiva* faz com que um modelo de dados, código do aplicativo ou script não funcionem depois de atualizar o modelo ou o servidor.
  
### <a name="net-40-version-upgrade"></a>Atualização de Versão do .NET 4.0  
 Bibliotecas de cliente do Analysis Services Management Objects (AMO), o ADOMD.NET e o modelo de objeto de tabela (TOM) agora voltados para o tempo de execução do .NET 4.0. Isso pode ser uma alteração interruptiva para aplicativos destinados ao .NET 3.5. Aplicativos que usam versões mais recentes desses assemblies agora devem ser voltados para o .NET 4.0 ou posterior.  
  
### <a name="amo-version-upgrade"></a>Atualização de Versão do AMO  
 Esta versão é uma atualização de versão para [objetos de gerenciamento do Analysis Services &#40;AMO&#41; ](https://msdn.microsoft.com/library/mt436122.aspx) e é uma alteração significativa em determinadas circunstâncias.  O código e os scripts existentes que chamam o AMO continuarão a ser executados como antes se você efetuar a atualização a partir de uma versão anterior. No entanto, se você precisar *recompilar* seu aplicativo e você tiver como alvo uma instância do SQL Server 2016 Analysis Services, você deve adicionar o namespace a seguir para tornar o seu código ou script operacional:  
  
```  
  
using Microsoft.AnalysisServices;  
using Microsoft.AnalysisServices.Core;  
  
```  
  
 O namespace [Microsoft.AnalysisServices.Core](https://msdn.microsoft.com/library/microsoft.analysisservices.core.aspx) agora é necessário sempre que a referenciar o assembly Microsoft. AnalysisServices em seu código. Objetos que estiveram anteriormente apenas no namespace do **Microsoft.AnalysisServices** são movidos para o namespace principal nesta versão, se o objeto for usado em cenários de tabela e cenários multidimensionais da mesma maneira.  Por exemplo, as APIs de servidor são realocadas para o namespace principal.  
  
 Apesar de agora haver vários namespaces, eles existem no mesmo assembly (Microsoft.AnalysisServices.dll).  
  
### <a name="xevent-discover-changes"></a>Alterações de XEvent DISCOVER  
 Para oferecer um melhor suporte XEvent DESCOBRIR streaming no SSMS para SQL Server 2016 Analysis Services, `DISCOVER_XEVENT_TRACE_DEFINITION` é substituído com os rastreamentos XEvent seguintes:  
  
-   DISCOVER_XEVENT_PACKAGES  
  
-   DISCOVER_XEVENT_OBJECT  
  
-   DISCOVER_XEVENT_OBJECT_COLUMNS  
  
-   DISCOVER_XEVENT_SESSION_TARGETS  

## <a name="behavior-changes"></a>Alterações de comportamento
Uma *alteração de comportamento* afeta a maneira como os recursos funcionam ou interagem na versão atual em comparação com as versões anteriores do SQL Server.
  
Revisões de valores padrão, a configuração manual necessária para concluir uma atualização ou restaurar a funcionalidade, ou então uma nova implementação de um recurso existente são exemplos de uma alteração de comportamento no produto.
  
Os comportamentos de recursos alterados nesta versão, mas que não interrompem um modelo ou código existente após a atualização, estão listados aqui.
  
### <a name="analysis-services-in-sharepoint-mode"></a>Analysis Services no modo do SharePoint
 Não é mais necessário executar o assistente de Configuração do Power Pivot como uma tarefa pós-instalação. Isso é verdadeiro para todas as versões com suporte do SharePoint que carregar modelos do SQL Server 2016 Analysis Services atual.
  
### <a name="directquery-mode-for-tabular-models"></a>Modo DirectQuery para modelos de tabela
 *DirectQuery* é um modo de acesso a dados para modelos de tabela, em que a execução da consulta é executada em um banco de dados relacional de back-end, recuperando um conjunto de resultados em tempo real. Ele geralmente é usado para grandes conjuntos de dados que não cabem na memória ou quando dados são voláteis e você deseja os dados mais recentes retornados em consultas a um modelo de tabela.
  
 O DirectQuery já existe como um modo de acesso a dados em várias versões mais recentes. No SQL Server 2016 Analysis Services, a implementação foi ligeiramente revisada, supondo que o modelo de tabela no nível de compatibilidade 1200 ou superior. DirectQuery tem menos restrições do que antes. Ele também tem propriedades de banco de dados diferentes.
  
 Se você estiver usando DirectQuery em um modelo de tabela existente, você poderá manter o modelo em seu nível de compatibilidade atual, 1100 ou 1103, e continuar a usar o DirectQuery, já que ele está implementado para esses níveis. Como alternativa, você pode atualizar para 1200 ou superior para se beneficiar de aprimoramentos feitos ao DirectQuery.
  
 Não há nenhuma atualização in-loco de um modelo DirectQuery porque as configurações de níveis de compatibilidade mais antigos não têm contrapartes exatas nos níveis de compatibilidade 1200 e maior mais recentes. Se você tiver um modelo tabular existente que é executado no modo DirectQuery, você deve abrir o modelo no SQL Server Data Tools, desativar o DirectQuery, defina o **nível de compatibilidade** propriedade para 1200 ou superior e, em seguida, reconfigure o DirectQuery Propriedades. Consulte [o modo DirectQuery](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md) para obter detalhes.


## <a name="see-also"></a>Consulte também
[Compatibilidade com versões anteriores do Analysis Services (SQL Server 2017)](analysis-services-backward-compatibility-sql2017.md)
