---
title: Guia do desenvolvedor&#39;s (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Integration Services, programming
- SSIS, programming
- SQL Server Integration Services, programming
- packages [Integration Services], programming
ms.assetid: 60fe148b-a7c4-4289-ae3e-2e949fc1886c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3fc7c93f8e499fb063e0d01c9132606f3ddfa3f7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62892393"
---
# <a name="developer39s-guide-integration-services"></a>Guia do desenvolvedor&#39;s (Integration Services)
  O [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] inclui um modelo de objeto totalmente reescrito, que foi aprimorado com vários recursos que tornam a extensão e a programação mais fáceis, flexíveis e eficientes. Desenvolvedores podem estender e programar quase todos os aspectos de pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 Como desenvolvedor do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], há duas abordagens fundamentais que você pode adotar na programação do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]:  
  
-   Você pode estender pacotes escrevendo componentes que são disponibilizados dentro do Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] para fornecer funcionalidade personalizada em um pacote.  
  
-   Você pode criar, configurar e executar pacotes programaticamente a partir de seus próprios aplicativos.  
  
 Se você considerar que os componentes internos do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] não atendem aos seus requisitos, você poderá ampliar a capacidade do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] codificando suas próprias extensões. Nessa abordagem, você tem duas opções distintas:  
  
-   Para uso ad hoc em um único pacote, você pode criar uma tarefa personalizada, escrevendo código na tarefa Script, ou um componente de fluxo de dados personalizado, escrevendo código no componente Script, que pode ser configurado como uma origem, transformação ou destino. Esses wrappers avançados escrevem o código de infraestrutura para você e permitem focar exclusivamente o desenvolvimento da sua funcionalidade personalizada; entretanto, não é fácil reutilizá-los em outros locais.  
  
-   Para permitir o uso em vários pacotes, você pode criar extensões personalizadas do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] tais como gerenciadores de conexões, tarefas, enumeradores, provedores de log e componentes de fluxo de dados. O modelo de objeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] gerenciado contém classes base que fornecem um ponto de partida e facilitam ainda mais o desenvolvimento de extensões personalizadas.  
  
 Se desejar criar pacotes dinamicamente, ou gerenciar e executar pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fora do ambiente de desenvolvimento, você poderá manipular pacotes programaticamente. Você pode carregar, modificar e executar pacotes existentes, ou criar e executar pacotes inteiramente novos programaticamente. Nessa abordagem, você tem uma série de opções:  
  
-   Carregar e executar um pacote existente sem modificação.  
  
-   Carregue um pacote existente, reconfigure-o (por exemplo, especifique outra fonte de dados) e execute-o.  
  
-   Crie um pacote novo, adicione e configure componentes, fazendo alterações em cada objeto e em cada propriedade, salve-o e, depois, execute-o.  
  
 Essas abordagens da programação do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] são descritas nessa seção e demonstradas através de exemplos.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Visão geral da programação do Integration Services](integration-services-programming-overview.md)  
 Descreve as funções de fluxo de controle e fluxo de dados no desenvolvimento do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 [Compreendendo as transformações síncronas e assíncronas](understanding-synchronous-and-asynchronous-transformations.md)  
 Descreve a diferença importante entre saídas síncronas e assíncronas e os componentes que usam essas saídas no fluxo de dados.  
  
 [Trabalhando programaticamente com gerenciadores de conexões](working-with-connection-managers-programmatically.md)  
 Lista os gerenciadores de conexões que você pode usar a partir do código gerenciado e os valores que os gerenciadores de conexões retornam quando o código chama o método `AcquireConnection`.  
  
 [Estender pacotes com scripts](extending-packages-scripting/extending-packages-with-scripting.md)  
 Descreve como estender o fluxo de controle por meio da tarefa Script ou o fluxo de dados por meio do componente Script.  
  
 [Estendendo pacotes com objetos personalizados](extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 Descreve como criar e programar tarefas personalizadas, componentes de fluxo de dados e outros objetos de pacote para uso em vários pacotes.  
  
 [Compilar Pacotes Programaticamente](building-packages-programmatically/building-packages-programmatically.md)  
 Descreve como criar, configurar e salvar pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] programaticamente.  
  
 [Executar e gerenciar pacotes programaticamente](run-manage-packages-programmatically/running-and-managing-packages-programmatically.md)  
 Descreve como enumerar, executar e gerenciar pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] programaticamente.  
  
## <a name="reference"></a>Referência  
 [Referência de mensagens e erros do Integration Services](integration-services-error-and-message-reference.md)  
 Lista os códigos de erro predefinidos do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] acompanhados de seus nomes simbólicos e descrições.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Ferramentas de solução de problemas para desenvolvimento de pacotes](troubleshooting/troubleshooting-tools-for-package-development.md)  
 Descreve os recursos e as ferramentas que o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece para solucionar problemas de pacotes durante o desenvolvimento.  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Exemplos do CodePlex, [Exemplos de Produtos do Integration Services](https://go.microsoft.com/fwlink/?LinkID=131204), em www.codeplex.com/MSFTISProdSamples  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Integration Services](sql-server-integration-services.md)  
  
  
