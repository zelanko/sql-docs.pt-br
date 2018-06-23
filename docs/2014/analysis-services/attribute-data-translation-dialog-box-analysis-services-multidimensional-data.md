---
title: Atributo de caixa de diálogo de tradução de dados (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.dimensiondesigner.dimensionstoragesettings.f1
helpviewer_keywords:
- Attribute Data Translation dialog box
ms.assetid: bed286de-1e9b-49de-b09e-3cd076aba152
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 1b8d7f28696e04045ca5ac3f11bf38d4c67f60c2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116037"
---
# <a name="attribute-data-translation-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Tradução de Dados de Atributo (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Tradução de Dados de Atributo** para definir a coluna que contém os dados de legenda de tradução, assim como o agrupamento e a ordem de classificação a serem usados com os dados traduzidos. É possível exibir a caixa de diálogo **Tradução de Dados de Atributo** das seguintes maneiras:  
  
-   Clicando em **Nova coluna de legendas** ou em **Editar coluna de legendas** no painel **Barra de ferramentas** da guia **Traduções** do **Designer de Dimensão**.  
  
-   Clicando com o botão direito do mouse no painel **Detalhes da tradução** ou na guia **Traduções** do **Designer de Dimensão** e selecionando a coluna **Nova coluna de legendas** ou **Editar coluna de legendas**.  
  
## <a name="options"></a>Opções  
 **Atributo**  
 Exibe o atributo selecionado.  
  
 **Idioma**  
 Exibe o idioma selecionado.  
  
 **Legenda traduzida**  
 Define a legenda traduzida atual do atributo selecionado.  
  
 **Colunas de tradução**  
 Define a coluna onde os dados de legendas da tradução são armazenados. Apenas uma coluna pode ser selecionada. Todas as tabelas relacionadas que são referidas pela tabela de dimensões primária são exibidas.  
  
 **Designador de agrupamento**  
 Define o designador de agrupamento do atributo selecionado. Por padrão, o agrupamento atual do Windows é selecionado. Clique na seta para baixo para selecionar entre os agrupamentos disponíveis.  
  
 **Binary**  
 Selecione esta opção para classificar e comparar dados baseados nos padrões de bit definidos para cada caractere. A ordem de classificação binária diferencia maiúsculas e minúsculas, isto é, minúscula precede maiúscula, e diferencia acento. Essa é a ordem de classificação mais rápida.  
  
 Se esta opção não estiver selecionada, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] seguirá as regras de classificação e comparação definidas em dicionários do idioma ou alfabeto associado.  
  
> [!NOTE]  
>  Se essa opção estiver selecionada, as opções **Diferenciar maiúsculas de minúsculas**, **Diferenciar acentos**, **Diferenciar Katakana**e **Diferenciar Largura** estarão desabilitadas.  
  
 **Maiusculas e minúsculas**  
 Selecione esta opção para classificar e comparar dados com base nas regras do dicionário fornecido para o idioma ou alfabeto associado e para diferenciar entre letras maiúsculas e minúsculas.  
  
 Se esta opção não estiver selecionada, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considerará que as versões em maiúsculas e minúsculas de letras são iguais. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] define se letras minúsculas são classificadas inferior ou letras maiusculas quando **diferencia maiusculas de minúsculas** não estiver selecionada.  
  
 **Acentos**  
 Selecione esta opção para classificar e comparar dados com base nas regras do dicionário fornecido para o idioma ou alfabeto associado e para distinguir entre letras acentuadas ou não. Por exemplo, 'a' não é igual a 'á'.  
  
 Se esta opção não estiver selecionada, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considerará que as versões acentuadas e não acentuadas de letras são iguais.  
  
 **Diferenciar Katakana**  
 Selecione esta opção para classificar e comparar dados com base nas regras do dicionário fornecido para o idioma ou alfabeto associado e para distinguir entre os dois tipos de caracteres katakana japoneses: Hiragana e Katakana.  
  
 Se essa opção não estiver selecionada, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considerará que caracteres Hiragana e Katakana são iguais.  
  
 **Diferenciar largura**  
 Selecione esta opção para classificar e comparar dados com base nas regras do dicionário fornecido para o idioma ou alfabeto associado e para diferenciar entre um caractere de byte único (meia largura) e o mesmo caractere quando representado como um caractere de byte duplo (largura inteira).  
  
 Se essa opção não estiver selecionada, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considerará as representações de byte único e de byte duplo do mesmo caractere como iguais.  
  
## <a name="see-also"></a>Consulte também  
 [Designers e caixas de diálogo do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Detalhes de conversão &#40;guia traduções, Designer de dimensão&#41; &#40;Analysis Services - dados multidimensionais&#41;](translation-details-dimension-designer-analysis-services-multidimensional-data.md)  
  
  