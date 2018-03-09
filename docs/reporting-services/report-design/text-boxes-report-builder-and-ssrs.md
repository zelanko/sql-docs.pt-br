---
title: "Caixas de texto (Construtor de Relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10134"
- "10120"
- sql13.rtp.rptdesigner.textproperties.general.f1
- sql13.rtp.rptdesigner.textboxproperties.general.f1
ms.assetid: df49e4e3-f279-4c63-a03b-b70c095f4ba2
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 3800731909023731291417edf6228245cf93ac04
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="text-boxes-report-builder-and-ssrs"></a>Caixas de texto (Construtor de Relatórios e SSRS)
  Quando você pensa em uma caixa de texto, provavelmente imagina uma caixa autônoma que contém texto em uma superfície como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office PowerPoint. Nos relatórios paginados do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , algumas caixas de texto são assim, e podem exibir texto estático para títulos, descrições e rótulos ou texto dinâmico baseado em expressões. Mas todas as células de uma tabela ou matriz (uma região de dados tablix) também contêm uma caixa de texto, que pode ser formatada da mesma maneira que caixas de texto autônomas do seu relatório.  
  
> [!NOTE]  
>  Se você arrastar o valor do campo do conjunto de dados de um relatório diretamente para a superfície de design do relatório ou para uma caixa de texto na superfície de design do relatório, verá apenas o primeiro valor no conjunto de resultados ao executar o relatório. Para ver todos os valores de um campo, você precisa primeiro criar uma tabela, matriz ou região de dados de lista e arrastar o campo para uma célula na região de dados. Dessa maneira, quando você executar o relatório, verá todos os valores naquele campo.  
  
 Para mostrar texto repetido em um layout de formato livre, crie uma região de dados de lista e coloque a caixa de texto nele. Use uma lista quando quiser repetir um formato para vários valores, como, por exemplo, um formato de fatura do cliente repetido uma vez para cada cliente. Leia mais sobre a [criação de formulários e notas fiscais com listas de desejos](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md).  
  
 Use um contêiner de retângulo quando quiser controlar o layout da caixa de texto e o espaço em branco abaixo da última caixa de texto. Para obter mais informações, consulte [Retângulos e linhas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md).  
  
 A expressão em uma caixa de texto pode conter texto literal, apontar para um campo do banco de dados ou calcular dados. Todas as expressões são mostradas como texto de espaço reservado para que seja possível formatar números, cores e outras propriedades de aparência. Você também pode combinar espaços reservados com texto literal na mesma caixa de texto.  
  
 Você pode formatar texto em cada caixa de texto usando fontes, cores, estilos e ações variadas. Para obter mais informações, consulte [Formatando texto e espaços reservados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="GrowShrinkTextBox"></a> Ampliando e reduzindo uma caixa de texto  
 Por padrão, as caixas de texto apresentam um tamanho fixo. Você pode permitir a redução ou a expansão vertical de uma caixa de texto com base no seu conteúdo. Para obter mais informações, consulte [Permitir que uma caixa de texto seja ampliada ou reduzida &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/allow-a-text-box-to-grow-or-shrink-report-builder-and-ssrs.md).  
  
## <a name="rotating-a-text-box"></a>Girando uma caixa de texto  
 Girar caixas de texto pode ajudar a criar relatórios mais legíveis, dar suporte à orientação de texto específica à localidade, ajustar mais colunas em um relatório impresso com tamanho de página fixo e criar relatórios com mais apelo gráfico. Uma caixa de texto pode ser girada em direções diferentes: horizontal, vertical (90 graus) ou girada em 270 graus. A opção vertical geralmente é usada para idiomas do Leste Asiático que são escritos de cima para baixo. Na maioria dos renderizadores, a opção vertical trata a rotação de glifo corretamente, de forma que o texto seja escrito de cima para baixo, mas os caracteres não fiquem de lado. Para outros idiomas, nas opções vertical e 270 graus, o texto é escrito lateralmente.  
  
 Você pode girar caixas de texto que contêm texto literal, campos de um conjunto de dados de relatório ou dados calculados. A caixa de texto pode ser independente no corpo do relatório, em uma tabela ou matriz, ou em um cabeçalho e rodapé do relatório.  
  
 A imagem seguinte mostra três versões de um relatório de tabela que agrupa dados por mês. A caixa de texto que contém o valor de mês usa uma orientação de caixa de texto diferente.  
  
 ![rs_TextBoxOrientation](../../reporting-services/report-design/media/rs-textboxorientation.gif "rs_TextBoxOrientation")  
  
 A orientação é definida na caixa de texto e se aplica a todo o texto da caixa. Você não pode especificar uma orientação diferente para partes da caixa de texto.  
  
 Para começar, consulte a seção sobre como girar texto em [Tutorial: formatar texto &#40;Construtor de Relatórios&#41;](../../reporting-services/tutorial-format-text-report-builder.md) e veja [Definir orientação da caixa de texto &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/set-text-box-orientation-report-builder-and-ssrs.md).  
  
##  <a name="HowTo"></a> Tópicos de instruções  
 [Adicionar, mover ou excluir uma caixa de texto &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-move-or-delete-a-text-box-report-builder-and-ssrs.md)  
  
 [Formatar o texto em uma caixa de texto &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)  
  
 [Definir a orientação da caixa de texto &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/set-text-box-orientation-report-builder-and-ssrs.md)  
  
 [Permitir que uma caixa de texto seja ampliada ou reduzida &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/allow-a-text-box-to-grow-or-shrink-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Formatando texto e espaços reservados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [Formatando números e datas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)  
  
  
