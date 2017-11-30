---
title: "Visão geral das extensões de processamento de dados | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: data processing extensions [Reporting Services], about extensions
ms.assetid: 1d652605-9313-4c75-98b4-ba4dcbbb222d
caps.latest.revision: "39"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 11e8c43eb7b717227cf5a624f6a18a424b598967
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="data-processing-extensions-overview"></a>Visão geral das extensões de processamento de dados
  As extensões de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] permitem que você se conecte a uma fonte de dados e recupere dados. Eles também servem como uma ponte entre uma fonte de dados e um conjunto de dados. As extensões de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] são modeladas de acordo com um subconjunto das interfaces do provedor de dados do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
 A tabela a seguir lista as extensões de processamento de dados incluídas no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
|Extensão de processamento de dados|Description|  
|-------------------------------|-----------------|  
|Extensão de processamento de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Usa o Provedor de Dados .NET Framework para SQL Server para se conectar e recuperar dados do [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)].|  
|Extensão de processamento de dados para OLE DB|Usa o Provedor de Dados .NET Framework para OLE DB. Com essa extensão, o servidor de relatório pode consultar qualquer fonte de dados que tenha um provedor OLE DB.|  
|Extensão de processamento de dados para Oracle|Usa o Provedor de Dados .NET Framework para Oracle. Com essa extensão, o servidor de relatório pode acessar fontes de dados Oracle por meio do software de conectividade de cliente Oracle.|  
|Extensão de processamento de dados para ODBC|Usa o Provedor de Dados .NET Framework para ODBC. Com essa extensão, o servidor de relatório pode acessar dados em qualquer banco de dados para qual exista um driver ODBC.|  
  
 Você pode usar a API [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] de processamento de dados para adicionar processamento de dados ao seu servidor de relatório.  
  
> [!NOTE]  
>  O [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] tem suporte interno para provedores de dados no [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Se você já implementou um provedor de dados completo, não precisará implementar uma extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Entretanto, você deve considerar a extensão do seu provedor de dados para incluir funcionalidade específica para o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 2005, que inclui credenciais de conexão seguros e agregações do lado de servidor.  
  
 Cada uma das extensões de processamento de dados incluídas com o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] usa um conjunto comum de interfaces. Isso garante que cada extensão implementa funcionalidade comparável.  
  
 Você pode desenvolver extensões de processamento de dados para as suas próprias fontes de dados, ou pode usar as interfaces para adicionar um processamento de uma camada de dados adicional a infraestruturas comuns de banco de dados. Você pode implantar suas extensões de processamento de dados personalizadas para habilitar a integração direta de dados nos servidores de relatórios existentes em sua organização. Você também poderá usá-las como parte de um pacote de relatórios personalizado fornecido a seus consumidores.  
  
 ![Arquitetura da extensão de processamento de dados](../../../reporting-services/extensions/data-processing/media/bk-dataprocess-extensions.gif "Arquitetura da extensão de processamento de dados")  
Arquitetura de extensão de processamento de dados do Reporting Services  
  
 As vantagens para a implementação de uma extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] incluem:  
  
-   Uma arquitetura de acesso a dados simplificada, com frequência com melhor sustentabilidade e desempenho aprimorado.  
  
-   A capacidade de exibir diretamente a funcionalidade específica da extensão para consumidores.  
  
-   Uma interface específica para seus consumidores para acessar sua fonte de dados no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
## <a name="data-extension-process-flow"></a>Fluxo de processo de extensão de dados  
 Antes de desenvolver a sua extensão de dados personalizada, você precisa entender como o servidor de relatório usa extensões de dados para processar dados. Você também deve compreender os construtores e os métodos chamados pelo pelo servidor de relatório.  
  
 ![Fluxo do processo da extensão de processamento de dados](../../../reporting-services/extensions/data-processing/media/bk-ext-01.gif "Fluxo do processo da extensão de processamento de dados")  
O fluxo de processo passo a passo de uma extensão de dados chamada pelo servidor de relatório  
  
 A ilustração mostra a sequência de eventos a seguir:  
  
1.  O servidor de relatório cria um objeto de conexão e o passa na cadeia de conexão e credenciais associados ao relatório.  
  
2.  O texto de comando do relatório é usado para criar um objeto de comando. No processo, a extensão de processamento de dados pode incluir código que analisa o texto de comando e cria qualquer parâmetro para o comando.  
  
3.  Depois que o objeto de comando e qualquer parâmetro são processados, um leitor de dados é gerado para retornar um conjunto de resultados e permite que o servidor de relatório associe os dados do relatório com o layout do relatório.  
  
## <a name="developer-requirements"></a>Requisitos de desenvolvedor  
 O desenvolvimento de uma extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] exige que você tenha:  
  
-   Um computador de implantação com o Designer de Relatórios ou com um servidor de relatório instalado.  
  
-   Um computador de desenvolvimento com o [!INCLUDE[vsprvsext](../../../includes/vsprvsext-md.md)] ou superior ou o SDK (Software Development Kit) do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] instalado.  
  
-   Uma compreensão detalhada dos recursos e das capacidades do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
-   Uma compreensão detalhada de arquitetura do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vstecado](../../../includes/vstecado-md.md)], dos provedores de dados [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], dos objetos DataSet ADO.NET e das interfaces comuns do [!INCLUDE[vstecado](../../../includes/vstecado-md.md)].  
  
-   Experiência de desenvolvimento em uma linguagem do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], como [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# ou [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] .NET.  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
