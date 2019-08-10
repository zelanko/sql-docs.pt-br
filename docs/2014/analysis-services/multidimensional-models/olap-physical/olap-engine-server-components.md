---
title: Componentes do servidor do mecanismo OLAP | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Analysis Services, architecture
- ports [Analysis Services]
- XML/A listener
- server architecture [Analysis Services]
ms.assetid: 5193c976-9dcd-459c-abba-8c3c44e7a7f2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0537be8bda9c367fc381140183b10ddf383cf16a
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68889529"
---
# <a name="olap-engine-server-components"></a>Componentes do servidor de mecanismo OLAP
  O componente de servidor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] é o aplicativo **msmdsrv. exe** , que é executado como um serviço do Windows. Esse aplicativo consiste em componentes de segurança, um componente de ouvinte do XML for Analysis (XMLA), um componente de processador de consulta e vários outros componentes internos que executam as seguintes funções:  
  
-   Análise de instruções recebidas dos clientes  
  
-   Gerenciamento de metadados  
  
-   Tratamento de transações  
  
-   Processamento de cálculos  
  
-   Armazenagem de dimensões e dados de célula  
  
-   Criação de agregações  
  
-   Programação de consultas  
  
-   Cache de objetos  
  
-   Gerenciamento de recursos do servidor  
  
## <a name="architectural-diagram"></a>Diagrama de arquitetura  
 Uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] executada como serviço e comunicação autônomos com o serviço ocorre por meio do XMLA, usando HTTP ou TCP. AMO é uma camada entre o aplicativo de usuário e a instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Essa camada fornece acesso a objetos administrativos do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. AMO é uma biblioteca de classe que recebe comandos de um aplicativo cliente e os converte em mensagens de XMLA para a instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . AMO apresenta objetos de instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] como classes para o aplicativo de usuário final, com membros de método que executam comandos e membros de propriedade que mantêm os dados para os objetos [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
 A ilustração a seguir mostra a arquitetura de componentes do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], inclusive todos os elementos principais executados dentro da instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e todos os componentes de usuário que interagem com a instância. A ilustração também mostra que o único modo de acessar a instância é usando o ouvinte do XML for Analysis (XMLA) ou usando HTTP ou TCP.  
  
 ![Diagrama da arquitetura do sistema Analysis Services](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/analysisservicessystemarchitecture.gif "Diagrama da arquitetura do sistema Analysis Services")  
  
## <a name="xmla-listener"></a>Ouvinte XMLA  
 O componente ouvinte XMLA processa todas as comunicações de XMLA entre o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e seus clientes. A [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] definição de configuração no arquivo msmdsrv. ini pode ser usada para especificar uma porta na qual uma instância escuta. `Port` Um valor 0 nesse arquivo indica que o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ouve na porta padrão. A menos que especificado de outro modo, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] usa as seguintes portas TCP padrão:  
  
|Port|Descrição|  
|----------|-----------------|  
|2383|Instância padrão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|2382|Redirecionador para outras instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|Atribuído dinamicamente na inicialização do servidor|Instância nomeada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
  
 Consulte [Configurar o Firewall do Windows para permitir acesso Analysis Services](../../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) para obter mais detalhes.  
  
## <a name="see-also"></a>Consulte também  
 [Regras &#40;de nomenclatura de objeto Analysis Services&#41;](object-naming-rules-analysis-services.md)   
 [Arquitetura física &#40;Analysis Services – Dados Multidimensionais&#41;](understanding-microsoft-olap-physical-architecture.md)   
 [Arquitetura &#40;lógica Analysis Services-dados multidimensionais&#41;](../olap-logical/understanding-microsoft-olap-logical-architecture.md)  
  
  
