---
title: Fonte OData | Microsoft Docs
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.DTS.DESIGNER.ODATASOURCE.F1
ms.assetid: cc9003c9-638e-432b-867e-e949d50cec90
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c52506dcfa582cc3e0992fe4fda772489d544247
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="odata-source"></a>Origem do OData
  Use o componente OData Source em um pacote do SSIS para consumir os dados do serviço do OData (Protocolo Open Data). O componente oferece suporte para os protocolos OData v3 e v4.  
  
-   Para o protocolo V3 do OData, o componente dá suporte aos formatos de dados ATOM e JSON.  
  
-   Para o protocolo V4 do OData, o componente dá suporte ao formato de dados JSON.  
  
> [!NOTE]  
>  Você também pode usar o OData Source para ler as listas do SharePoint. Para ver todas as listas em um servidor do SharePoint, use a seguinte URL: http://\<server > / _vti_bin/ListData.svc. Para obter mais informações sobre as convenções de URL do SharePoint, consulte [Interface REST do SharePoint Foundation](http://msdn.microsoft.com/library/ff521587.aspx).  Fonte OData agora oferece suporte a produtos do Microsoft Dynamics AX Online e do Microsoft Dynamics CRM Online.
  
## <a name="odata-format"></a>Formato OData  
 A maioria dos serviços do OData retornam os resultados em vários formatos. Você pode especificar o formato do conjunto de resultados usando a opção de consulta de $format. Os formatos como JSON e JSON Light são mais eficientes do que o ATOM ou XML, e podem oferecer um melhor desempenho ao transferir grandes quantidades de dados. A tabela a seguir fornece os resultados dos testes de exemplo. Como você pode ver, houve um ganho de desempenho de 30% a 53% ao trocar do ATOM para o JSON e um ganho de desempenho de 67% ao trocar do ATOM para o novo formato JSON Light (disponível nos Serviços de Dados do WCF 5.1).  
  
|||||  
|-|-|-|-|  
|Linhas|ATOM|JSON|JSON (Light)|  
|10.000|113 segundos|74 segundos|68 segundos|  
|1.000.000|1.110 segundos|853 segundos|665 segundos|  
  
> [!NOTE]  
>  O OData Source do SSIS usa a versão 5.6.1 para analisar os feeds do OData V3 e o ODataLib 6.12.0 para analisar os feeds do OData V4.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Tutorial: Usando o OData Source](../../integration-services/data-flow/tutorial-using-the-odata-source.md)  
  
-   [Modifique a consulta de origem do OData em tempo de execução](../../integration-services/data-flow/modify-odata-source-query-at-runtime.md)  
  
-   [Editor de Origem do OData &#40;Página Conexão&#41;](../../integration-services/data-flow/odata-source-editor-connection-page.md)  
  
-   [Editor de Fonte OData &#40;Página Colunas&#41;](../../integration-services/data-flow/odata-source-editor-columns-page.md)  
  
-   [Editor de Fonte OData &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/odata-source-editor-error-output-page.md)  
  
-   [Propriedades da origem do OData](../../integration-services/data-flow/odata-source-properties.md)  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de Conexões OData](../../integration-services/connection-manager/odata-connection-manager.md)  
  
  
