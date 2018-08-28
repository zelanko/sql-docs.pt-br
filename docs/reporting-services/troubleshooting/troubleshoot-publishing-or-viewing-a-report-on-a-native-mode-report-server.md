---
title: Solução de problemas ao publicar ou exibir um relatório em um Servidor de Relatório no modo nativo | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: troubleshooting
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: df7720a1-d178-45bb-8d6f-63e208cae7fe
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d38bf935bb79325e4d748c39edaaeb075e8b474e
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2018
ms.locfileid: "40410418"
---
# <a name="troubleshoot-publishing-or-viewing-a-report-on-a-native-mode-report-server"></a>Solução de problemas ao publicar ou exibir um relatório em um Servidor de Relatório no modo nativo
  
  
  
Quando você publica ou carrega um relatório em um servidor de relatório configurado no modo nativo, talvez tenha problemas específicos para exibir relatórios no servidor de relatório. Use este tópico para ajudar a solucionar esses problemas.   
  
## <a name="why-am-i-being-prompted-for-credentials-when-i-publish-a-report"></a>Por que minhas credenciais são solicitadas quando publico um relatório?  
Para implantar um relatório em um servidor de relatório, você deve especificar o endereço do servidor. Talvez você veja a caixa de diálogo de Logon do Reporting Services, que solicita suas credenciais.   
  
O nome do servidor de relatório não foi especificado corretamente  
  
  
Quando você implanta o relatório em um servidor de relatório no modo nativo, um erro comum é especificar o nome da pasta de relatórios, em vez do nome do servidor de relatório.   
  
Verifique se a URL do servidor de relatório é o endereço do servidor de relatório (por exemplo, `http://localhost/reportserver`), e não o endereço do diretório virtual Gerenciador de Relatórios (por exemplo, `http://localhost/reports`). Caso tenha especificado um número de porta para o servidor de relatório diferente do número da porta padrão 80, deverá especificá-lo no endereço do servidor de relatório (por exemplo, `http://localhost:81/reportserver`).   
  
 ## <a name="nothing-happens-when-i-toggle-items-in-my-published-report"></a>Nada acontece quando alterno itens no meu relatório publicado.  
  Quando você exibe um relatório na visualização local, pode alternar os itens no relatório e mostrá-los ou ocultá-los. Quando você exibe o mesmo relatório após publicá-lo no servidor de relatório, o recurso de alternância de itens não funciona mais.   
  
\<report server name> Inclui um sublinhado (_)  
  
Se um relatório for executado sem erros, mas os itens de alternância não funcionam (por exemplo, você clica em um ícone expandir (+) e nada acontece), verifique o nome do computador que está hospedando o servidor de relatório. Se o nome do computador incluir um sublinhado, isso indica que os itens de alternância não estão funcionando. Esse é um problema conhecido. Não há uma solução.   
  
Para executar relatórios com itens de alternância, use um computador cujo nome não tenha caracteres de sublinhado.  
  
## <a name="images-and-charts-do-not-load-when-i-use-run-as-and-a-browser-to-run-my-report"></a>As imagens e os gráficos não são carregados quando eu uso Executar como e um navegador para executar meu relatório.  
Quando você executa o Gerenciador de Relatórios em um contexto de segurança diferente, talvez não veja todos os itens em um relatório.   
  
### <a name="insufficient-permissions-on-internet-temporary-file-folders"></a>Permissões insuficientes na pasta Arquivos Temporários da Internet  
  
Em algumas circunstâncias, quando você usa o Gerenciador de Relatórios para exibir os relatórios publicados que incluem gráficos ou imagens, talvez não os veja. Por exemplo, quando você usa o comando **Executar como** da Microsoft para exibir um relatório usando um contexto de segurança diferente, talvez você não tenha permissão para a pasta em que o servidor de relatório armazena em cache gráficos e imagens como arquivos temporários da Internet.   
  
Verifique se você tem permissão para acessar as pastas que contêm os arquivos em cache.   
    
## <a name="see-also"></a>Consulte Também  
[Suporte ao navegador para Reporting Services e Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)  
[Erros e eventos (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[Solucionar problemas de recuperação de dados com relatórios do Reporting Services](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[Solucionar problemas de assinaturas e entrega do Reporting Services](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

