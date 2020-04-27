---
title: Usando assemblies personalizados com relatórios | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom assemblies [Reporting Services]
- assemblies [Reporting Services], custom
- custom assemblies [Reporting Services], about custom assemblies
ms.assetid: 53d141d0-2185-466a-84dc-7b90d284da3d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e79f48f4e4a2eb5fbc83c353461709658caf2509
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63265663"
---
# <a name="using-custom-assemblies-with-reports"></a>Usando assemblies personalizados com relatórios
  No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], você pode escrever código personalizado para valores de item de relatório, estilos e formatação. Por exemplo, você pode usar código personalizado para formatar moedas com base na localidade, sinalizar certos valores com formatação especial ou aplicar outras regras comerciais que sejam praticadas por sua empresa. Uma maneira de incluir esse código em seus relatórios é criar um assembly de código personalizado usando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que você pode referenciar em seus arquivos de definição de relatório. O servidor chama as funções em seus assemblies personalizados quando um relatório é executado. Os assemblies personalizados podem ser usados para recuperar funções especializadas que você planeja usar em seus relatórios.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Referenciando assemblies em um arquivo RDL](referencing-assemblies-in-an-rdl-file.md)  
 Descreve como referenciar seus assemblies personalizados em um arquivo de linguagem de definição de relatório.  
  
 [Implantando um assembly personalizado](deploying-a-custom-assembly.md)  
 Descreve como implantar um assembly personalizado para o Designer de Relatórios e para o servidor de relatório.  
  
 [Usando assemblies de nome forte personalizados](using-strong-named-custom-assemblies.md)  
 Descreve como usar assemblies personalizados com nomes fortes.  
  
 [Declarando permissões em assemblies personalizados](asserting-permissions-in-custom-assemblies.md)  
 Descreve como implantar assemblies personalizados com permissões limitadas e específicas e como declarar essas permissões em código.  
  
 [Acessando assemblies personalizados por meio de expressões](accessing-custom-assemblies-through-expressions.md)  
 Descreve como chamar métodos de assembly personalizados como expressões de relatório em suas definições de relatório.  
  
 [Inicializando objetos assembly personalizados](initializing-custom-assembly-objects.md)  
 Descreve como inicializar valores para objetos de assembly personalizados chamados de um relatório.  
  
 [Como fazer: Depurar assemblies personalizados](how-to-debug-custom-assemblies.md)  
 Descreve como depurar seu código de assembly personalizado.  
  
## <a name="see-also"></a>Consulte Também  
 [Linguagem RDL &#40;SSRS&#41;](../reports/report-definition-language-ssrs.md)  
  
  
