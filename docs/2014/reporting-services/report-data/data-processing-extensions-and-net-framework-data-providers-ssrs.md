---
title: Extensões de processamento de dados e provedores de dados .NET Framework (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], data
- data processing extensions [Reporting Services]
- data providers [Reporting Services]
- data retrieval [Reporting Services]
- Reporting Services, data sources
- report data [Report Builder], accessing
ms.assetid: 42a5afb5-f4c8-4957-b1fd-77bf39afa5be
caps.latest.revision: 18
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 80d27aca81ccac9b176cbc4fbab21b8cfae544b4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37150077"
---
# <a name="data-processing-extensions-and-net-framework-data-providers-ssrs"></a>Extensões de processamento de dados e provedores de dados do .NET Framework (SSRS)
  Uma extensão de processamento de dados [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é um componente instalado com [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], projetado para recuperar dados de um tipo específico de fonte de dados e para fornecer funcionalidade adicional para oferecer suporte ao design de relatórios e processamento de relatórios. Uma extensão de processamento de dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] é um componente disponível do [!INCLUDE[msCoName](../../includes/msconame-md.md)] ou de fontes de terceiros que dá suporte às interfaces <xref:System.Data> que permitem que você recupere e modifique dados de um tipo específico de fonte de dados.  
  
## <a name="understanding-a-data-processing-extension"></a>Entendendo uma extensão de processamento de dados  
 Uma extensão de processamento de dados [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dá suporte a um subconjunto das interfaces <xref:System.Data> . As extensões de processamento de dados exigem apenas o acesso somente leitura a uma fonte de dados para que as interfaces para gravação e atualização não sejam implementadas. Cada extensão de processamento de dados pode fornecer recursos personalizados para dar suporte ao processamento de relatório. Por exemplo, uma extensão de processamento de dados pode oferecer suporte aos seguintes tipos de recursos:  
  
-   Gerenciamento de credenciais separadamente da cadeia de conexão  
  
-   Suportando parâmetros de vários valores  
  
-   Recuperação de agregações de servidor, que são calculadas na fonte de dados  
  
-   Recuperando propriedades de dados bem como valores de dados da fonte de dados  
  
## <a name="understanding-a-data-provider"></a>Entendendo um provedor de dados  
 Uma extensão de processamento de dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] (às vezes, conhecido como um driver) dá suporte a um conjunto padrão de interfaces <xref:System.Data> para ler, gravar e atualizar dados em uma fonte de dados. Um provedor de dados pode ser usado quando não houver nenhuma extensão de processamento de dados disponível para um tipo específico de fonte de dados. Muitos provedores de dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] padrão de terceiros estão disponíveis.  
  
 Uma vez que [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tem uma arquitetura de provedor de dados extensível, você pode criar uma extensão de processamento de dados personalizada para incluir a funcionalidade extra fornecida pelas extensões de processamento de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte [Implementing a Data Processing Extension](../extensions/data-processing/implementing-a-data-processing-extension.md). Para as extensões de processamento de dados de terceiros, consulte a documentação que acompanha a extensão de processamento de dados de terceiros.  
  
> [!NOTE]  
>  Um provedor de dados [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] ou uma extensão de processamento de dados personalizada deve ser instalada e registrada antes de ser usada para acessar dados de uma fonte de dados. A extensão de processamento de dados deve ser instalada e registrada tanto no cliente de relatório para criá-lo quanto no servidor de relatórios para exibir o relatório publicado. Nem todos os provedores de dados se destinam a funcionar em um ambiente de servidor. Para obter mais informações, consulte [Registrar um provedor de dados .NET Framework padrão &#40;SSRS&#41;](register-a-standard-net-framework-data-provider-ssrs.md) e [Implantando uma extensão de processamento de dados](../extensions/data-processing/deploying-a-data-processing-extension.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral das extensões de processamento de dados](../extensions/data-processing/data-processing-extensions-overview.md)   
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
