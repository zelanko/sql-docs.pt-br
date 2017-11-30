---
title: "Imprimir um relatório (Construtor de Relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b96936c9-c387-41a9-8c19-6eb325769ffd
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 98680d72888f7c5bea47a6b1d7bf8e81d90bc06c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="print-a-report-report-builder-and-ssrs"></a>Imprimir um relatório (Construtor de Relatórios e SSRS)
  Depois de salvar um relatório em um servidor de relatório, exiba e imprima o relatório em um navegador, no portal da Web do Reporting Services ou em qualquer aplicativo usado para exibir um relatório exportado. Antes de salvar um relatório, você pode imprimi-lo quando o visualiza.  
  
 Quando você imprime um relatório, pode especificar o tamanho do papel a ser usado. O tamanho do papel determina o número de páginas em um relatório e quais dados do relatório se ajustam em cada página. O tamanho do papel afeta somente relatórios renderizados com processadores de quebra de página não flexíveis: PDF, Imagem e Impressão. A definição do tamanho do papel não tem efeito sobre outros processadores. Para obter mais informações, consulte [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
 Na barra de ferramentas do visualizador de relatórios no portal da Web do Reporting Services ou na versão prévia do Construtor de Relatório, você pode exportar um relatório para um renderizador de quebra de página impressa ou clicar no botão Imprimir para imprimir uma cópia do relatório. Talvez você precise definir o tamanho do papel ou outras propriedades de configuração de página. Use a caixa de diálogo **Propriedades do Relatório** para alterar as propriedades de configuração de página, inclusive o tamanho do papel.  
  
 Você pode especificar margens de página de impressão em dois locais diferentes: em modo de design e em modo de execução.  
  
-   **Modo Design.** Quando você define as margens da página em modo de design, essas configurações são salvas na definição do relatório quando o relatório é salvo.  
  
-   **Modo de execução.** Quando você define as margens da página em modo de execução, essas informações não são salvas na definição do relatório. Na próxima vez que imprimir o relatório, você obterá as configurações da definição do relatório, a menos que você indique as margens de impressão novamente.  
  
    > [!NOTE]  
    >  As margens de impressão não são exibidas nos modos de design ou de execução. Não há nenhuma relação entre a área da superfície de design e a área de impressão do relatório. Em ver as margens de impressão, em modo de execução, clique em Layout de Impressão na guia **Executar** na Faixa de Opções.  
  
 Para obter mais informações sobre paginação de relatório, consulte [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-print-a-report-in-report-builder"></a>Para imprimir um relatório no Construtor de Relatórios  
  
1.  Abra um relatório.  
  
2.  Na guia Página Inicial, clique em **Executar**.  
  
3.  (opcional) Clique em **Layout de Impressão** para saber como o relatório ficará quando for impresso.  
  
4.  (opcional) Clique em **Configuração de Página** para definir o papel, a orientação e as margens.  
  
    > [!NOTE]  
    >  Os valores padrão provêm das propriedades do relatório, definidas na exibição Design. Os valores definidos aqui na caixa de diálogo **Configuração de Página** somente são válidos durante esta sessão. Quando você fechar este relatório e reabri-lo, ele terá os valores padrão novamente.  
  
5.  Clique em **Imprimir**.  
  
6.  Na caixa de diálogo **Imprimir** , selecione uma impressora e especifique outras opções de impressão.  
  
### <a name="to-print-a-report-from-a-web-browser-application"></a>Para imprimir um relatório em um aplicativo de navegador da Web  
  
1.  No portal da Web do Reporting Services, navegue para o relatório que deseja imprimir. Abra o relatório.  
  
3.  Na barra de ferramentas na parte superior do relatório, clique em **Imprimir**.  
  
    > [!NOTE]  
    >  Na primeira vez que você imprime um relatório HTML, o servidor de relatório solicita que você instale um controle ActiveX usado para impressão. Você deve instalar e configurar o controle para imprimir.  
  
4.  Na caixa de diálogo **Imprimir** , selecione uma impressora e clique em **Imprimir**.  
  
### <a name="to-print-a-report-from-other-applications"></a>Para imprimir um relatório em outros aplicativos  
  
1.  No portal da Web do Reporting Services, navegue para o relatório que deseja imprimir. Abra o relatório.  
  
2.  Na barra de ferramentas na parte superior do relatório, selecione um formato de renderização e clique em **Exportar**. O relatório é aberto em um aplicativo de visualizador que corresponde ao formato de renderização.  
  
     Por exemplo, se você selecionar PDF, o relatório será aberto no Adobe Acrobat Reader.  
  
3.  No menu **Arquivo** desse programa, clique em **Imprimir**.  
  
### <a name="to-change-paper-size"></a>Para alterar o tamanho do papel  
  
1.  Clique com o botão direito do mouse fora do corpo do relatório e clique em **Propriedades do Relatório**.  
  
2.  Em **Configuração de Página**, selecione um valor na lista **Tamanho do Papel** . Cada opção preenche as propriedades **Largura** e **Altura** . Você também pode especificar um tamanho personalizado, digitando valores numéricos nas caixas **Largura** e **Altura** . [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Os valores de tamanho têm uma unidade padrão com base nas configurações de localidade do usuário. Para designar uma unidade diferente, digite um designador de unidade física como cm, mm, pt ou pc depois do valor numérico.  
  
### <a name="to-set-page-margins-in-design-mode"></a>Para definir as margens da página em modo de design  
  
-   Clique com o botão direito do mouse na área azul ao redor da superfície de design, clique em **Propriedades do Relatório**e clique na página **Configurar Página** .  
  
### <a name="to-set-page-margins-in-run-mode"></a>Para definir as margens da página em modo de design  
  
-   Clique em **Configurar Página** na guia **Executar** .  
  
## <a name="see-also"></a>Consulte também  
 [Imprimir relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [Exportar relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [Caixa de diálogo Propriedades do Relatório, Configuração de Página &#40;Construtor de Relatórios&#41;](http://msdn.microsoft.com/library/eb3b5d01-7b82-4808-a58b-9e096742f8c6)   
 [Modo de exibição de Design de relatório &#40;Construtor de Relatórios&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)  
  
  
