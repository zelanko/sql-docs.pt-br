---
title: "Salvando relatórios (Construtor de Relatórios) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-builder
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 59ddc4b8-9517-4d3f-9c88-a07e9907cecb
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6300efd4947f449b74f38c131dc0b869cd324ae2
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="saving-reports-report-builder"></a>Salvando relatórios (Construtor de Relatórios)
  No Construtor de Relatórios, você pode salvar um relatório paginado em um servidor de relatório do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , na biblioteca do SharePoint, no compartilhamento de arquivos no qual você tem permissão de gravação ou no computador. 
  
Quando salva um relatório, na verdade, você está salvando a definição do relatório, que descreve o layout dele. Você não está salvando os dados. Sempre que o relatório é executado, seus dados são atualizados e é provável que sejam diferentes da execução anterior do relatório.  
  
 Para salvar o relatório em outro formato ou salvar a definição do relatório com os dados, use um dos seguintes recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   Exporte um relatório renderizado para outro formato de arquivo, como CSV (arquivos separados por vírgulas) ou pastas de trabalho do Excel e salve-o nesse formato. Também é possível gerar feeds de dados de relatórios e salvar os dados do relatório.  
  
-   Crie assinaturas de relatório para entregar e salvar relatórios a um compartilhamento de arquivo.  
  
-   Use o histórico de relatório para salvar versões de relatórios renderizados como cópias históricas.  
  
 Para saber mais sobre como exibir e gerenciar relatórios diretamente no servidor de relatório, consulte [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md) e [Servidor de Relatório do Reporting Services &#40;Modo nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md).  
  
##  <a name="SavingReportDefinitions"></a> Salvar relatórios em um servidor de relatório  
  O processo de salvar um relatório em um servidor de relatório também é conhecido como publicação de relatório. Embora seja possível salvar relatórios no computador, salvar relatórios em um servidor de relatório oferece muitas vantagens:  
  
-   Os relatórios ficam disponíveis para outros que têm permissão para acessar a pasta na qual você salvou o relatório.  
  
-   Os relatórios podem ser gerenciados e exibidos no portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Recursos de relatório, como fontes de dados, imagens e sub-relatórios são armazenados em um local para acesso mais fácil.  
  
-   Os relatórios podem ser entregues a outros usuários por meio de assinaturas.  
  
-   Os relatórios são armazenados de modo seguro no banco de dados do servidor de relatório.  
  
-   As execuções de relatórios podem ser registradas e é possível fornecer informações de desempenho e auditoria.  
  
##  <a name="ExportingAndSavingReports"></a> Exportando e salvando relatórios  
 Se você tiver um número pequeno de relatórios para arquivar, considere exportar um relatório e salvá-lo como um arquivo. Após exportar um relatório para um aplicativo (como PDF ou Excel), você pode salvá-lo como um arquivo e colocá-lo em um diretório compartilhado protegido na rede. Como alternativa, você poderá carregar um arquivo PDF ou Excel salvo como um item de recurso, se desejar manter todas as cópias de um relatório, independentemente do formato, no banco de dados do servidor de relatório. Para obter mais informações sobre como exportar um relatório, consulte [Exportar relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md) e [Carregar um arquivo ou relatório](../../reporting-services/reports/upload-a-file-or-report-report-manager.md).  
  
##  <a name="UsingFileShareDelivery"></a> Usando entrega de compartilhamento de arquivos  
 Se você tiver um grande número de relatórios a serem arquivados, crie uma assinatura que entrega o relatório diretamente ao sistema de arquivos. Para esta abordagem, você deve criar uma assinatura para cada relatório, escolher uma pasta compartilhada para armazenar os relatórios e definir uma agenda que determine quando o arquivo é criado. Depois de definir uma assinatura, o servidor de relatório pode executar o relatório sem assistência e adicionar arquivos de relatório ao arquivo morto usando a agenda fornecida. Você também poderá criar agendas de uso único, se desejar arquivar relatórios ocasionalmente. Para obter mais informações sobre assinaturas e a entrega de compartilhamento de arquivos, consulte [Entrega de compartilhamento de arquivos no Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md).  
  
##  <a name="UsingReportHistory"></a> Usando histórico de relatório  
 Você também pode usar o recurso de histórico de relatório para criar cópias históricas. Em seguida, é possível fazer backup do banco de dados do servidor de relatório e armazenar o backup em um local seguro para uso futuro. Todo o histórico de relatório (juntamente com relatórios, itens de fontes de dados compartilhadas, pastas, assinaturas e agendas compartilhadas) é armazenado no banco de dados do servidor de relatório. É possível criar um backup para manter uma cópia permanente do histórico de relatório e de metadados, como informações sobre assinatura que indicam os destinatários de um relatório. Para obter mais informações, consulte [Criar, modificar e excluir instantâneos no Histórico de Relatórios](../../reporting-services/report-server/create-modify-and-delete-snapshots-in-report-history.md).  
 
##  <a name="HowTo"></a> Tópicos de instruções  
  
-   [Salvar relatórios em um servidor de relatório &#40;Construtor de Relatórios&#41;](../../reporting-services/report-builder/save-reports-to-a-report-server-report-builder.md)  
  
-   [Salvar um relatório em uma biblioteca do SharePoint &#40;Construtor de Relatórios&#41;](../../reporting-services/report-builder/save-a-report-to-a-sharepoint-library-report-builder.md)  
   
## <a name="see-also"></a>Consulte também  
 [Relatórios, partes de relatório e definições de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [Instalar e desinstalar o Construtor de Relatórios](http://msdn.microsoft.com/library/2c9a5814-17bf-4947-8fb3-6269e7caa416)   
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Exportar relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [Imprimir relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)  
  
  
