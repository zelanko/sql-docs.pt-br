---
title: Arquitetura lógica (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Analysis Services, architecture
- logical architecture [Analysis Services Multidimensional Data]
ms.assetid: 1b9cae0a-8990-4194-af5f-a1ea5f2aff06
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 074659d42e1960c5f24cf4afa20668a3d8c823b0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62725469"
---
# <a name="logical-architecture-analysis-services---multidimensional-data"></a>Arquitetura lógica (Analysis Services – Dados Multidimensionais)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o usa componentes de cliente e servidor para fornecer OLAP (processamento analítico online) e Data Mining funcionalidade para aplicativos [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Business Intelligence:  
  
-   O componente de servidor do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] é implementado como um serviço do Microsoft Windows. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] dá suporte a várias instâncias no mesmo computador, com cada instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] do implementada como uma instância separada do serviço do Windows.  
  
-   Os clientes comunicam-se com o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] usando o XMLA padrão público, um protocolo baseado em SOAP para emissão de comandos e recebimento de respostas, expostos como um serviço Web. Os modelos de objeto de cliente são também fornecidos por XMLA e podem ser acessados pelo uso de um provedor gerenciado, como ADOMD.NET ou um provedor OLE DB.  
  
-   Os comandos de consulta podem ser emitidos usando as seguintes linguagens: SQL, Multidimensional Expressions (MDX), uma linguagem de consulta padrão do setor para análise ou DMX (Data Mining Extensions) uma linguagem de consulta padrão do setor orientada para mineração de dados. O ASSL (Analysis Services Scripting Language) também pode ser usado para gerenciar objetos de banco de dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
 O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] também oferece suporte a um mecanismo de cubo local, permitindo que aplicativos em clientes desconectados naveguem em dados multidimensionais armazenados localmente. Para obter mais informações, consulte [requisitos de arquitetura de cliente para o desenvolvimento de Analysis Services](../olap-physical/client-architecture-requirements-for-analysis-services-development.md)  
  
## <a name="in-this-section"></a>Nesta seção  
 **Visão geral da arquitetura lógica**  
 [Visão geral da arquitetura lógica &#40;Analysis Services de dados multidimensionais&#41;](logical-architecture-overview-analysis-services-multidimensional-data.md)  
  
 **Objetos do servidor**  
 [Objetos de servidor &#40;Analysis Services-dados multidimensionais&#41;](server-objects-analysis-services-multidimensional-data.md)  
  
 **Objetos de banco de dados**  
 [Objetos de banco de dados &#40;Analysis Services-&#41;](database-objects-analysis-services-multidimensional-data.md)  
  
 **Objetos de dimensão**  
 [Objetos de dimensão &#40;Analysis Services de dados multidimensionais&#41;](../../multidimensional-models-olap-logical-dimension-objects/dimension-objects-analysis-services-multidimensional-data.md)  
  
 **Objetos de Cubo**  
 [Objetos de cubo &#40;Analysis Services de dados multidimensionais&#41;](../../multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)  
  
 **Segurança de acesso do usuário**  
 [Arquitetura da segurança de acesso do usuário](understanding-microsoft-olap-logical-architecture.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Noções básicas sobre a arquitetura Microsoft OLAP](../olap-physical/understanding-microsoft-olap-architecture.md)   
 [Arquitetura física &#40;Analysis Services de dados multidimensionais&#41;](../olap-physical/understanding-microsoft-olap-physical-architecture.md)  
  
  
