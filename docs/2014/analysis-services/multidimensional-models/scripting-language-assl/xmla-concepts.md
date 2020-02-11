---
title: Conceitos de XMLA | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XMLA, concepts
ms.assetid: 816183a7-d2f7-4e14-8e5b-2a4c1798fbc1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0da9467d293c0081309accd99fb46d7589fb4b8b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62736570"
---
# <a name="xmla-concepts"></a>Conceitos de XMLA
  O padrão XMLA (XML for Analysis) oferece suporte a acesso a dados para fontes de dados que residem na World Wide Web. [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] implementa o XMLA de acordo com a especificação XMLA [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 1,1.  
  
 O XMLA (XML for Analysis) é um protocolo XML baseado em SOAP, criado especificamente para acesso a dados universal para qualquer fonte de dados multidimensional padrão residente na Web. O XMLA também elimina a necessidade de implantar um componente de cliente que expõe as interfaces Component Object Model [!INCLUDE[msCoName](../../../includes/msconame-md.md)] (com) ou .NET Framework. O XMLA é otimizado para a Internet, quando viagens de ida e volta ao servidor são onerosas em termos de tempo e de recursos e quando conexões com estado para uma fonte de dados podem limitar conexões do usuário no servidor.  
  
 O XMLA é o protocolo nativo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]para, usado para toda a interação entre um aplicativo cliente e uma [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]instância do. O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] oferece suporte completo ao XML for Analysis 1.1 e também oferece extensões para oferecer suporte ao gerenciamento de metadados, gerenciamento de sessão e a recursos de bloqueio. O AMO (Objetos de Gerenciamento de Análise) e o ADOMD.NET usam o protocolo XMLA ao se comunicarem com uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
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
  
  
