---
title: Definir e configurar unidades de medida (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: a15a96c3-7d2c-433e-a440-4ea051e967a9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 48700208f4ff67c9f6b6932537558c283df13ee6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65576644"
---
# <a name="set-and-configure-measurement-units-report-builder-and-ssrs"></a>Definir e configurar unidades de medida (Construtor de Relatórios e SSRS)
  Em um relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , os indicadores usam uma das duas unidades de medida: percentual ou numérica.   
    
  Por padrão, indicadores são configurados para usar percentuais como a unidade de medida. Isso significa que os valores de indicador atribuídos a cada ícone no conjunto de indicadores são determinados por um intervalo de percentuais. Os intervalos de percentuais são divididos uniformemente pelos ícones no conjunto de indicadores. Cada ícone representa um estado de indicador. Você pode alterar os percentuais para cada ícone no conjunto de indicadores especificando percentuais inicial e final diferentes. Os indicadores também detectam automaticamente os valores mínimo e máximo nos dados.  
  
 Você pode alterar a unidade de medida para ser um valor numérico. Nesse caso, você não especifica o mínimo ou o máximo para obter os dados; em vez disso, fornece apenas os valores inicial e final para cada ícone usado pelo indicador.  
  
 Opções como unidades de medida podem ser definidas usando expressões. Para obter mais informações, consulte [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
## <a name="to-use-the-numeric-state-measurement-unit"></a>Para usar a unidade de medida em estado numérico  
  
1.  Clique com o botão direito do mouse no indicador que você deseja alterar e clique em **Propriedades do Indicador**.  
  
2.  Clique em **Valores e Estados** no painel esquerdo.  
  
3.  Na lista **Unidade de Medida de Estados** , clique em **Numérico**.  
  
     Se preferir, clique no botão **Expressão** (*fx*) para editar uma expressão que define o valor da opção.  
  
4.  Para cada ícone no conjunto de indicadores, atualize os valores nas caixas de texto **Início** e **Fim** .  
  
     Se preferir, clique no botão **Expressão** (*fx*) para editar uma expressão que define os valores das opções **Início** e **Fim** .  
  
    > [!NOTE]  
    >  Os valores das caixas de texto **Início** e **Fim** devem ser numéricos.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-use-the-percentage-measurement-unit"></a>Para usar a unidade de medida em percentual  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Indicadores &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
