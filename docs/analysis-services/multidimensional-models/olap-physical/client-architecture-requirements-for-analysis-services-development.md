---
title: Requisitos de arquitetura de cliente do Analysis Services desenvolvimento | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- local mining models [Analysis Services]
- Analysis Services, architecture
- providers [Analysis Services]
- data pumps [Analysis Services]
- client architecture [Analysis Services]
- local cubes [Analysis Services]
ms.assetid: 03a8eb6b-159f-4a0a-afbe-06a2424b6090
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4bf626021f48834b9c7e3711ffcf5f31639591fc
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="client-architecture-requirements-for-analysis-services-development"></a>Requisitos de arquitetura do cliente para o desenvolvimento do Analysis Services
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] oferece suporte a uma arquitetura de cliente fino. O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] mecanismo de cálculo é totalmente baseado em servidor, para que todas as consultas são resolvidas no servidor. Como resultado, apenas uma viagem de ida e volta entre o cliente e o servidor é necessária para cada consulta, resultando em um desempenho evolutivo à medida que as consultas aumentam em complexidade.  
  
 O protocolo nativo para o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] é XML for Analysis (XML/A). O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] fornece diversas interfaces de acesso de dados para aplicativos cliente, mas todos os componentes comunicam-se com uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] usando XML for Analysis.  
  
 Diversos provedores diferentes são fornecidos com o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para oferecer suporte às diferentes linguagens de programação. Um provedor comunica-se com um servidor [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], enviando e recebendo XML for Analysis em pacotes SOAP sobre TCP/IP e sobre HTTP por meio do ISS (Serviços de Informações da Internet). Uma conexão HTTP usa um objeto COM instanciado por IIS, chamado de bomba de dados, que age como um condutor de dados [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. A bomba de dados não examina os dados subjacentes contidos em um fluxo HTTP de qualquer maneira, nem de qualquer das estruturas de dados subjacentes disponíveis a nenhum código na biblioteca de dados.  
  
 ![Arquitetura lógica do cliente para o Analysis Services](../../../analysis-services/multidimensional-models/olap-physical/media/as-clientarch9.gif "arquitetura lógica de cliente para o Analysis Services")  
  
 Os aplicativos cliente Win32 podem se conectar a um servidor [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] usando DB OLE para interfaces OLAP ou o modelo de objeto Microsoft® ActiveX® Data Objects (ADO) para linguagens de automação COM (Component Object Model), como Microsoft Visual Basic®. Aplicativos codificados com linguagens .NET podem se conectar a um servidor [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] por meio do ADOMD.NET.  
  
 Aplicativos existentes podem se comunicar com [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] sem modificação, apenas usando um dos provedores [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
|Linguagem de programação|Interface de acesso de dados|  
|--------------------------|---------------------------|  
|C++|OLE DB para OLAP|  
|Visual Basic 6|ADO MD|  
|Linguagens .NET|ADO MD.NET|  
|Toda linguagem que ofereça suporte SOAP|XML for Analysis|  
  
 O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] tem uma arquitetura Web com uma camada intermediária evolutiva completa para implantação por organizações grandes e pequenas. O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] fornece amplo suporte à camada intermediária para serviço Web. Aplicativos ASP têm suporte pelo OLE DB para OLAP e ADO MD, os aplicativos ASP.NET são suportados pelo ADOMD.NET. A camada intermediária ilustrada na figura a seguir é evolutiva para vários usuários simultaneamente.  
  
 ![Diagrama lógico para arquitetura de camada intermediária](../../../analysis-services/multidimensional-models/olap-physical/media/as-midtierarch9.gif "diagrama lógico para arquitetura de camada intermediária")  
  
 Ambos os aplicativos cliente e de camada intermediária podem se comunicar diretamente com o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] sem usar um provedor. Aplicativos cliente e de camada intermediária podem enviar XML for Analysis em pacotes SOAP sobre TCP/IP, HTTP ou HTTPS. O cliente pode ser codificado usando qualquer linguagem com suporte SOAP. Nesse caso, a comunicação é facilmente gerenciada pelo IIS (Serviços de Informações de Internet) usando HTTP, embora uma conexão direta com o servidor usando TCP/IP também possa ser codificada. Essa é a solução para o cliente mais fino possível no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="analysis-services-in-tabular-or-sharepoint-mode"></a>Analysis Services no modo Tabular ou do SharePoint  
 Em [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], o servidor pode ser iniciado no modo de mecanismo (VertiPaq) de análise na memória xVelocity para bancos de dados tabulares e [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] pastas de trabalho que foram publicadas em um site do SharePoint.  
  
 O [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)] e o [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] são os únicos ambientes de cliente com suporte para a criação e a consulta de bancos de dados na memória que usam o modo Tabular ou do SharePoint, respectivamente O item inserido [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] banco de dados que você cria usando o Excel e [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] ferramentas está contida na pasta de trabalho do Excel e é salvo como parte do arquivo. xlsx do Excel.  
  
 Porém, uma pasta de trabalho [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] poderá usar dados armazenados em um cubo tradicional se esses dados forem importados para ela. Você também poderá importar dados de outra pasta de trabalho [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] se eles tiverem sido publicados em um site do SharePoint.  
  
> [!NOTE]  
>  Quando você usa um cubo como uma fonte de dados para uma pasta de trabalho [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)], os dados obtidos no cubo são definidos como uma consulta MDX; porém, os dados são importados como um instantâneo bidimensional. Não é possível trabalhar interativamente com os dados nem atualizar os dados do cubo.  
  
 Para obter mais informações sobre como usar um cubo SSAS como uma fonte de dados, consulte o [Power Pivot para Excel](http://go.microsoft.com/fwlink/?LinkId=164234).  
  
### <a name="interfaces-for-power-pivot-client"></a>Interfaces de cliente do Power Pivot  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]interage com o mecanismo de armazenamento do mecanismo (VertiPaq) de análise na memória xVelocity na pasta de trabalho, usando as interfaces estabelecidas e os idiomas para o Analysis Services: AMO e ADOMD.NET; MDX e XMLA. Dentro do suplemento, as medidas são definidas por meio de uma linguagem de fórmula semelhante à do Excel, o DAX (Expressões de Análise de Dados). As expressões DAX são inseridas nas mensagens de XMLA que são enviadas ao servidor no processo.  
  
### <a name="providers"></a>Provedores  
 As comunicações entre [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e o Excel usam o provedor OLEDB do MSOLAP (versão 11.0). No provedor do MSOLAP, há quatro módulos diferentes, ou transportes, que podem ser usados para enviar mensagens entre o cliente e o servidor.  
  
 **TCP/IP** usada para conexões de cliente-servidor normais.  
  
 **HTTP** usada para conexões HTTP por meio do serviço de bomba de dados do SSAS ou por uma chamada para o SharePoint [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] componente de serviço da Web (WS).  
  
 **INPROC** usada para conexões com o mecanismo no processo.  
  
 **CANAL** reservado para comunicações com o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] serviço do sistema no farm do SharePoint.  
  
## <a name="see-also"></a>Consulte também  
 [Componentes de servidor do mecanismo OLAP](../../../analysis-services/multidimensional-models/olap-physical/olap-engine-server-components.md)  
  
  

