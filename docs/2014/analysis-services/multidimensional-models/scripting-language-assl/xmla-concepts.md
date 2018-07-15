---
title: Conceitos de XMLA | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XMLA, concepts
ms.assetid: 816183a7-d2f7-4e14-8e5b-2a4c1798fbc1
caps.latest.revision: 10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3e381b0c3880dfd07ff10740ec1fffeeb295629a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37293506"
---
# <a name="xmla-concepts"></a>Conceitos de XMLA
  O padrão XMLA (XML for Analysis) oferece suporte a acesso a dados para fontes de dados que residem na World Wide Web. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] implementa XMLA por especificação XMLA 1.1.  
  
 O XMLA (XML for Analysis) é um protocolo XML baseado em SOAP, criado especificamente para acesso a dados universal para qualquer fonte de dados multidimensional padrão residente na Web. XMLA também elimina a necessidade de implantar um componente de cliente que expõe o modelo de objeto de componente (COM) ou [!INCLUDE[msCoName](../../../includes/msconame-md.md)] interfaces do .NET Framework. O XMLA é otimizado para a Internet, quando viagens de ida e volta ao servidor são onerosas em termos de tempo e de recursos e quando conexões com estado para uma fonte de dados podem limitar conexões do usuário no servidor.  
  
 O XMLA é o protocolo nativo para [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], usado para todas as interações entre um aplicativo cliente e uma instância de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] oferece suporte completo ao XML for Analysis 1.1 e também oferece extensões para oferecer suporte ao gerenciamento de metadados, gerenciamento de sessão e a recursos de bloqueio. O AMO (Objetos de Gerenciamento de Análise) e o ADOMD.NET usam o protocolo XMLA ao se comunicarem com uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="handling-xmla-communications"></a>Manipulando comunicações do XMLA  
 O padrão aberto XMLA descreve dois métodos geralmente acessíveis: `Discover` e `Execute`. Esses métodos usam a arquitetura de cliente e de servidor acoplada de forma flexível suportada pelo XML para manipular informações de entrada e de saída sobre uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 O método `Discover` obtém informações e metadados de um serviço Web. Essas informações podem incluir uma lista de fontes de dados disponíveis, como também informações sobre qualquer um dos provedores de fontes de dados. As propriedades definem dados obtidos de uma fonte de dados e dão forma a eles. O método `Discover` é comum para a definição dos muitos tipos de informação que podem ser requisitados por um aplicativo cliente de fontes de dados em instâncias do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. As propriedades e a interface genérica oferecem extensibilidade sem exigir que você reescreva funções existentes em um aplicativo cliente.  
  
 O método `Execute` permite que aplicativos executem comandos específicos do provedor em fontes de dados XMLA.  
  
 Embora o protocolo XMLA seja otimizado para aplicativos Web, também poderá ser usado para aplicativos orientados à LAN. Os aplicativos a seguir podem aproveitar os benefícios desta API baseada em XML:  
  
-   Aplicativos cliente/servidor que exigem tecnologia flexível entre os clientes e o servidor  
  
-   Aplicativos cliente/servidor que tenham como destino vários sistemas operacionais  
  
-   Clientes que não exigem estado significante para aumentar a capacidade do servidor  
  
## <a name="xmla-and-the-unified-dimensional-model"></a>XMLA e o modelo dimensional unificado  
 O XMLA é o protocolo usado por aplicativos de business intelligence que empregam a metodologia UDM (modelo dimensional unificado)  
  
  
