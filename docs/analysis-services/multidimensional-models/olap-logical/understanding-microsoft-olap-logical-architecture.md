---
title: "Arquitetura lógica (Analysis Services - dados multidimensionais) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- Analysis Services, architecture
- logical architecture [Analysis Services Multidimensional Data]
ms.assetid: 1b9cae0a-8990-4194-af5f-a1ea5f2aff06
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6a53a33d7a2c86498864321e1f1d85cf9a1d9d3c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="understanding-microsoft-olap-logical-architecture"></a>Noções básicas sobre a arquitetura lógica do OLAP da Microsoft
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] usa componentes cliente e servidor para fornecer processamento analítico online (OLAP) e funcionalidade de mineração de dados para aplicativos de business intelligence:  
  
-   O componente de servidor do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] é implementado como um serviço do Microsoft Windows. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] dá suporte a várias instâncias no mesmo computador, com cada instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] implementado como uma instância separada do serviço do Windows.  
  
-   Os clientes comunicam-se com o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] usando o XMLA padrão público, um protocolo baseado em SOAP para emissão de comandos e recebimento de respostas, expostos como um serviço Web. Os modelos de objeto de cliente são também fornecidos por XMLA e podem ser acessados pelo uso de um provedor gerenciado, como ADOMD.NET ou um provedor OLE DB.  
  
-   Os comandos de consulta podem ser emitidos usando as seguintes linguagens: SQL, Multidimensional Expressions (MDX), uma linguagem de consulta padrão do setor para análise ou DMX (Data Mining Extensions) uma linguagem de consulta padrão do setor orientada para mineração de dados. O ASSL (Analysis Services Scripting Language) também pode ser usado para gerenciar objetos de banco de dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
 O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] também oferece suporte a um mecanismo de cubo local, permitindo que aplicativos em clientes desconectados naveguem em dados multidimensionais armazenados localmente. Para obter mais informações, consulte [requisitos de arquitetura do cliente para o desenvolvimento do Analysis Services](../../../analysis-services/multidimensional-models/olap-physical/client-architecture-requirements-for-analysis-services-development.md)  
  
## <a name="in-this-section"></a>Nesta seção  
 **Visão geral da arquitetura lógica**  
 [Visão geral da arquitetura lógica &#40; Analysis Services - dados multidimensionais &#41;](../../../analysis-services/multidimensional-models/olap-logical/logical-architecture-overview-analysis-services-multidimensional-data.md)  
  
 **Objetos de servidor**  
 [Objetos de servidor &#40; Analysis Services - dados multidimensionais &#41;](../../../analysis-services/multidimensional-models/olap-logical/server-objects-analysis-services-multidimensional-data.md)  
  
 **Objetos de banco de dados**  
 [Objetos de banco de dados &#40; Analysis Services - dados multidimensionais &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
 **Objetos de dimensão**  
 [Objetos de dimensão &#40; Analysis Services - dados multidimensionais &#41;](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimension-objects-analysis-services-multidimensional-data.md)  
  
 **Objetos de cubo**  
 [Objetos de cubo &#40; Analysis Services - dados multidimensionais &#41;](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)  
  
 **Segurança de acesso do usuário**  
 [Arquitetura de segurança de acesso do usuário](http://msdn.microsoft.com/library/71b44e10-2bd0-44f7-8de9-7c8f5b7ac082)  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre a arquitetura Microsoft OLAP](../../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)   
 [Arquitetura física &#40; Analysis Services - dados multidimensionais &#41;](../../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-physical-architecture.md)  
  
  
