---
title: OData Source | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.ODATASOURCE.F1
ms.assetid: cc9003c9-638e-432b-867e-e949d50cec90
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 86f055efd5ef4cbb41d7e600d88b4704bf4e47b1
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85431883"
---
# <a name="odata-source"></a>Origem do OData
  Você usa o componente de origem OData em um pacote do SSIS para consumir os dados dos serviços do OData (protocolo Open Data). O componente oferece suporte aos protocolos v2 e v3 do OData, bem como os formatos de dados ATOM e JSON.  
  
> [!NOTE]  
>  A origem OData pode ser usada para ler listas do SharePoint. Para ver todas as listas no servidor do SharePoint, use a seguinte URL: http:// \<server> /_vti_bin/listdata.svc. Para obter mais informações sobre as convenções de URL do SharePoint, consulte [Interface REST do SharePoint Foundation](https://msdn.microsoft.com/library/ff521587.aspx).  
  
## <a name="odata-format"></a>Formato OData  
 A maioria dos serviços do OData retornam os resultados em vários formatos. Você pode especificar o formato do conjunto de resultados usando a opção de consulta de $format. Os formatos como JSON e JSON Light são mais eficientes do que ATOM/XML, e podem oferecer melhor desempenho durante a transferência de grandes quantidades de dados. A tabela a seguir fornece os resultados dos testes de exemplo. Como você pode ver, houve um ganho de desempenho de 30% a 53% ao alternar de ATOM para JSON, e um ganho de desempenho de 67% ao alternar de ATOM para o novo formato JSON Light (disponível nos serviços de dados do WCF 5.1).  
  
|||||  
|-|-|-|-|  
|Linhas|ATOM|JSON|JSON (Light)|  
|10000|113 segundos|74 segundos|68 segundos|  
|1.000.000|1.110 segundos|853 segundos|665 segundos|  
  
> [!NOTE]  
>  A origem OData SSIS usa o ODataLib 5.5.0 para avaliar os feeds do OData e pode ler todos os formatos suportados por essa biblioteca.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Instalar e desinstalar o componente de origem do OData](../install-and-uninstall-odata-source-component.md)  
  
-   [Tutorial: usando a fonte OData &#91;SSIS&#93;](tutorial-using-the-odata-source.md)  
  
-   [Modifique a consulta de origem do OData em runtime](modify-odata-source-query-at-runtime.md)  
  
-   [Editor de Origem do OData &#40;Página Conexão&#41;](../odata-source-editor-connection-page.md)  
  
-   [Editor de Fonte OData &#40;Página Colunas&#41;](../odata-source-editor-columns-page.md)  
  
-   [Editor de Fonte OData &#40;Página Saída de Erro&#41;](../odata-source-editor-error-output-page.md)  
  
-   [Propriedades da origem do OData](odata-source-properties.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciador de conexões do OData](../connection-manager/odata-connection-manager.md)  
  
  
