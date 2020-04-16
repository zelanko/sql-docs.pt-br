---
title: Componentes do servidor do motor OLAP | Microsoft Docs
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
ms.openlocfilehash: 535d1e05fc82882e0a2b5ea43ac9b2147e62338b
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388016"
---
# <a name="olap-engine-server-components"></a>Componentes do servidor de mecanismo OLAP
  O componente [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] do servidor é o aplicativo **msmdsrv.exe,** que funciona como um serviço do Windows. Esse aplicativo consiste em componentes de segurança, um componente de ouvinte do XML for Analysis (XMLA), um componente de processador de consulta e vários outros componentes internos que executam as seguintes funções:

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

 ![Diagrama da arquitetura de sistema do Analysis Services](../../../analysis-services/dev-guide/media/analysisservicessystemarchitecture.gif "Diagrama da arquitetura de sistema do Analysis Services")

## <a name="xmla-listener"></a>Ouvinte XMLA
 O componente ouvinte XMLA processa todas as comunicações de XMLA entre o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e seus clientes. A [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] `Port` configuração de configuração no arquivo msmdsrv.ini pode [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ser usada para especificar uma porta na qual uma instância ouve. Um valor 0 nesse arquivo indica que o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ouve na porta padrão. A menos que especificado de outro modo, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] usa as seguintes portas TCP padrão:

|Porta|Descrição|
|----------|-----------------|
|2383|Instância padrão [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]de .|
|2382|Rediretor para outras instâncias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|
|Atribuído dinamicamente na inicialização do servidor|Nomeado exemplo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]de .|

 Consulte [Configurar o Firewall do Windows para permitir o acesso aos serviços de análise](../../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) para obter mais detalhes.

## <a name="see-also"></a>Consulte Também
 [Regras de nomeação de objetos &#40;Serviços de Análise&#41;](object-naming-rules-analysis-services.md) [Arquitetura Física &#40;Serviços de Análise - Serviços multidimensionais de análise de](understanding-microsoft-olap-physical-architecture.md) &#40;de arquitetura&#41;de arquitetura lógica -&#41;de dados [multidimensionais](../olap-logical/understanding-microsoft-olap-logical-architecture.md)


