---
title: "Processar relatórios grandes | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report processing [Reporting Services], large reports
- page breaks [Reporting Services]
- large reports
- size [SQL Server], reports
- distributing reports [Reporting Services], large reports
ms.assetid: c5275a9f-c95b-46d7-bc62-633879a8a291
caps.latest.revision: 42
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 065902778339650fcd123556acdeabfe8504224f
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="process-large-reports"></a>Processar relatórios grandes
  Relatórios grandes apresentam certos desafios de processamento e requerem certas configurações para que sejam executados corretamente. Relatórios grandes não devem ser executados sob demanda, salvo se estiverem configurados para oferecer suporte à paginação.  
  
> [!NOTE]  
>  Por padrão, quebras de página são habilitadas. Não desabilite quebras de página se achar que o relatório conterá uma grande quantidade de dados. O formato de renderização HTML usado para renderizar inicialmente um relatório abre um relatório no navegador. Se o relatório não for paginado, todos os dados serão incluídos em uma única página, incompatível com a maioria dos navegadores. Por exemplo, um relatório com 5.000 linhas de dados provavelmente não poderá ser exibido em um navegador, em uma única página.  
  
 Se você estiver trabalhando com um relatório grande, escolha as opções de execução, renderização e entrega do relatório que podem acomodar documentos desse tipo. O tamanho do relatório é determinado principalmente pelo conjunto de linhas retornado da consulta e pela extensão de renderização usada para apresentar o relatório.  
  
 Para relatórios que contêm dados voláteis, o tamanho do relatório pode variar radicalmente de uma execução de relatório para outra. Nesse caso, você deve monitorar a fonte de dados para determinar como a volatilidade dos dados afeta o seu relatório e se é necessário seguir as etapas descritas neste tópico.  
  
 Para obter mais informações sobre como diagnosticar erros de tempo limite e de falta de memória, consulte o artigo [Como diagnosticar problemas ao executar relatórios no servidor de relatório](http://go.microsoft.com/fwlink/?LinkId=85634) em blogs.msdn.com.  
  
## <a name="configuration-recommendations"></a>Recomendações de configuração  
 As recomendações para execução e renderização de relatório e o acesso a ele incluem os seguintes itens:  
  
-   Projete o relatório para oferecer suporte à paginação. O servidor de relatório envia uma página do relatório por vez. Se o relatório incluir paginação, será possível controlar a quantidade de dados que será transmitida ao navegador. Para obter mais informações, consulte [Pré-carregar o cache &#40;Gerenciador de Relatórios&#41;](../../reporting-services/report-server/preload-the-cache-report-manager.md).  
  
-   Configure o relatório para ser executado como um instantâneo de relatório agendado para evitar que seja executado sob demanda. Não defina um valor de tempo limite para a execução de relatório. Execute o relatório em horários de pouca atividade.  
  
-   Configure o relatório para usar uma fonte de dados compartilhada para controlar se ele deve ser processado. Uma vantagem de usar uma fonte de dados compartilhada é a possibilidade de desabilitá-la. Desabilitar a fonte de dados impede o processamento do relatório.  
  
-   Desabilite o histórico de relatório se desejar conservar espaço em disco. Para desabilitar o histórico de relatório, desmarque todas as caixas de seleção na página Propriedades do histórico.  
  
-   Limite o acesso ao relatório. Configure o relatório para usar segurança de nível de item e substitua as atribuições de função padrão por novas atribuições que concedam acesso somente aos usuários que precisam de tal acesso.  
  
     Por padrão, os usuários podem abrir qualquer relatório que possa ser exibido na hierarquia da pasta. Ainda que você configure um relatório para execução como instantâneo, usuários que podem exibir o item do relatório em uma pasta podem abrir o relatório. Se o relatório for muito grande, pode fazer com que o navegador pare de responder quando um usuário abrir o relatório no Gerenciador de Relatórios.  
  
## <a name="rendering-recommendations"></a>Recomendações de renderização  
 Antes de configurar a distribuição de relatório, é importante saber quais clientes de renderização podem acomodar documentos grandes. O formato recomendado é a extensão de renderização HTML padrão com pequenas quebras de página flexível, mas é possível escolher qualquer outro formato que ofereça suporte à paginação.  
  
 O desempenho e o consumo de memória variam de acordo com o formato de renderização. O mesmo relatório será processado a velocidades diferentes e exigirá quantidades diferentes de memória dependendo do formato selecionado. Os formatos mais rápidos e que consomem menos memória são CSV, XML e HTML. PDF e Excel têm o desempenho mais lento, mas por motivos diferentes. O formato PDF usa intensamente a CPU, enquanto o Excel usa a RAM de maneira intensiva. A renderização de imagens recai entre os dois grupos. Você pode especificar o formato ao definir como o relatório será distribuído.  
  
## <a name="deployment-and-distribution-recommendations"></a>Recomendações de implantação e distribuição  
 Se você estiver usando quebras de página para controlar a renderização do relatório, poderá implantar um relatório grande do mesmo modo que faria com qualquer outro relatório. É possível conceder acesso ao relatório através do Gerenciador de Relatórios, uma parte do SharePoint Web, ou uma URL adicionada a um portal ou site da Web. Todas essas opções de implantação oferecem suporte a acesso sob demanda, assim como também oferecem suporte a um instantâneo de relatório executado anteriormente.  
  
 Uma estratégia de implantação alternativa é distribuir relatórios a usuários individuais. Você poderá distribuir relatórios grandes através de assinaturas se tiver cuidado com a configuração das opções de entrega. Use uma assinatura padrão ou uma assinatura controlada por dados para entregar o relatório. Algumas recomendações para assinatura e entrega:  
  
-   Configure uma assinatura para usar um arquivo Web (MHTML), PDF ou Excel.  
  
-   Configure uma assinatura para usar entrega de compartilhamento de arquivo se estiver usando PDF ou Excel. Quando o relatório for entregue, será possível usar um aplicativo de desktop para trabalhar com o relatório. É necessário definir permissões no compartilhamento de arquivo para determinar quem pode exibir o relatório.  
  
     Observe que quando o relatório está no compartilhamento de arquivo, ele não é controlado ou protegido pelo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para ser notificado quando o relatório for atualizado, crie uma segunda assinatura que use entrega de email para enviar somente uma notificação.  
  
 Se você quiser usar entrega de relatório por email, configure a assinatura para incluir um link. Evite enviar o relatório como anexo.  
  
## <a name="see-also"></a>Consulte também  
 [Assinaturas e entrega &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Definir propriedades de processamento de relatórios](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Gerenciamento do conteúdo do Servidor de Relatório &#40;Modo Nativo do SSRS&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Pré-carregar o cache &#40;Gerenciador de Relatórios&#41;](../../reporting-services/report-server/preload-the-cache-report-manager.md)  
  
  
