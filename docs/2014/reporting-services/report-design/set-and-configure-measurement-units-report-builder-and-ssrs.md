---
title: Definir e configurar unidades de medida (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a15a96c3-7d2c-433e-a440-4ea051e967a9
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: b20cdba15d9b7b98e6fe3592fce350edece600be
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36005466"
---
# <a name="set-and-configure-measurement-units-report-builder-and-ssrs"></a>Definir e configurar unidades de medida (Construtor de Relatórios e SSRS)
  Indicadores fornecem duas unidades de medida: percentual e numérica. Por padrão, indicadores são configurados para usar percentuais como a unidade de medida. Isso significa que os valores de indicador atribuídos a cada ícone no conjunto de indicadores são determinados por um intervalo de percentuais. Os intervalos de percentuais são divididos uniformemente pelos ícones no conjunto de indicadores. Cada ícone representa um estado de indicador. Você pode alterar os percentuais para cada ícone no conjunto de indicadores especificando percentuais inicial e final diferentes. Os indicadores também detectam automaticamente os valores mínimo e máximo nos dados.  
  
 Você pode alterar a unidade de medida para ser um valor numérico. Nesse caso, você não especifica o mínimo ou o máximo para obter os dados; em vez disso, fornece apenas os valores inicial e final para cada ícone usado pelo indicador.  
  
 Opções como unidades de medida podem ser definidas usando expressões. Para obter mais informações, consulte [Expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-use-the-numeric-state-measurement-unit"></a>Para usar a unidade de medida em estado numérico  
  
1.  Clique com o botão direito do mouse no indicador que você deseja alterar e clique em **Propriedades do Indicador**.  
  
2.  Clique em **Valores e Estados** no painel esquerdo.  
  
3.  Na lista **Unidade de Medida de Estados** , clique em **Numérico**.  
  
     Se preferir, clique no botão **Expressão** (*fx*) para editar uma expressão que define o valor da opção.  
  
4.  Para cada ícone no conjunto de indicadores, atualize os valores nas caixas de texto **Início** e **Fim** .  
  
     Se preferir, clique no botão **Expressão** (*fx*) para editar uma expressão que define os valores das opções **Início** e **Fim** .  
  
    > [!NOTE]  
    >  Os valores das caixas de texto **Início** e **Fim** devem ser numéricos.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-use-the-percentage-measurement-unit"></a>Para usar a unidade de medida em percentual  
  
1.  Clique com o botão direito do mouse no indicador que você deseja alterar e clique em **Propriedades do Indicador**.  
  
2.  Clique em **Valores e Estados** no painel esquerdo.  
  
3.  Na lista **Unidade de Medida de Estados** , clique em **Percentual**.  
  
     Se preferir, clique no botão **Expressão** (*fx*) para editar uma expressão que define o valor da opção.  
  
4.  Opcionalmente, altere as opções **Mínimo** e **Máximo** para usar valores específicos em vez de detectar automaticamente os valores mínimo e máximo dos dados que o indicador usa. O valor **Mínimo** deve ser menor do que o valor **Máximo**.  
  
    > [!NOTE]  
    >  Se você definir explicitamente os valores mínimo e máximo, aquele intervalo de valor será usado pelo indicador independentemente dos valores reais mínimo e máximo nos dados. Isto significa que valores menores que o mínimo e maiores que o máximo serão excluídos da avaliação que determina o ícone de indicador que será mostrado no relatório.  
  
     Se preferir, clique no botão **Expressão** (*fx*) para editar uma expressão que define os valores da opção.  
  
5.  Para cada ícone no conjunto de indicadores, atualize os valores nas caixas de texto **Início** e **Fim** .  
  
     Se preferir, clique no botão **Expressão** (*fx*) para editar uma expressão que define os valores das opções **Início** e **Fim** .  
  
    > [!NOTE]  
    >  Os valores das caixas de texto **Início** e **Fim** devem ser numéricos.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Indicadores &#40;Construtor de Relatórios e SSRS&#41;](indicators-report-builder-and-ssrs.md)  
  
  