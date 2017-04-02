---
title: "Recursos do Integration Services com suporte nas edi&#231;&#245;es do SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e5018225-68bb-4f34-ae4a-ead79d8ad13a
caps.latest.revision: 15
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# Recursos do Integration Services com suporte nas edi&#231;&#245;es do SQL Server
 Este tópico fornece detalhes sobre os recursos do SSIS (SQL Server Integration Services) com suporte nas diferentes edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)].  

Para saber quais recursos têm suporte nas edições Evaluation e Developer, consulte SQL Server Enterprise Edition. 
  
Para notas de versão mais recentes e informações sobre novidades, consulte o seguinte:
-   [Notas de versão do SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
-   [Novidades do Integration Services no SQL Server 2016](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)
-   [Novidades do Integration Services no SQL Server vNext](../integration-services/what-s-new-in-integration-services-in-sql-server-vnext.md)
    
**Experimente o SQL Server 2016!**    

A edição Evaluation do SQL Server está disponível por um período de avaliação de 180 dias.  
    
> [![Baixar no Centro de Avaliação](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[Baixar o SQL Server 2016 no Centro de Avaliação](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Máquina Virtual pequena do Azure](../analysis-services/media/azure-virtual-machine-small.png) **[Criar uma Máquina Virtual com o SQL Server 2016 já instalado](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)**    

##  <a name="a-nameisanew-integration-services-features-in-sql-server-vnext"></a><a name="IS"></a>Novos recursos do Integration Services no SQL Server vNext
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Desenvolvedor|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Escalar horizontalmente|Sim||||||Sim|
|Suporte para Microsoft Dynamics AX e Microsoft Dynamics CRM nos componentes do OData <sup>1</sup>|Sim|Sim|||||Sim|

<sup>1</sup> Também há suporte para esse recurso no SQL Server 2016 com Service Pack 1.

##  <a name="a-nameisa-integration-services"></a><a name="IS"></a> Integration Services  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Desenvolvedor|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Conectores internos de fonte de dados|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Tarefas e conectores de fonte de dados do Azure|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Assistente de Importação e Exportação do SQL Server|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Tarefas e conectores do Hadoop / HDFS|Sim|Sim|Sim||||Sim|  
|Designer do SSIS e tempo de execução|Sim|Sim|||||Sim|  
|Tarefas e transformações internas|Sim|Sim|||||Sim|  
|Ferramentas de criação de perfil de dados básicos|Sim|Sim|||||Sim|  
|Serviço Change Data Capture para Oracle da Attunity|Sim||||||Sim|  
|Change Data Capture Designer para Oracle da Attunity|Sim||||||Sim| 

##  <a name="a-nameisaaa-integration-services---advanced-adapters"></a><a name="ISAA"></a> Integration Services – Adaptadores avançados  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Desenvolvedor|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Destino Oracle de alto desempenho|Sim||||||Sim|  
|Destino de Teradata de alto desempenho|Sim||||||Sim|  
|Origem e destino do SAP BW|Sim||||||Sim|  
|Adaptador de destino de treinamento do modelo de mineração de dados|Sim||||||Sim|  
|Adaptador de destino de processamento de dimensões|Sim||||||Sim|  
|Adaptador de destino de processamento de partições|Sim||||||Sim|  
|Componentes do Change Data Capture da Attunity|Sim||||||Sim|  
|Conector para ODBC (Conectividade Aberta de Banco de Dados) da Attunity.|Sim||||||Sim|  
  
##  <a name="a-nameisata-integration-services---advanced-transforms"></a><a name="ISAT"></a> Integration Services – Transformações avançadas  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Desenvolvedor|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Pesquisas persistentes (alto desempenho)|Sim||||||Sim|  
|Transformação de consulta de mineração de dados|Sim||||||Sim|  
|Transformações de pesquisa e agrupamento difuso|Sim||||||Sim|  
|Transformações de extração e pesquisa de termos|Sim||||||Sim|  
  