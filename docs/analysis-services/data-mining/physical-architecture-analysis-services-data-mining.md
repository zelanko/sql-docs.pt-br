---
title: Arquitetura física (Analysis Services - mineração de dados) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 99e2cf7386bdf395ac82f05cc0b94f3e2b5e3123
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62668494"
---
# <a name="physical-architecture-analysis-services---data-mining"></a>Arquitetura física (Analysis Services – Mineração de Dados)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa componentes cliente e de servidor para fornecer funcionalidades de mineração de dados para aplicativos de Business Intelligence:  
  
-   O componente de servidor é implementado como um serviço do Microsoft Windows. Você pode ter várias instâncias no mesmo computador, sendo que cada instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é implementada como uma instância separada do serviço do Windows.  
  
-   Os clientes comunicam-se com o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando o XMLA padrão público, um protocolo baseado em SOAP para emissão de comandos e recebimento de respostas, expostos como um serviço Web. Os modelos de objeto de cliente são também fornecidos por XMLA e podem ser acessados pelo uso de um provedor gerenciado, como ADOMD.NET ou um provedor OLE DB.  
  
-   Os comandos de consulta podem ser emitidos usando-se extensões DMX, uma linguagem de consulta padrão do setor orientada à mineração de dados. O ASSL (Analysis Services Scripting Language) também pode ser usado para gerenciar objetos de banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
## <a name="architectural-diagram"></a>Diagrama de arquitetura  
 Uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] executada como serviço e comunicação autônomos com o serviço ocorre por meio do XMLA, usando HTTP ou TCP.  
  
 O AMO é uma camada entre o aplicativo de usuário e a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que fornece acesso a objetos administrativos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . AMO é uma biblioteca de classe que recebe comandos de um aplicativo cliente e os converte em mensagens de XMLA para a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . AMO apresenta objetos de instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] como classes para o aplicativo de usuário final, com membros de método que executam comandos e membros de propriedade que mantêm os dados para os objetos [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 A ilustração a seguir mostra a arquitetura de componentes do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , inclusive serviços da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e componentes de usuário que interagem com a instância.  
  
 A ilustração mostra que a única forma de acessar a instância é usando o ouvinte XML for Analysis (XMLA), através do HTTP ou do TCP.  
  
> [!WARNING]  
>  O DSO foi substituído. Você não deve usar o DSO para desenvolver soluções.  
  
 ![Diagrama de arquitetura de sistema do Analysis Services](../../analysis-services/data-mining/media/analysisservicessystemarchitecture.gif "diagrama da arquitetura de sistema do Analysis Services")  
  
## <a name="server-configuration"></a>Configuração do Servidor  
 Uma instância de servidor pode oferecer suporte a vários bancos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , cada um com sua própria instância do serviço [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que responde a solicitações de clientes e processa objetos.  
  
 Instâncias separadas devem ser instaladas quando você deseja trabalhar com modelos de tabela e mineração de dados e/ou modelos multidimensionais. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dá suporte à instalação lado a lado de instâncias executadas em modo de tabela (que usa o mecanismo de armazenamento analítico na memória xVelocity [VertiPaq]) e instâncias executadas em uma das configurações convencionais OLAP, MOLAP ou ROLAP. Para obter mais informações, consulte [Determinar o modo de servidor de uma instância do Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
 Todas as comunicações entre um cliente e o servidor do Analysis Services usam XMLA, que é um protocolo independente de plataforma e de idioma. Quando é recebida uma solicitação de um cliente, o Analysis Services determina se ela está relacionada ao OLAP ou à mineração de dados e roteia a solicitação adequadamente. Para obter mais informações, consulte [Componentes de servidor do mecanismo OLAP](../../analysis-services/multidimensional-models/olap-physical/olap-engine-server-components.md).  
  
## <a name="see-also"></a>Consulte também  
 [Arquitetura lógica &#40;Analysis Services – Mineração de dados&#41;](../../analysis-services/data-mining/logical-architecture-analysis-services-data-mining.md)  
  
  
