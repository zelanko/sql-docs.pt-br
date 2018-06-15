---
title: Recursos compatíveis com as edições do SQL Server 2016 do Analysis Services | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 19618fc0311de28184e3a95c5e57e423d121f085
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34015563"
---
# <a name="analysis-services-features-supported-by-sql-server-editions"></a>Recursos do Analysis Services com suporte nas edições do SQL Server
[!INCLUDE[ssas-appliesto-sql2016-later](../includes/ssas-appliesto-sql2016-later.md)]

Este tópico fornece detalhes de recursos com suporte nas diferentes edições do SQL Server 2016 Analysis Services. Para os recursos com suporte nas edições Evaluation e Developer, consulte Enterprise edition.

## <a name="analysis-services-servers"></a>Analysis Services (servidores)
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Desenvolvedor|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Bancos de dados compartilhados escalonáveis|Sim||||||Sim|  
|Fazer backup/Restaurar e Anexar/Desanexar bancos de dados|Sim|Sim|||||Sim|  
|Sincronizar bancos de dados|Sim||||||Sim|  
|Instâncias do cluster de failover do AlwaysOn|Sim<br /><br /> O número de nós é o máximo do sistema operacional|Sim<br /><br /> Suporte para 2 nós|||||Sim<br /><br /> O número de nós é o máximo do sistema operacional|  
|Programação (AMO, ADOMD.Net, OLEDB, XML/A, ASSL, TMSL)|Sim|Sim|||||Sim|  
  
## <a name="tabular-models"></a>Modelos de tabela 
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Desenvolvedor|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Hierarquias|Sim|Sim|||||Sim|  
|KPIs|Sim|Sim|||||Sim|  
|Perspectivas|Sim||||||Sim|  
|Traduções|Sim|Sim|||||Sim|  
|Cálculos DAX, consultas DAX, consultas MDX|Sim|Sim|||||Sim|  
|Segurança em nível de linha|Sim|Sim|||||Sim|  
|Várias partições|Sim||||||Sim|  
|Modo de armazenamento na memória|Sim|Sim|||||Sim|  
|Modo de armazenamento do DirectQuery|Sim||||||Sim|  

## <a name="multidimensional-models"></a>Modelos multidimensionais 
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Desenvolvedor|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Medidas semiaditivas|Sim|Não <sup>1</sup>|||||Sim|  
|Hierarquias|Sim|Sim|||||Sim|  
|KPIs|Sim|Sim|||||Sim|  
|Perspectivas|Sim||||||Sim|  
|Ações|Sim|Sim|||||Sim|  
|Inteligência de conta|Sim|Sim|||||Sim|  
|Inteligência de dados temporais|Sim|Sim|||||Sim|  
|Rollups personalizados|Sim|Sim|||||Sim|  
|Cubo de write-backs|Sim|Sim|||||Sim|  
|Dimensões de write-back|Sim||||||Sim|  
|Células de Writeback|Sim|Sim|||||Sim|  
|Detalhamento|Sim|Sim|||||Sim|  
|Tipos de hierarquia avançados (pai-filho e hierarquias desbalanceadas)|Sim|Sim|||||Sim|  
|Dimensões avançadas (Dimensões de referência, dimensões muitos-para-muitos)|Sim|Sim|||||Sim|  
|Medidas e dimensões vinculadas|Sim|Sim  <sup>2</sup> |||||Sim|  
|Traduções|Sim|Sim|||||Sim|  
|Agregações|Sim|Sim|||||Sim|  
|Várias partições|Sim|Sim, até 3|||||Sim|  
|Cache pró-ativo|Sim||||||Sim|  
|Assemblies personalizados (procedimentos armazenados)|Sim|Sim|||||Sim|  
|Consultas MDX e scripts|Sim|Sim|||||Sim|  
|Consultas DAX|Sim|Sim|||||Sim|  
|Modelo de segurança com base em função|Sim|Sim|||||Sim|  
|Segurança no nível da dimensão e da célula|Sim|Sim|||||Sim|  
|Armazenamento de cadeias de caracteres escalonável|Sim|Sim|||||Sim|  
|Modelos de armazenamento MOLAP, ROLAP e HOLAP|Sim|Sim|||||Sim|  
|Transporte de XML binário e compactado|Sim|Sim|||||Sim|  
|Processamento de modo push|Sim||||||Sim|  
|Write-back direto|Sim||||||Sim|  
|Expressões de medida|Sim||||||Sim|  
  
 <sup>1</sup> Há suporte para a medida semiaditiva LastChild na edição Standard, ao contrário de outras medidas semiaditivas, como None, FirstChild, FirstNonEmpty, LastNonEmpty, AverageOfChildren e ByAccount. Medidas aditivas, como Sum, Count, Min, Max e medidas não aditivas (DistinctCount) têm suporte em todas as edições.  
  <sup>2</sup> standard edition oferece suporte a vinculação de medidas e dimensões no mesmo banco de dados, mas não de outros bancos de dados ou instâncias.
  
## <a name="power-pivot-for-sharepoint"></a>Power Pivot para SharePoint  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Desenvolvedor|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Integração de farm do SharePoint baseado em arquitetura de serviço compartilhado|Sim||||||Sim|  
|Relatórios de uso|Sim||||||Sim|  
|Regras de monitoramento de integridade|Sim||||||Sim|  
|Galeria do Power Pivot|Sim||||||Sim|  
|Atualização de dados do Power Pivot|Sim||||||Sim|  
|Feeds de dados do Power Pivot|Sim||||||Sim|  
  
## <a name="data-mining"></a>Mineração de dados  
  
|Nome do recurso|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Desenvolvedor|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Algoritmos padrão|Sim|Sim|||||Sim|  
|Ferramentas de mineração de dados (Assistentes, Editores, Construtores de Consultas)|Sim|Sim|||||Sim|  
|Validação cruzada|Sim||||||Sim|  
|Modelos em subconjuntos filtrados de dados da estrutura de mineração|Sim||||||Sim|  
|Série temporal: combinação personalizada entre métodos ARTXP e ARIMA|Sim||||||Sim|  
|Série temporal: previsão com novos dados|Sim||||||Sim|  
|Consultas de DM simultâneas ilimitadas|Sim||||||Sim|  
|Configuração avançada e opções de ajuste para algoritmos de mineração de dados|Sim||||||Sim|  
|Suporte para algoritmos de plug-in|Sim||||||Sim|  
|Processamento paralelo de modelo|Sim||||||Sim|  
|Série temporal: previsão de séries cruzadas|Sim||||||Sim|  
|Atributos ilimitados para regras de associação|Sim||||||Sim|  
|Previsão de sequências|Sim||||||Sim|  
|Destinos de várias previsões para Naïve Bayes, rede neural e regressão logística|Sim||||||Sim|  
  
 ## <a name="see-also"></a>Consulte também  
 [Especificações do produto para SQL Server 2016](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)   
 [Instalação do SQL Server](../database-engine/install-windows/installation-for-sql-server-2016.md)  


