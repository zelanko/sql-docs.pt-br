---
title: Recursos do Analysis Services compatíveis com as edições do SQL Server | Microsoft Docs
ms.date: 07/10/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6d4f0cc16638963dbbbb091bc19cade36e45fe3b
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792548"
---
# <a name="analysis-services-features-supported-by-sql-server-edition"></a>Edição do SQL Server dá suportados a recursos do Analysis Services

[!INCLUDE[ssas-appliesto-sql2016-later](../includes/ssas-appliesto-sql2016-later.md)]

Este artigo descreve os recursos com suporte nas diferentes edições do SQL Server 2016, 2017, os serviços de análise de 2019. Edição de avaliação oferece suporte a recursos da edição Enterprise.

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
|perspectivas|Sim||||||Sim|  
|Translations|Sim|Sim|||||Sim|  
|Cálculos DAX, consultas DAX, consultas MDX|Sim|Sim|||||Sim|  
|Segurança em nível de linha|Sim|Sim|||||Sim|  
|Várias partições|Sim||||||Sim|  
|Grupos de cálculo|Sim (começando com o SQL Server 2019)|Sim (começando com o SQL Server 2019)|||||Sim (começando com o SQL Server 2019)|  
|Modo de armazenamento na memória|Sim|Sim|||||Sim|  
|Modo DirectQuery|Sim|Sim (começando com o SQL Server 2019)|||||Sim|  

## <a name="multidimensional-models"></a>Modelos multidimensionais 
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Desenvolvedor|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Medidas semiaditivas|Sim|Não <sup> [1](#sameas)</sup>|||||Sim|  
|Hierarquias|Sim|Sim|||||Sim|  
|KPIs|Sim|Sim|||||Sim|  
|perspectivas|Sim||||||Sim|  
|Ações|Sim|Sim|||||Sim|  
|Inteligência de conta|Sim|Sim|||||Sim|  
|Inteligência de dados temporais|Sim|Sim|||||Sim|  
|Rollups personalizados|Sim|Sim|||||Sim|  
|Cubo de write-backs|Sim|Sim|||||Sim|  
|Dimensões de write-back|Sim <sup>[2](#wb)</sup>||||||Sim <sup>[2](#wb)</sup>|  
|Células de Writeback|Sim|Sim|||||Sim|  
|Detalhamento|Sim|Sim|||||Sim|  
|Tipos de hierarquia avançados (pai-filho e hierarquias desbalanceadas)|Sim|Sim|||||Sim|  
|Dimensões avançadas (Dimensões de referência, dimensões muitos-para-muitos)|Sim|Sim|||||Sim|  
|Medidas e dimensões vinculadas|Sim|Sim <sup> [3](#linkmd)</sup> |||||Sim|  
|Translations|Sim|Sim|||||Sim|  
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
|Expressões de medida|Sim||||||Sim|  
  
<a name="sameas">[1] </a> Medida semiaditiva LastChild o tem suporte na edição Standard, mas outras medidas semiaditivas, como None, FirstChild, FirstNonEmpty, LastNonEmpty, AverageOfChildren e ByAccount, não são. Medidas aditivas, como Sum, Count, Min, Max e medidas não aditivas (DistinctCount) têm suporte em todas as edições. 

<a name="wb">[2] </a> Dimensões de write-back são descontinuadas no SQL Server Analysis Services 2019 e versões posteriores.
 
<a name="linkmd">[3] </a> Standard edition oferece suporte à vinculação de medidas e dimensões no mesmo banco de dados, mas não de outros bancos de dados ou instâncias.
  
  
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

> [!NOTE]
> Mineração de dados é [preterido](analysis-services-backward-compatibility-sql2017.md#deprecated-features) no SQL Server Analysis Services 2017.
  
|Nome do recurso|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Desenvolvedor|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Algoritmos padrão|Sim|Sim|||||Sim|  
|Ferramentas de mineração de dados (Assistentes, Editores, Construtores de Consultas)|Sim|Sim|||||Sim|  
|Validação cruzada|Sim||||||Sim|  
|Modelos em subconjuntos filtrados de dados da estrutura de mineração|Sim||||||Sim|  
|Série temporal: Combinação personalizada entre métodos ARTXP e ARIMA|Sim||||||Sim|  
|Série temporal: Previsão com novos dados|Sim||||||Sim|  
|Consultas de DM simultâneas ilimitadas|Sim||||||Sim|  
|Configuração avançada e opções de ajuste para algoritmos de mineração de dados|Sim||||||Sim|  
|Suporte para algoritmos de plug-in|Sim||||||Sim|  
|Processamento paralelo de modelo|Sim||||||Sim|  
|Série temporal: previsão de séries cruzadas|Sim||||||Sim|  
|Atributos ilimitados para regras de associação|Sim||||||Sim|  
|Previsão de sequências|Sim||||||Sim|  
|Destinos de várias previsões para Naïve Bayes, rede neural e regressão logística|Sim||||||Sim|  
  


