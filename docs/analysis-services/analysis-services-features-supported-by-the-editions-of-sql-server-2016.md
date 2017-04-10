---
title: "Recursos do Analysis Services com suporte nas edi&#231;&#245;es do SQL Server 2016 | Microsoft Docs"
ms.custom: ""
ms.date: "09/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
  - "analysis-services/multidimensional-tabular"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f09d7be1-bd63-43f8-b91c-bf19166b4457
caps.latest.revision: 4
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 3
---
# Recursos do Analysis Services com suporte nas edi&#231;&#245;es do SQL Server 2016
Esse tópico fornece detalhes dos recursos que têm suporte na diferentes edições do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
 A edição Evaluation do SQL Server está disponível por um período de avaliação de 180 dias.  
  
 Para obter as notas de versão mais recentes, confira [SQL Server 2016 Release Notes](../sql-server/sql-server-2016-release-notes.md). Para obter as últimas informações sobre as novidades, consulte [Novidades no Analysis Services](../analysis-services/what-s-new-in-analysis-services.md).
    
 **Experimente o SQL Server 2016!**    
    
 > [![Baixar no Centro de Avaliação](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[Baixar o SQL Server 2016 no Centro de Avaliação](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![A máquina virtual pequena do Azure](../analysis-services/media/azure-virtual-machine-small.png) **[Criar uma máquina virtual com o SQL Server 2016 já instalado](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)**    
    
  
 Para saber quais recursos têm suporte nas edições Evaluation e Developer, consulte SQL Server Enterprise Edition.
  
 Para navegar até a tabela de uma tecnologia do SQL Server, clique no respectivo link: 
 
 -  [Analysis Services](#SSAS)  
  
-   [Modelo semântico de BI (multidimensional)](#BIMD)  
  
-   [Modelo semântico de BI (tabular)](#BIT)  
  
-   [Power Pivot para SharePoint](#PPSP)  
  
-   [Mineração de dados](#DM)  
  
-   [Clientes de Business Intelligence](#BIC)  

##  <a name="SSAS"></a> Analysis Services  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Desenvolvedor|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Bancos de dados compartilhados escalonáveis|Sim||||||Sim|  
|Fazer backup/Restaurar e Anexar/Desanexar bancos de dados|Sim|Sim|||||Sim|  
|Sincronizar bancos de dados|Sim||||||Sim|  
|Instâncias do cluster de failover do AlwaysOn|Sim<br /><br /> O número de nós é o máximo do sistema operacional|Sim<br /><br /> Suporte para 2 nós|||||Sim<br /><br /> O número de nós é o máximo do sistema operacional|  
|Programação (AMO, ADOMD.Net, OLEDB, XML/A, ASSL, TMSL)|Sim|Sim|||||Sim|  
  
##  <a name="BIMD"></a> Modelo semântico de BI (multidimensional)  
  
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
|Medidas e dimensões vinculadas|Sim|Sim <sup>2</sup> |||||Sim|  
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
  <sup>2</sup> A edição Standard dá suporte à vinculação de medidas e dimensões no mesmo banco de dados, mas não de outros bancos de dados ou instâncias.
   
##  <a name="BIT"></a> Modelo semântico de BI (tabular)  
  
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
  
##  <a name="PPSP"></a> Power Pivot para SharePoint  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Desenvolvedor|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Integração de farm do SharePoint baseado em arquitetura de serviço compartilhado|Sim||||||Sim|  
|Relatórios de uso|Sim||||||Sim|  
|Regras de monitoramento de integridade|Sim||||||Sim|  
|Galeria do Power Pivot|Sim||||||Sim|  
|Atualização de dados do Power Pivot|Sim||||||Sim|  
|Feeds de dados do Power Pivot|Sim||||||Sim|  
  
##  <a name="DM"></a> Mineração de dados  
  
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
  
##  <a name="BIC"></a> Clientes de Business Intelligence  
 Os aplicativos cliente de software a seguir estão disponíveis no Centro de Download da Microsoft e são fornecidos para ajudar a criar documentos de Business Intelligence executados em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Quando esses documentos forem hospedados em um ambiente de servidor, use uma edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que dê suporte para esse tipo de documento. A tabela a seguir identifica qual edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contém os recursos de servidor necessários para hospedar os documentos criados nesses aplicativos cliente.  
  
|Nome da ferramenta|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Desenvolvedor|  
|---------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Suplementos de mineração de dados para Excel e Visio 2010 (.xlsx, .vsdx)|Sim|Sim|||||Sim|  
|[!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 2010 and 2013 (.xlsx)|Sim||||||Sim|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] (.xlsx)|Sim||||||Sim|  
  
> [!NOTE]  
>  1.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] é um suplemento do Excel para a criação de pastas de trabalho com um modelo de dados.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] não depende do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], mas o [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] é necessário para compartilhar e colaborar em pastas de trabalho do Excel com um modelo de dados no SharePoint. Essa funcionalidade está disponível como parte do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition.  
>   
>      No Excel 2016, a funcionalidade do Power Pivot é interna e, portanto, você não precisa mais do suplemento Power Pivot.  
> 2.  A tabela acima identifica as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] necessárias para habilitar essas ferramentas cliente; no entanto, essas ferramentas podem acessar os dados hospedados em qualquer edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 ## Consulte também  
 [Recursos com suporte nas edições do SQL Server 2016](Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
 [Especificações do produto para SQL Server 2016](../Topic/Product%20Specifications%20for%20SQL%20Server%202016.md)   
 [Instalação do SQL Server 2016](../database-engine/install-windows/installation-for-sql-server-2016.md)  

