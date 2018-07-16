---
title: Selecionar atributos de dimensão (Assistente para dimensões) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.dimensionattributes.f1
ms.assetid: f58a3e14-ab27-44d3-8c26-f5c9ee7583b0
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 08e54b933094b86c68af60277ff73b701bb5e4f6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37263442"
---
# <a name="select-dimension-attributes-dimension-wizard"></a>Selecionar atributos de dimensão (Assistente para Dimensões)
  Use a página **Selecionar Atributos de Dimensão** para selecionar e modificar os atributos para a dimensão a ser criada.  
  
> [!NOTE]  
>  Se você não consegue ler os valores de alguma coluna, maximize a janela do assistente e altere a largura de cada cabeçalho de coluna até que consiga ler os valores.  
  
 **Para abrir o Assistente para dimensões**  
  
-   No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], no **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta **Dimensões** de um projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e clique em **Nova Dimensão**.  
  
## <a name="options"></a>Opções  
 (Coluna com caixas de seleção)  
 Selecione para incluir um atributo na dimensão.  
  
 Para incluir um atributo específico, marque a caixa de seleção para esse atributo.  
  
 Para incluir todos os atributos, marque a caixa de seleção no cabeçalho de coluna.  
  
> [!NOTE]  
>  A caixa de seleção para o atributo de chave não pode ser desmarcada.  
  
 **Nome do atributo**  
 Lista os atributos disponíveis.  
  
 Para alterar o nome de um atributo, clique no nome do atributo e digite um nome novo para o atributo.  
  
 **Habilitar navegação**  
 Selecione para tornar o atributo disponível ao usuário final para navegação e filtragem. **Habilitar Navegação** deve ser selecionado para o atributo de chave. Para atributos não chave, o padrão é que **Habilitar Navegação** não esteja selecionado, o que faz com que os atributos não chave só sejam mostrados como propriedades do membro.  
  
 Na maioria dos casos, o atributo se torna disponível ou não está disponível para navegação definindo a `AttributeHierarchyEnabled` propriedade para `True` ou `False`, respectivamente. No entanto, nas três caixas a seguir, o assistente usa configurações diferentes.  
  
|Caso|Configurações|  
|----------|--------------|  
|Uma dimensão contém uma hierarquia pai-filho e **Habilitar Navegação** não é selecionado|O assistente deixa a `AttributeHierarchyEnabled` propriedade definida como `True`e define o `AttributeHierarchyVisible` atributo `False` para o atributo de chave.|  
|Uma tabela em uma dimensão contém uma chave estrangeira para uma tabela que não está na dimensão|O assistente seleciona a chave estrangeira como um atributo a ser incluído, mas não selecionará **Habilitar Navegação**. Se você mantiver estas configurações, a propriedade `AttributeHiearchyEnabled` do atributo será definida como `True` e a propriedade `AttributeHieararchyVisible` será definida como `False`.|  
|Uma dimensão contém tabelas floco de neve que são alcançadas por meio de colunas de chave estrangeira anuláveis<br /><br /> —e—<br /><br /> Habilitar Navegação não está selecionado para o atributo que está baseado na chave da tabela floco de neve|O assistente criará o novo atributo que tem o `AttributeHiearchyEnabled` propriedade definida como `True`e o `AttributeHieararchyVisible` propriedade definida como `False`.|  
  
 **Tipo de atributo**  
 (Opcional) Defina o tipo para o atributo. O valor padrão é **Regular**. O tipo de atributo fornece orientação a aplicativos clientes quanto a quais informações o atributo poderia conter.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda de F1 do Assistente de dimensão](dimension-wizard-f1-help.md)   
 [Dimensões &#40;Analysis Services - dados multidimensionais&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Dimensões em modelos multidimensionais](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
