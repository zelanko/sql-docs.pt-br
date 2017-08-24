---
title: "Recursos compatíveis com as edições do SQL Server do Integration Services | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e5018225-68bb-4f34-ae4a-ead79d8ad13a
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 365fb52c9808e0402323d52c85371c35555d833e
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-features-supported-by-the-editions-of-sql-server"></a>Recursos de serviços de integração com suporte nas edições do SQL Server
 Este tópico fornece detalhes sobre os recursos do SSIS (SQL Server Integration Services) com suporte nas diferentes edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)].  

Para recursos com suporte pelas edições Evaluation e Developer, consulte os recursos listados para o Enterprise Edition nas tabelas a seguir.
  
Para informações sobre novidades e as notas de versão mais recentes, consulte os seguintes artigos:
-   [Notas de versão do SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
-   [Novidades do Integration Services no SQL Server 2016](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)
-   [O que há de novo no Integration Services no SQL Server de 2017](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)
    
**Experimente o SQL Server 2016!**    

A edição Evaluation do SQL Server está disponível por um período de avaliação de 180 dias.  
    
> [![Baixar no Centro de Avaliação](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[Baixar o SQL Server 2016 no Centro de Avaliação](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
## <a name="ISNew"></a>Novos recursos do Integration Services no SQL Server 2017
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Expansão mestre|Sim|||||
|Trabalho de expansão|Sim|Sim <sup>1</sup>|TBD|TBD|TBD|
|Suporte para o Microsoft Dynamics AX e do Microsoft Dynamics CRM em componentes do OData <sup>2</sup>|Sim|Sim||||

<sup>1</sup> se você executar os pacotes que exigem recursos somente Enterprise em expansão, os trabalhadores de fora de escala também deve executar em instâncias do SQL Server Enterprise.

<sup>2</sup> esse recurso também é suportado no SQL Server 2016 com Service Pack 1.

## <a name="IEWiz"></a>Assistente de exportação e importação do SQL Server

|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Assistente de Importação e Exportação do SQL Server|Sim|Sim|Sim|Sim|Sim|  

## <a name="IS"></a> Integration Services  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Conectores internos de fonte de dados|Sim|Sim|||| 
|Tarefas e transformações internas|Sim|Sim||||  
|Origem e destino attunity ODBC|Sim|Sim|||| 
|Tarefas e conectores de fonte de dados do Azure|Sim|Sim||||  
|Tarefas e conectores do Hadoop/HDFS|Sim|Sim||||  
|Ferramentas de criação de perfil de dados básicos|Sim|Sim|||| 

## <a name="ISAA"></a>Serviços de integração - fontes e destinos avançados  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Destino Oracle de alto desempenho attunity|Sim|||||  
|Destino Teradata de alto desempenho attunity|Sim|||||  
|Origem e destino do SAP BW|Sim|||||  
|Destino de treinamento do modelo de mineração de dados|Sim|||||  
|Destino de processamento de dimensão|Sim|||||  
|Destino de processamento de partição|Sim|||||  
  
## <a name="ISAT"></a>Integration Services – tarefas e transformações avançadas  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Pesquisas de persistentes (alto desempenho)|Sim|||||  
|Componentes do Change Data Capture attunity <sup>1</sup>|Sim|||||  
|Transformação de consulta de mineração de dados|Sim|||||  
|Transformações de pesquisa difusa e agrupamento difuso|Sim|||||  
|Extração de termos e transformações de pesquisa de termo|Sim|||||  

<sup>1</sup> componentes o Change Data Capture da attunity exigem Enterprise edition. O serviço Change Data Capture e o Change Data Capture Designer, no entanto, não requerem Enterprise edition. Você pode usar o Designer e o serviço em um computador em que o SSIS não está instalado.
