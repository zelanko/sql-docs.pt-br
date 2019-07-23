---
title: Visão geral da programação do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Integration Services, programming
- architecture [Integration Services]
- assemblies [Integration Services]
- SSIS, programming
- SQL Server Integration Services, programming
- run-time engine [Integration Services]
- packages [Integration Services], programming
- data flow engine [Integration Services]
- languages [Integration Services]
ms.assetid: 262babc6-eea5-4609-bc65-07d64cbcfee9
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 487fe7483ed2a53ade9d64ab1fdca503cf748e94
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057524"
---
# <a name="integration-services-programming-overview"></a>Visão geral da programação do Integration Services

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] tem uma arquitetura que separa a movimentação e a transformação de dados de gerenciamento e fluxos de controle de pacotes. Há dois mecanismos distintos que definem essa arquitetura e isso pode ser automatizado e estendido na programação do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. O mecanismo de tempo de execução implementa a infraestrutura de gerenciamento de fluxos de controle e pacotes que permite aos desenvolvedores controlar o fluxo de execução e definir opções para registro de log, manipuladores de eventos e variáveis. O mecanismo de fluxo de dados é um mecanismo de desempenho alto, especializado, dedicado exclusivamente a extrair, transformar e carregar dados. Sua programação do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] se baseará nesses dois mecanismos.  
  
 A imagem a seguir descreve a arquitetura do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 ![Arquitetura do Integration Services](../integration-services/media/mw-dts-01.gif "Arquitetura do Integration Services")  
  
## <a name="integration-services-run-time-engine"></a>Mecanismo de tempo de execução do Integration Services  
 O mecanismo de tempo de execução do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] controla o gerenciamento e a execução de pacotes, implementando a infraestrutura que habilita a ordem de execução, o registro em log, variáveis e a manipulação de eventos. A programação do mecanismo de tempo de execução do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] permite que os desenvolvedores automatizem a criação, a configuração e a execução de pacotes e criem tarefas personalizadas e outras extensões.  
  
 Para obter mais informações, consulte [Estender o pacote com a tarefa Script](../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md), [Desenvolver uma tarefa personalizada](../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md) e [Compilar pacotes programaticamente](../integration-services/building-packages-programmatically/building-packages-programmatically.md).  
  
## <a name="integration-services-data-flow-engine"></a>Mecanismo de fluxo de dados do Integration Services  
 O mecanismo de fluxo de dados gerencia a tarefa de fluxo de dados, que é especializada, de alto desempenho, dedicada à movimentação e transformação de dados de origens distintas. Diferente de outras tarefas, a tarefa de fluxo de dados contém objetos adicionais chamados de componentes de fluxo de dados, que podem ser origens, transformações ou destinos. Esses componentes são as principais partes de movimentação da tarefa. Eles definem a movimentação e a transformação de dados. A programação do mecanismo de fluxo de dados permite que desenvolvedores automatizem a criação e a configuração dos componentes em uma tarefa de fluxo de dados e criem componentes personalizados.  
  
 Para obter mais informações, consulte [Estender o fluxo de dados com o componente de Script](../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md), [Desenvolver um componente de fluxo de dados personalizado](../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) e [Compilar pacotes programaticamente](../integration-services/building-packages-programmatically/building-packages-programmatically.md).  
  
## <a name="supported-languages"></a>Idiomas com suporte  
 O [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] dá suporte total ao [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]. Isso permite que desenvolvedores programem o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ao escolherem idiomas compatíveis com .NET. Embora o mecanismo de tempo de execução e o mecanismo de fluxo de dados sejam escritos em código nativo, ambos estão disponíveis através de um modelo de objeto totalmente gerenciado.  
  
 Você pode programar pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], tarefas personalizadas e componentes no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ou em outro editor de código ou de texto. O [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] oferece ao desenvolvedor muitas ferramentas e recursos para simplificar e acelerar os ciclos iterativos de codificação, depuração e teste. O [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] também facilita a implantação. Porém, você não precisa do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para compilar e criar projetos de código do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. O SDK do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] inclui os compiladores [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] e [!INCLUDE[csprcs](../includes/csprcs-md.md)] e as ferramentas relacionadas.  
  
> [!IMPORTANT]  
>  Por padrão, o [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] é instalado com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], mas não com o SDK de [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] . A menos que o SDK esteja instalado no computador e a documentação do SDK esteja incluída na coleção de manuais online, os links para o conteúdo do SDK desta seção não funcionarão. Depois de instalar o SDK do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)], você pode adicionar a documentação do SDK à coleção de Manuais Online e ao sumário seguindo as instruções fornecidas em [Adicionar ou remover a documentação do produto do SQL Server](https://msdn.microsoft.com/library/ef798cc8-87cf-4d60-a7bf-9e061bdd0052).  
  
 A tarefa e o componente Script do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] utilizam o VSTA ([!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications) como um ambiente de script inserido. O VSTA dá suporte ao [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Basic e ao [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual C#.  
  
> [!NOTE]  
>  As interfaces de programação de aplicativo [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] são incompatíveis com as linguagens de scripts baseadas em COM, como VBScript.  
  
## <a name="locating-assemblies"></a>Localizando assemblies  
 No [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], os assemblies do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] foram atualizados para o .NET 4.0. Há um cache de assembly global separado para o .NET 4, localizado em *\<unidade>* :\Windows\Microsoft.NET\assembly. Você pode localizar todos os assemblies do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] nesse caminho, normalmente na pasta GAC_MSIL.  
  
 Assim como nas versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], os principais arquivos .dll de extensibilidade do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] também estão localizados em *\<unidade>* :\Arquivos de Programas\Microsoft SQL Server\100\SDK\Assemblies.  
  
## <a name="commonly-used-assemblies"></a>Assemblies comumente usados  
 A tabela a seguir lista os assemblies usados com frequência durante a programação do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] através do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)].  
  
|Assembly|Descrição|  
|--------------|-----------------|  
|Microsoft.SqlServer.ManagedDTS.dll|Contém o mecanismo de tempo de execução gerenciado.|  
|Microsoft.SqlServer.RuntimeWrapper.dll|Contém o assembly de interoperabilidade primária (PIA), ou wrapper, para o mecanismo de tempo de execução nativo.|  
|Microsoft.SqlServer.PipelineHost.dll|Contém o mecanismo de fluxo de dados gerenciado.|  
|Microsoft.SqlServer.PipelineWrapper.dll|Contém o assembly de interoperabilidade primária (PIA), ou wrapper, para o mecanismo de fluxo de dados nativo.|  
  
  
