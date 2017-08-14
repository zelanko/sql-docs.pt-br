---
title: Referenciando Assemblies em um arquivo RDL | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- RDL [Reporting Services], referencing assemblies
- referencing custom assemblies
- custom assemblies [Reporting Services], referencing
- Report Definition Language, referencing assemblies
- report definition files [Reporting Services]
ms.assetid: 9a48e552-7d47-4243-9be1-894990c506d9
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 9fd80c818f13972434b72a72ce306e2f494cf56f
ms.contentlocale: pt-br
ms.lasthandoff: 08/12/2017

---
# <a name="referencing-assemblies-in-an-rdl-file"></a>Referenciando assemblies em um arquivo RDL
  Para suporte ao uso de assemblies de código personalizado em arquivos de definição de relatório, os dois elementos de linguagem de definição de relatório (RDL) são incluídos na especificação RDL: o **CodeModules** elemento e o **Classes** elemento.  
  
 O **CodeModules** elemento permite que você se refira aos assemblies de código gerenciado em expressões de relatório. **CodeModules** é um elemento de nível superior que contém a referência ao assembly que você use os arquivos de definição de relatório para chamar funções especializadas. Uma entrada em uma definição de relatório que dá suporte ao uso de um assembly personalizado poderia ser assim:  
  
```  
<CodeModules>  
   <CodeModule>CurrencyConversion, Version=1.0.1363.31103, Culture=neutral, PublicKeyToken=null</CodeModule>  
</CodeModules>  
```  
  
 Em vez de chamar <xref:System.Reflection.Assembly.Load%2A> do seu código personalizado, registre seus assemblies personalizados manualmente adicionando **CodeModule** elementos para o arquivo RDL ou usando o **referências** guia do **propriedades do relatório** caixa de diálogo. Para obter mais informações, consulte [Referências a código personalizado e assemblies em expressões no Designer de Relatórios &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
 O **Classes** elemento suporta o uso de membros de instância em uma definição de relatório. **Classes de** é um elemento de nível superior que contém uma referência ao nome de classe e um nome de instância. Uma entrada em uma definição de relatório que dá suporte ao uso de membros de instância poderia ser assim:  
  
```  
<Classes>  
   <Class>  
      <ClassName>CurrencyConversion.DollarCurrencyConversion</ClassName>  
      <InstanceName>m_myDollarConversion</InstanceName>  
   </Class>  
</Classes>  
```  
  
 Para obter mais informações, consulte [acessando Assemblies personalizados por meio de expressões](../../reporting-services/custom-assemblies/accessing-custom-assemblies-through-expressions.md).  
  
## <a name="see-also"></a>Consulte também  
 [Usar assemblies personalizados com relatórios](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
