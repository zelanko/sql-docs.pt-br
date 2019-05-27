---
title: Salvando relatórios (Construtor de Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 59ddc4b8-9517-4d3f-9c88-a07e9907cecb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e21b1c9e48dcccf8b72a60fbd381aac3d878c0dc
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107627"
---
# <a name="saving-reports-report-builder"></a>Salvando relatórios (Construtor de Relatórios)
  O Construtor de Relatórios permite salvar um relatório em um servidor de relatório, na biblioteca do SharePoint, no compartilhamento de arquivo no qual você tem permissão de gravação, ou no seu computador. É possível salvar um relatório no mesmo local do qual foi aberto, salvá-lo em outro local ou salvá-lo com um novo nome no mesmo local ou em outro local. Por padrão, um relatório é salvo novamente no local do qual foi aberto. Quando salva o relatório, na verdade, você está salvando a definição do relatório, que descreve o layout do relatório. Você não está salvando os dados. Sempre que o relatório é executado, seus dados são atualizados e é provável que sejam diferentes da execução anterior do relatório.  
  
 Para salvar o relatório em outro formato ou salvar a definição do relatório com os dados, use um dos seguintes recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   Exporte um relatório renderizado para outro formato de arquivo, como CSV (arquivos separados por vírgulas) ou pastas de trabalho do Excel e salve-o nesse formato. Também é possível gerar feeds de dados de relatórios e salvar os dados do relatório.  
  
-   Crie assinaturas de relatório para entregar e salvar relatórios a um compartilhamento de arquivo.  
  
-   Use o histórico de relatório para salvar versões de relatórios renderizados como cópias históricas.  
  
 Para saber mais sobre como exibir e gerenciar relatórios diretamente no servidor de relatórios, consulte [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md) e [Servidor de relatórios do Reporting Services &#40;Modo nativo&#41;](../report-server/reporting-services-report-server-native-mode.md) nos [Manuais Online](https://go.microsoft.com/fwlink/?LinkId=154888) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em msdn.microsoft.com.  
  
##  <a name="SavingReportDefinitions"></a> Salvando definições de relatório  
 Embora seja possível salvar relatórios no computador, salvar relatórios em um servidor de relatório oferece muitas vantagens.  
  
 Salvar um relatório em um servidor de relatório oferece as seguintes vantagens:  
  
-   Os relatórios ficam disponíveis para outros que têm permissão para acessar a pasta na qual você salvou o relatório.  
  
-   Os relatórios podem ser gerenciados e exibidos a partir do Gerenciador de Relatórios.  
  
-   Recursos de relatório, como fontes de dados, imagens e sub-relatórios são armazenados em um local para acesso mais fácil.  
  
-   Os relatórios podem ser entregues a outros usuários por meio de assinaturas.  
  
-   Os relatórios são armazenados de modo seguro no banco de dados do servidor de relatório.  
  
-   As execuções de relatórios podem ser registradas e é possível fornecer informações de desempenho e auditoria.  
  
 O processo de salvar um relatório em um servidor de relatório também é conhecido como publicação de relatório. Quando você salva o relatório, salva apenas a definição de relatório. Sempre que o relatório é executado, seus dados são atualizados e é provável que sejam diferentes da execução anterior do relatório. Para salvar a definição do relatório com os dados, use o recurso de histórico de relatório. Usando esse recurso, você salva uma cópia do relatório com seus dados.  
  

  
##  <a name="ExportingAndSavingReports"></a> Exportando e salvando relatórios  
 Se você tiver um número pequeno de relatórios para arquivar, considere exportar um relatório e salvá-lo como um arquivo. Após exportar um relatório para um aplicativo (como PDF ou Excel), você pode salvá-lo como um arquivo e colocá-lo em um diretório compartilhado protegido na rede. Como alternativa, você poderá carregar um arquivo PDF ou Excel salvo como um item de recurso, se desejar manter todas as cópias de um relatório, independentemente do formato, no banco de dados do servidor de relatório. Para obter mais informações sobre como exportar um relatório, consulte [exportando relatórios &#40;construtor de relatórios e SSRS&#41; ](export-reports-report-builder-and-ssrs.md) e [carregar um arquivo ou relatório &#40;Gerenciador de relatórios&#41;](../reports/upload-a-file-or-report-report-manager.md).  
  

  
##  <a name="UsingFileShareDelivery"></a> Usando entrega de compartilhamento de arquivos  
 Se você tiver um grande número de relatórios a serem arquivados, crie uma assinatura que entrega o relatório diretamente ao sistema de arquivos. Para esta abordagem, você deve criar uma assinatura para cada relatório, escolher uma pasta compartilhada para armazenar os relatórios e definir uma agenda que determine quando o arquivo é criado. Depois de definir uma assinatura, o servidor de relatório pode executar o relatório sem assistência e adicionar arquivos de relatório ao arquivo morto usando a agenda fornecida. Você também poderá criar agendas de uso único, se desejar arquivar relatórios ocasionalmente. Para obter mais informações sobre assinaturas e entrega de compartilhamento de arquivos, consulte "Entrega de arquivos no Reporting Services" na [documentação do Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) nos Manuais Online do SQL Server.  
  

  
##  <a name="UsingReportHistory"></a> Usando histórico de relatório  
 Você também pode usar o recurso de histórico de relatório para criar cópias históricas. Em seguida, é possível fazer backup do banco de dados do servidor de relatório e armazenar o backup em um local seguro para uso futuro. Todo o histórico de relatório (juntamente com relatórios, itens de fontes de dados compartilhadas, pastas, assinaturas e agendas compartilhadas) é armazenado no banco de dados do servidor de relatório. É possível criar um backup para manter uma cópia permanente do histórico de relatório e de metadados, como informações sobre assinatura que indicam os destinatários de um relatório. Para obter mais informações, consulte "Gerenciando o histórico de relatório" na [documentação do Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) nos Manuais Online do SQL Server.  
  

  
##  <a name="HowTo"></a> Tópicos de instruções  
  
-   [Salvar relatórios em um servidor de relatório &#40;Construtor de Relatórios&#41;](save-reports-to-a-report-server-report-builder.md)  
  
-   [Salvar um relatório em uma biblioteca do SharePoint &#40;Construtor de Relatórios&#41;](save-a-report-to-a-sharepoint-library-report-builder.md)  
  
-   [Salvar relatórios em seu computador &#40;construtor de relatórios&#41;](../save-reports-to-your-computer-report-builder.md)  
  

  
## <a name="see-also"></a>Consulte também  
 [Relatórios, partes de relatório e definições de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [Instalar, desinstalar e oferecer suporte ao construtor de relatórios](../install-uninstall-and-report-builder-support.md)   
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Exportando relatórios &#40;relatórios e SSRS&#41;](export-reports-report-builder-and-ssrs.md)   
 [Imprimir relatórios &#40;Construtor de Relatórios e SSRS&#41;](print-reports-report-builder-and-ssrs.md)  
  
  
