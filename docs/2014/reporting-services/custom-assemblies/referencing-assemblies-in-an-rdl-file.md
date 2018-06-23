---
title: Referenciando assemblies em um arquivo RDL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- RDL [Reporting Services], referencing assemblies
- referencing custom assemblies
- custom assemblies [Reporting Services], referencing
- Report Definition Language, referencing assemblies
- report definition files [Reporting Services]
ms.assetid: 9a48e552-7d47-4243-9be1-894990c506d9
caps.latest.revision: 35
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 129e8d896dac89451af46873f97bcdc6074d016f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007001"
---
# <a name="referencing-assemblies-in-an-rdl-file"></a>Referenciando assemblies em um arquivo RDL
  Para dar suporte ao uso de assemblies de código personalizado em arquivos de definição de relatório, dois elementos da linguagem RDL foram incluídos na especificação de RDL: o elemento **CodeModules** e o elemento **Classes**.  
  
 O elemento **CodeModules** permite referenciar assemblies de código gerenciado em expressões de relatório. **CodeModules** é um elemento de nível superior que contém a referência ao assembly usado nos arquivos de definição de relatório para chamar funções especializadas. Uma entrada em uma definição de relatório que dá suporte ao uso de um assembly personalizado poderia ser assim:  
  
```  
<CodeModules>  
   <CodeModule>CurrencyConversion, Version=1.0.1363.31103, Culture=neutral, PublicKeyToken=null</CodeModule>  
</CodeModules>  
```  
  
 Em vez de chamar <xref:System.Reflection.Assembly.Load%2A> do código personalizado, registre os assemblies personalizados manualmente adicionando elementos **CodeModule** ao arquivo RDL ou usando a guia **Referências** da caixa de diálogo **Propriedades do Relatório**. Para obter mais informações, consulte [Referências a código personalizado e assemblies em expressões no Designer de Relatórios &#40;SSRS&#41;](../report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
 O elemento **Classes** dá suporte ao uso de membros de instância em uma definição de relatório. **Classes** é um elemento de nível superior que contém uma referência ao nome de classe e um nome de instância. Uma entrada em uma definição de relatório que dá suporte ao uso de membros de instância poderia ser assim:  
  
```  
<Classes>  
   <Class>  
      <ClassName>CurrencyConversion.DollarCurrencyConversion</ClassName>  
      <InstanceName>m_myDollarConversion</InstanceName>  
   </Class>  
</Classes>  
```  
  
 Para obter mais informações, consulte [Acessando assemblies personalizados por meio de expressões](accessing-custom-assemblies-through-expressions.md).  
  
## <a name="see-also"></a>Consulte também  
 [Usar assemblies personalizados com relatórios](using-custom-assemblies-with-reports.md)  
  
  