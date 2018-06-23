---
title: Usando assemblies personalizados com relatórios | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- custom assemblies [Reporting Services]
- assemblies [Reporting Services], custom
- custom assemblies [Reporting Services], about custom assemblies
ms.assetid: 53d141d0-2185-466a-84dc-7b90d284da3d
caps.latest.revision: 31
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: ceeed9cb6688ca488e3726c5419f4cffa443e1df
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020646"
---
# <a name="using-custom-assemblies-with-reports"></a>Usando assemblies personalizados com relatórios
  No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], você pode escrever código personalizado para valores de item de relatório, estilos e formatação. Por exemplo, você pode usar código personalizado para formatar moedas com base na localidade, sinalizar certos valores com formatação especial ou aplicar outras regras comerciais que sejam praticadas por sua empresa. Uma forma de incluir esse código nos relatórios é criar um assembly de código personalizado usando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], que pode ser referenciado nos arquivos de definição de relatório. O servidor chama as funções em seus assemblies personalizados quando um relatório é executado. Os assemblies personalizados podem ser usados para recuperar funções especializadas que você planeja usar em seus relatórios.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Fazer referência a assemblies em um arquivo RDL](referencing-assemblies-in-an-rdl-file.md)  
 Descreve como referenciar seus assemblies personalizados em um arquivo de linguagem de definição de relatório.  
  
 [Implantando um assembly personalizado](deploying-a-custom-assembly.md)  
 Descreve como implantar um assembly personalizado para o Designer de Relatórios e para o servidor de relatório.  
  
 [Usar assemblies de nome forte personalizados](using-strong-named-custom-assemblies.md)  
 Descreve como usar assemblies personalizados com nomes fortes.  
  
 [Declarar permissões em assemblies personalizados](asserting-permissions-in-custom-assemblies.md)  
 Descreve como implantar assemblies personalizados com permissões limitadas e específicas e como declarar essas permissões em código.  
  
 [Acessar assemblies personalizados por meio de expressões](accessing-custom-assemblies-through-expressions.md)  
 Descreve como chamar métodos de assembly personalizados como expressões de relatório em suas definições de relatório.  
  
 [Inicializar objetos assembly personalizados](initializing-custom-assembly-objects.md)  
 Descreve como inicializar valores para objetos de assembly personalizados chamados de um relatório.  
  
 [Como depurar assemblies personalizados](how-to-debug-custom-assemblies.md)  
 Descreve como depurar seu código de assembly personalizado.  
  
## <a name="see-also"></a>Consulte também  
 [Linguagem RDL &#40;SSRS&#41;](../reports/report-definition-language-ssrs.md)  
  
  