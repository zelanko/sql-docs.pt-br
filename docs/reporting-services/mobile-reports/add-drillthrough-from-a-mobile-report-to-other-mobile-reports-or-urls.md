---
title: Adicionar o detalhamento de um relatório móvel para outros relatórios móveis ou URLs | Microsoft Docs
ms.date: 09/20/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 30d0a3fd-5588-417e-b25d-cc5b7624cdb1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4b702c79ad5c80254595ef5c4ff440919a8482e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280720"
---
# <a name="add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls"></a>Adicionar o detalhamento de um relatório móvel para outros relatórios móveis ou URLs
Você pode adicionar o detalhamento de qualquer grade de dados, gráfico ou medidor em um relatório móvel do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] para outro ou URL personalizada. 

Um *detalhamento*  é um link de um relatório de origem que abre outro relatório de destino ou uma URL. O relatório de detalhamento de destino geralmente contém detalhes sobre algum item no relatório de resumo. Dependendo do relatório móvel de origem, um ou mais parâmetros podem ser passados para o relatório móvel de destino ou integrados em uma URL personalizada.  
  
Quando você exibir o relatório móvel de origem no portal da Web do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] e selecionar um elemento com um destino do detalhamento, vá para o destino, outro relatório móvel ou uma URL.  

Itens de relatório com detalhamento, uma URL ou outro relatório móvel, contêm o ícone de detalhamento ![mobile-report-drill-through-icon](../../reporting-services/mobile-reports/media/mobile-report-drill-through-icon.png) no canto superior direito.

![mobile-report-gauge-drill-through](../../reporting-services/mobile-reports/media/mobile-report-gauge-drill-through.png) 

>**Dica**: crie o relatório de destino e salve-o em um portal da Web do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] primeiro. Se você planeja transmitir parâmetros do relatório de origem, adicione também os parâmetros ao relatório de destino. Em seguida, você pode definir o detalhamento do relatório de origem para o relatório de destino. [Adicione parâmetros a um relatório móvel](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md).
 
## <a name="set-up-drillthrough-to-a-mobile-report"></a>Configurar o detalhamento para um relatório móvel  

1. Na exibição de Layout no [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)], selecione uma visualização que dá suporte ao detalhamento.   

   Mapas e medidores dão suporte ao detalhamento, como a maioria dos gráficos e grades de dados simples.
   
2. No painel **Propriedades Visuais** , selecione **Destino de Detalhamento** > **Relatório móvel**.  
3. Selecione o servidor e o relatório móvel de destino.  

   >Observação: se o relatório móvel de destino não estiver no mesmo servidor que o relatório móvel de origem, conecte-o a uma URL personalizada, conforme explicado na próxima seção.  
 
4. Depois de selecionar um relatório móvel de destino, você pode ver seus parâmetros de entrada disponíveis, incluindo propriedades que podem ser vinculadas a controles do navegador e parâmetros configurados em conjuntos de dados do relatório móvel de destino.  

   ![móvel-relatório-detalhamento-destino](../../reporting-services/mobile-reports/media/mobile-report-drillthrough-target.PNG)
   
   *Propriedades de detalhamento do relatório móvel de destino*  
  
5. Selecione a seta à direita de cada propriedade para conectar propriedades com tipos de dados correspondentes a propriedades de saída disponíveis no relatório móvel de origem. Você também pode definir padrões para cada saída aqui, caso o usuário do relatório não tenha interagido com o relatório móvel de origem antes do detalhamento ao relatório móvel de destino.  
  
## <a name="set-up-a-drillthrough-to-a-custom-url"></a>Configurar um detalhamento para uma URL personalizada  
  
1. Na exibição de Layout no [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)], selecione uma visualização que dá suporte a destinos de detalhamento.    
2. No painel **Propriedades Visuais** , selecione **Destino de Detalhamento** > **URL Personalizada**.  Isso abrirá a caixa de diálogo de configuração de detalhamento.  
  
3. Em **Definir a URL de detalhamento**, insira a URL de destino para ir para ao clicar na visualização e selecione dos **Parâmetros disponíveis** listados à direita. Uma visualização da URL personalizada combinada com parâmetros de exemplo resolvidos (se fornecidos) é exibida no painel abaixo.  
  
   ![móvel-relatório-detalhamento-url](../../reporting-services/mobile-reports/media/mobile-report-drillthrough-url.PNG)
  
   *Detalhamento para propriedades da URL personalizada*  
  
4. Clique em **Aplicar**.  

  
Quando você visualiza um relatório móvel no [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)], se você clicar em uma visualização com detalhamento, verá uma mensagem informando que o detalhamento está desabilitado. Na verdade, você só pode detalhar para o destino depois de salvar ou publicar um relatório móvel e exibi-lo, não do modo de layout ou visualização do [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] .  

## <a name="hide-a-target-mobile-report-on-the-web-portal"></a>Ocultar um relatório móvel de destino no portal da Web
Se você não definir um valor padrão para o relatório de destino, considere ocultá-lo no portal da Web. Caso contrário, quando alguém tentar exibi-lo no portal da Web diretamente, sem passar pelo relatório de origem, ele estará vazio.

1. No portal da Web, selecione as reticências (...) no relatório de destino que você deseja ocultar e selecione Gerenciar.

2. Em **Propriedades**, selecione **Ocultar na exibição lado a lado**.

Você pode optar por exibir itens ocultos no portal da Web: 

* No canto superior direito do portal da Web, selecione **Exibir** > **Mostrar ocultos.** 

Itens ocultos são exibidos em uma cor mais clara.
    
### <a name="see-also"></a>Confira também  
 
* [Adicionar parâmetros a um relatório móvel do Reporting Services](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)
* [Criar relatórios móveis com o Publicador de Relatórios Móveis do SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) 
* [Portal da Web (modo nativo do SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md)

