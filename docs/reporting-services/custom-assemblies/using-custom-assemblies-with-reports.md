---
title: "Usando Assemblies personalizados com relatórios | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom assemblies [Reporting Services]
- assemblies [Reporting Services], custom
- custom assemblies [Reporting Services], about custom assemblies
ms.assetid: 53d141d0-2185-466a-84dc-7b90d284da3d
caps.latest.revision: 32
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: fb818ce570a542a3cfcccec5c9290821c4e21181
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="using-custom-assemblies-with-reports"></a>Usando assemblies personalizados com relatórios
  No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], você pode escrever código personalizado para valores de item de relatório, estilos e formatação. Por exemplo, você pode usar código personalizado para formatar moedas com base na localidade, sinalizar certos valores com formatação especial ou aplicar outras regras comerciais que sejam praticadas por sua empresa. É uma maneira de incluir esse código em seus relatórios criar um assembly de código personalizado usando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que você pode fazer referência de dentro de seus arquivos de definição de relatório. O servidor chama as funções em seus assemblies personalizados quando um relatório é executado. Os assemblies personalizados podem ser usados para recuperar funções especializadas que você planeja usar em seus relatórios.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Referenciando Assemblies em um arquivo RDL](../../reporting-services/custom-assemblies/referencing-assemblies-in-an-rdl-file.md)  
 Descreve como referenciar seus assemblies personalizados em um arquivo de linguagem de definição de relatório.  
  
 [Implantando um assembly personalizado](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md)  
 Descreve como implantar um assembly personalizado para o Designer de Relatórios e para o servidor de relatório.  
  
 [Usando Assemblies personalizados de nome forte](../../reporting-services/custom-assemblies/using-strong-named-custom-assemblies.md)  
 Descreve como usar assemblies personalizados com nomes fortes.  
  
 [Declarando permissões em Assemblies personalizados](../../reporting-services/custom-assemblies/asserting-permissions-in-custom-assemblies.md)  
 Descreve como implantar assemblies personalizados com permissões limitadas e específicas e como declarar essas permissões em código.  
  
 [Acessando Assemblies personalizados por meio de expressões](../../reporting-services/custom-assemblies/accessing-custom-assemblies-through-expressions.md)  
 Descreve como chamar métodos de assembly personalizados como expressões de relatório em suas definições de relatório.  
  
 [Inicializando objetos Assembly personalizados](../../reporting-services/custom-assemblies/initializing-custom-assembly-objects.md)  
 Descreve como inicializar valores para objetos de assembly personalizados chamados de um relatório.  
  
 [Como: depurar Assemblies personalizados](../../reporting-services/custom-assemblies/how-to-debug-custom-assemblies.md)  
 Descreve como depurar seu código de assembly personalizado.  
  
## <a name="see-also"></a>Consulte também  
 [Linguagem de definição de relatório &#40; SSRS &#41;](../../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
