---
title: Formatando números e datas (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.placeholderproperties.number.f1
- "10127"
- sql13.rtp.rptdesigner.textboxproperties.number.f1
- "10130"
- "10286"
- sql13.rtp.rptdesigner.serieslabelproperties.number.f1
- "10285"
- sql13.rtp.rptdesigner.axisproperties.number.f1
ms.assetid: 6de1a725-9f06-4708-be26-2d55e442e344
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 379f8a3cc95df4bfb2ed55ac639516d025abc32f
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50029205"
---
# <a name="formatting-numbers-and-dates-report-builder-and-ssrs"></a>Formatando números e datas (Construtor de Relatórios e SSRS)
  Você pode formatar números e datas em regiões de dados selecionando um formato na página **Número** da caixa de diálogo **Propriedades** da região de dados correspondentes.  
  
 Para especificar cadeias de caracteres de formato dentro de um item de relatório de caixa de texto, selecione o item que você deseja formatar, clique com o botão direito do mouse, selecione **Propriedades da Caixa de Texto**e clique em **Número**. É possível formatar células individuais em uma tabela ou região de dados de matriz da mesma forma, porque as células em uma tabela ou matriz são caixas de texto individuais.  
  
 Uma região de dados do gráfico, normalmente, mostra datas ao longo do eixo de categoria (x) e valores ao longo do eixo de valor (y). Para especificar a formatação em um gráfico, clique com o botão direito do mouse em um eixo e selecione **Propriedades do Eixo**. No eixo de valor, você pode especificar formatos apenas para números. Para obter mais informações, consulte [Formatação de rótulos de eixos em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md).  
  
 Para especificar formatação em uma região de dados de Medidor, clique com o botão direito do mouse na escala do medidor e selecione **Propriedades de Escala Radial** ou **Propriedades de Escala Linear**.  
  
> [!NOTE]  
>  Se algumas das opções de formatação que você deseja usar estiverem esmaecidas, isso significa que elas não são compatíveis com o tipo de dados do campo definido na fonte de dados. Por exemplo, se o campo contiver valores numéricos, mas o tipo de dados do campo for String, você não poderá aplicar opções de formatação de dados numéricos, como moeda ou decimais.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="considerations-for-formatting-numbers-and-dates"></a>Considerações para formatação de números e datas  
 Antes de formatar números e datas em seu relatório, considere o seguinte:  
  
-   Por padrão, números são formatados para refletir as configurações culturais no computador cliente. Use cadeias de caracteres de formatação para especificar como os números são exibidos de forma que a formatação seja consistente, independentemente do local onde a pessoa que está exibindo o relatório está localizada.  
  
-   Os formatos fornecidos na página **Número** são um subconjunto das cadeias de caracteres de formatação numérica padrão do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] . Para formatar um número ou data usando um formato personalizado que não seja mostrado na caixa de diálogo, você pode usar qualquer cadeia de caracteres de formatação do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para números e datas. Para obter mais informações sobre cadeias de caracteres de formato personalizadas, consulte o tópico [Formatting Types](https://go.microsoft.com/fwlink/?LinkId=112024) no MSDN.  
  
-   Se uma cadeia de caracteres de formato personalizada foi especificada, ela terá uma prioridade mais alta sobre as configurações padrão que são específicas à cultura. Por exemplo, suponha que você defina uma cadeia de caracteres de formato personalizada de "#, ###" mostrar o número 1234 como 1,234. Isso pode ter significados diferentes para usuários dos Estados Unidos e para usuários da Europa. Antes de especificar um formato personalizado, considere como o formato escolhido afetará os usuários de diferentes culturas que venham a exibir o relatório.  
  
-   Se você especificar uma cadeia de caracteres de formato inválida, o texto formatado será interpretado como uma cadeia de caracteres literal que substituirá a formatação.  
  
-   Se estiver formatando uma mistura de números e caracteres na mesma caixa de texto, considere a possibilidade de usar um espaço reservado para formatar o número separadamente do restante do texto. Para obter mais informações, consulte [Formatando texto e espaços reservados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md). Se uma cadeia de caracteres de formato inválida for especificada para a propriedade Format na caixa de texto, a cadeia de caracteres de formato será ignorada. Se uma cadeia de caracteres de formato inválida for especificada para a propriedade Format no gráfico ou no medidor, a cadeia de caracteres de formato especificada será interpretada como uma cadeia de caracteres e a formatação não será aplicada.  
  
-   Se você selecionar **Moeda** em **Categoria** e marcar a opção **Mostrar valores em**, poderá selecionar **Milhares**, **Milhões**ou **Bilhões** para exibir números usando formatos financeiros. Por exemplo, se o valor do campo for 1.789.905.394 e você selecionar **Bilhões** e especificar 2 casas decimais, o valor exibido no relatório será 1,78.  
  
## <a name="see-also"></a>Consulte Também  
 [Formatando texto e espaços reservados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [Formatando linhas, cores e imagens &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-lines-colors-and-images-report-builder-and-ssrs.md)   
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Formatar rótulos de eixo como datas ou moedas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Formatando escalas em um medidor &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)  
  
  
