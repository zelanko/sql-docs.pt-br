---
title: Recursos do Integration Services compatíveis com as edições do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e5018225-68bb-4f34-ae4a-ead79d8ad13a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9963f137470c7e252bc00be189c37ac98e6374e4
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71284357"
---
# <a name="integration-services-features-supported-by-the-editions-of-sql-server"></a>Recursos do Integration Services compatíveis com as edições do SQL Server

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


 Este tópico fornece detalhes sobre os recursos do SSIS (SQL Server Integration Services) com suporte nas diferentes edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)].  

Para saber quais os recursos compatíveis com as edições Developer e Evaluation, consulte os recursos listados para o Enterprise Edition nas tabelas abaixo.
  
Para notas de versão mais recentes e informações sobre novidades, consulte os seguintes artigos:
-   [Notas de versão do SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
-   [Novidades do Integration Services no SQL Server 2016](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)
-   [Novidades do Integration Services no SQL Server 2017](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)
    
**Experimente o SQL Server 2016!**    

A edição Evaluation do SQL Server está disponível por um período de avaliação de 180 dias.  
    
> [![Download no Centro de Avaliação](https://docs.microsoft.com/analysis-services/analysis-services/media/download.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) **[Download do SQL Server 2016 no Centro de Avaliação](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)**    
    
## <a name="new-integration-services-features-in-sql-server-2017"></a><a name="ISNew"></a> Novos recursos do Integration Services no SQL Server 2017
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Mestre do Scale Out|Sim|||||
|Trabalho do Scale Out|Sim|Sim <sup>1</sup>|TBD|TBD|TBD|
|Suporte para Microsoft Dynamics AX e Microsoft Dynamics CRM em componentes do OData <sup>2</sup>|Sim|Sim||||

<sup>1</sup> Se você executar pacotes que exijam recursos somente Enterprise no Scale Out, os Trabalhos do Scale Out também deverão ser executados em instâncias do SQL Server Enterprise.

<sup>2</sup> Esse recurso também é compatível com o SQL Server 2016 com Service Pack 1.

## <a name="sql-server-import-and-export-wizard"></a><a name="IEWiz"></a> Assistente de Importação e Exportação do SQL Server

|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Assistente de Importação e Exportação do SQL Server|Sim|Sim|Sim|Sim|Sim|  

## <a name="integration-services"></a><a name="IS"></a> Integration Services  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Conectores internos de fonte de dados|Sim|Sim|||| 
|Tarefas e transformações internas|Sim|Sim||||  
|Origem e destino ODBC |Sim|Sim|||| 
|Tarefas e conectores de fonte de dados do Azure|Sim|Sim||||  
|Tarefas e conectores do Hadoop/HDFS|Sim|Sim||||  
|Ferramentas de criação de perfil de dados básicos|Sim|Sim|||| 

## <a name="integration-services---advanced-sources-and-destinations"></a><a name="ISAA"></a> Integration Services – origens e destinos avançados  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Origem e destino Oracle de alto desempenho da Attunity|Sim|||||  
|Origem e destino Teradata de alto desempenho da Attunity|Sim|||||  
|Origem e destino do SAP BW|Sim|||||  
|Destino de treinamento do modelo de mineração de dados|Sim|||||  
|Destino de processamento de dimensões|Sim|||||  
|Destino de processamento de partições|Sim|||||  
  
## <a name="integration-services---advanced-tasks-and-transformations"></a><a name="ISAT"></a> Integration Services – Tarefas e transformações avançadas  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Componentes do Change Data Capture da Attunity <sup>1</sup>|Sim|||||  
|Transformação de consulta de mineração de dados|Sim|||||  
|Transformações de pesquisa difusa e de agrupamento difuso|Sim|||||  
|Transformações de extração e de pesquisa de termos|Sim|||||  

<sup>1</sup> Os componentes do Change Data Capture da Attunity a seguir requerem a Enterprise Edition. O serviço Change Data Capture e o Change Data Capture Designer, no entanto, não requerem a Enterprise Edition. Você pode usar o Designer e o serviço em um computador em que o SSIS não está instalado.
