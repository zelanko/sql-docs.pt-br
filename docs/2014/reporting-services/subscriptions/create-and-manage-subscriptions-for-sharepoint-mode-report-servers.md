---
title: Criar e gerenciar assinaturas de servidores de relatório no modo do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], creating
- subscriptions [Reporting Services], deleting
- subscriptions [Reporting Services], managing
ms.assetid: 44be7ee2-33ce-46e4-9d1a-a20aaf43a227
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f8439c48f7379b983b46edcaf1111606c1a3fbcc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48193196"
---
# <a name="create-and-manage-subscriptions-for-sharepoint-mode-report-servers"></a>Criar e gerenciar assinaturas de servidores de relatório no modo SharePoint
  Você pode criar assinaturas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para entregar relatórios de um aplicativo Web do SharePoint que esteja integrado com um servidor de relatório no modo do SharePoint. As assinaturas podem entregar relatórios a uma biblioteca de documentos, pasta de arquivo ou como email. Este tópico resume os requisitos e as etapas para criar uma assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo do SharePoint &#124; SharePoint 2010 e SharePoint 2013|  
  
 Ao criar uma assinatura, há três modos para especificar sua entrega:  
  
-   **Biblioteca de documentos**: você pode criar uma assinatura que entregue um documento baseado no relatório original para uma biblioteca no mesmo site do SharePoint que o relatório original. Não é possível entregar o documento para uma biblioteca em outro servidor ou outro site na mesma coleção de sites. Para entregar o documento, você deve ter a permissão Adicionar Itens na biblioteca na qual o relatório será entregue.  
  
-   **Pasta de arquivos:** você pode entregar um documento baseado no relatório original para uma pasta compartilhada no sistema de arquivos. Você deve selecionar uma pasta existente que possa ser acessada por uma conexão de rede.  
  
-   **Email:** se o servidor de relatório estiver configurado para usar a extensão de entrega de Email do Servidor de Relatório, você poderá criar uma assinatura que envia um relatório ou um arquivo de relatório exportado (salvo em um formato de saída) para sua caixa de entrada. Para receber apenas a notificação sem o relatório ou a URL do mesmo, desmarque as caixas de seleção **Incluir um link no relatório** e **Mostrar relatório dentro da mensagem** .  
  
 **Neste tópico:**  
  
-   [Requisitos gerais para assinaturas](#bkmk_subscription_requirements)  
  
-   [Para criar uma assinatura para entregar um relatório a uma biblioteca do SharePoint.](#bkmk_tosharepoint_library)  
  
-   [Para criar uma assinatura para entregar um relatório a uma biblioteca do SharePoint.](#bkmk_tosharepoint_library)  
  
-   [Para criar uma assinatura para a entrega de email do servidor de relatório](#bkmk_subscription_for_email)  
  
-   [Para exibir ou modificar uma assinatura](#bkmk_to_modify_subscription)  
  
-   [Para excluir uma assinatura](#bkmk_to_delete_subscription)  
  
##  <a name="bkmk_subscription_requirements"></a> Requisitos gerais para assinaturas  
 Para criar uma assinatura, o relatório deve usar credenciais armazenadas e você deve ter permissão para exibir o relatório e criar alertas.  
  
 Quando você cria uma assinatura, pode selecionar um formato de arquivo de saída. Nem todo relatório funciona bem em qualquer formato. Antes de selecionar o formato de uma assinatura, abra o relatório e exporte-o em formatos diferentes para verificar se ele é exibido como esperado.  
  
 Os usuários precisam da permissão de lista **Editar Itens** no SharePoint se quiserem criar assinaturas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte [Referência à permissão de sites e listas para itens do servidor de relatório](../security/sharepoint-site-and-list-permission-reference-for-report-server-items.md).  
  
> [!IMPORTANT]  
>  Uma assinatura que entrega um relatório a uma biblioteca ou uma pasta compartilhada cria um novo arquivo estático baseado no relatório original, mas que não é uma definição de relatório verdadeira executada na Web Part do Visualizador de Relatórios. Se o relatório original tiver recursos interativos (por exemplo, links de detalhamento) ou conteúdo dinâmico, esses recursos não ficarão disponíveis no arquivo estático entregue no local de destino. Se você selecionar uma “página da Web”, poderá preservar alguma interatividade, mais, como o documento não é um arquivo .rdl executado no Visualizador de Relatórios, clicar em um relatório criará novas páginas na sessão do navegador que devem ser percorridas para voltar ao site.  
  
 Não é possível renomear a extensão do nome de arquivo de um relatório exportado para .rdl e executá-lo na Web Part do Visualizador de Relatórios. Se quiser criar uma assinatura que forneça um relatório real, use a extensão de entrega Email do servidor de relatório e defina opções para incluir um link ao relatório.  
  
 As configurações de versão na biblioteca que contém o documento entregue determinam se uma nova versão do documento será criada em cada entrega. Por padrão, as configurações de versão estão habilitadas para cada biblioteca. A menos que você escolha especificamente **Nenhuma versão**, uma nova versão principal do documento será criada na entrega. Somente versões principais do documento são criadas; as versões secundárias nunca são criadas em resultado da entrega de uma assinatura, mesmo que você selecione uma opção de versão que permita versões secundárias. Se o número de versões principais a ser mantido for limitado, as entregas mais antigas serão substituídas por entregas mais novas quando o limite máximo for atingido.  
  
 Os formatos de saída selecionados para uma assinatura são baseados nas extensões de renderização instaladas no servidor de relatório. Você só pode selecionar formatos de saída com suporte nas extensões de renderização no servidor de relatório.  
  
###  <a name="bkmk_tosharepoint_library"></a> Para criar uma assinatura para entregar um relatório a uma biblioteca do SharePoint.  
  
1.  Navegue para uma biblioteca do SharePoint que contém o relatório.  
  
2.  Clique na seta para baixo ao lado do relatório e, sem seguida, selecione **Gerenciar Assinaturas**.  
  
3.  Clique em **Adicionar Assinatura**.  
  
4.  Em **Extensão de Entrega**, selecione **Bibliotecas de Documentos SharePoint**.  
  
5.  Em **Biblioteca de Documentos**, selecione uma biblioteca no mesmo site.  
  
6.  Em **Opções de Arquivo**, especifique o nome do arquivo e o título do documento que será criado pela assinatura.  
  
7.  Em **Formato de Saída**, selecione o formato de aplicativo.  
  
     O formato Arquivo da Web (MHTML) é o padrão porque produz um arquivo HTML autossuficiente, mas não preserva os recursos de relatório interativos que podem estar no relatório original.  
  
8.  Em **Opções de Substituição**, especifique uma opção que determina se as entregas subsequentes substituem um arquivo. Se desejar preservar as entregas anteriores, selecione **Criar arquivo com nome exclusivo**. Um número será anexado aos novos arquivos para criar um nome de arquivo exclusivo.  
  
9. Em **Evento de Entrega**, especifique uma agenda ou um evento que cause a execução da assinatura. Você pode criar uma agenda personalizada, selecionar uma agenda compartilhada, se disponível, ou executar a assinatura sempre que os dados forem atualizados em um relatório executado com dados de instantâneo. Para obter mais informações sobre agendamentos e processamento de dados, consulte [Definir opções de processamento &#40;Reporting Services no modo integrado do SharePoint&#41;](../set-processing-options-reporting-services-in-sharepoint-integrated-mode.md).  
  
10. Em **Parâmetros**, caso você esteja criando uma assinatura para um relatório com parâmetros, especifique os valores que deseja usar com o relatório quando a assinatura for processada. A seção de parâmetros não está visível nessa página se o relatório selecionado não contém parâmetros. Para obter mais informações sobre parâmetros, consulte [Definir parâmetros em um relatório publicado &#40;Reporting Services no modo integrado do SharePoint&#41;](../report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).  
  
###  <a name="bkmk_subscription_for_sharedfolder"></a> Para criar uma assinatura para entrega de pasta compartilhada  
  
1.  Navegue para uma biblioteca do SharePoint que contém o relatório.  
  
2.  Clique na seta para baixo ao lado do relatório e, sem seguida, selecione **Gerenciar Assinaturas**.  
  
3.  Clique em **Adicionar Assinatura**.  
  
4.  Em **Extensão de Entrega**, selecione **Compartilhamento de Arquivos do Windows**.  
  
5.  Em **Nome do Arquivo**, digite o nome do arquivo que será criado na pasta compartilhada.  
  
6.  Em **Caminho**, insira um caminho da pasta no formato UNC que inclua o nome de rede do computador. Não inclua barras invertidas à direita no caminho da pasta. Um exemplo de caminho é `\\ComputerName01\Public\MyReports`, onde Public e MyReports são pastas compartilhadas.  
  
7.  Em **Formato de Renderização**, selecione o formato de aplicativo do relatório.  
  
8.  Em **Modo de Gravação**, escolha entre **Nenhum**, **AutoIncrementar**ou **Substituir**. Essas opções determinam se as entregas subsequentes substituem um arquivo. Se desejar preservar as entregas anteriores, escolha **AutoIncrementar**. Um número será anexado aos novos arquivos para criar um nome de arquivo exclusivo. Se você escolher **Nenhum**, nenhuma entrega ocorrerá se já houver um arquivo com o mesmo nome no local de destino.  
  
9. Em **Extensão do Arquivo**, escolha **Verdadeiro** para adicionar uma extensão de nome de arquivo que corresponda ao formato de arquivo do aplicativo ou Falso para criar um arquivo sem uma extensão.  
  
10. Em **Nome de Usuário** e **Senha**, digite as credenciais com permissão para gravar na pasta compartilhada.  
  
11. Em **Evento de Entrega**, especifique uma agenda ou um evento que cause a execução da assinatura. Você pode criar uma agenda personalizada, selecionar uma agenda compartilhada, se disponível, ou executar a assinatura sempre que os dados forem atualizados em um relatório executado com dados de instantâneo. Para obter mais informações sobre agendamentos e processamento de dados, consulte [Definir opções de processamento &#40;Reporting Services no modo integrado do SharePoint&#41;](../set-processing-options-reporting-services-in-sharepoint-integrated-mode.md).  
  
12. Em **Parâmetros**, caso você esteja criando uma assinatura para um relatório com parâmetros, especifique os valores que deseja usar com o relatório quando a assinatura for processada. Para obter mais informações sobre parâmetros, consulte [Definir parâmetros em um relatório publicado &#40;Reporting Services no modo integrado do SharePoint&#41;](../report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).  
  
###  <a name="bkmk_subscription_for_email"></a> Para criar uma assinatura para a entrega de email do servidor de relatório  
  
1.  Navegue para uma biblioteca do SharePoint que contém o relatório.  
  
2.  Clique na seta para baixo ao lado do relatório e, sem seguida, selecione **Gerenciar Assinaturas**.  
  
3.  Clique em **Adicionar Assinatura**.  
  
4.  Em **Extensão de Entrega**, selecione **Email**.  
  
5.  Em **Opções de Entrega**, especifique um endereço de email para o qual o relatório será enviado.  
  
6.  Opcionalmente, você pode modificar a linha Assunto. A linha Assunto usa parâmetros internos que capturam o nome do relatório e o horário em que foi processado. Esses são os únicos parâmetros internos que podem ser usados. Os parâmetros são espaços reservados que personalizam o texto exibido na linha Assunto, mas você pode substituí-los por texto estático.  
  
7.  Escolha **Incluir um link no relatório** se desejar inserir uma URL de relatório no corpo da mensagem.  
  
8.  Em **Conteúdo do Relatório**, especifique se deseja inserir o relatório no corpo da mensagem.  
  
     O formato de renderização e o navegador determinam se o relatório será inserido ou anexado. Se o navegador oferecer suporte a HTML 4.0 e MHTML, e você selecionar o formato de renderização de arquivo da Web, o relatório será inserido como parte da mensagem. Todos os outros formatos de renderização (CSV, PDF etc.) entregam os relatórios como anexos. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não verifica o tamanho do anexo ou mensagem antes de enviar o relatório. Se o anexo ou a mensagem exceder o limite máximo permitido pelo servidor de email, o relatório não será entregue. Escolha uma das outras opções de entrega (por exemplo, URL ou notificação) para relatórios grandes.  
  
9. Em **Evento de Entrega**, especifique uma agenda ou um evento que cause a execução da assinatura. Você pode criar uma agenda personalizada, selecionar uma agenda compartilhada, se disponível, ou executar a assinatura sempre que os dados forem atualizados em um relatório executado com dados de instantâneo. Para obter mais informações sobre agendamentos e processamento de dados, consulte [Definir opções de processamento &#40;Reporting Services no modo integrado do SharePoint&#41;](../set-processing-options-reporting-services-in-sharepoint-integrated-mode.md).  
  
10. Em **Parâmetros**, caso você esteja criando uma assinatura para um relatório com parâmetros, especifique os valores que deseja usar com o relatório quando a assinatura for processada. Para obter mais informações sobre parâmetros, consulte [Definir parâmetros em um relatório publicado &#40;Reporting Services no modo integrado do SharePoint&#41;](../report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).  
  
###  <a name="bkmk_to_modify_subscription"></a> Para exibir ou modificar uma assinatura  
  
1.  Navegue para uma biblioteca do SharePoint que contém o relatório.  
  
2.  Clique na seta para baixo ao lado do relatório e, sem seguida, clique em **Gerenciar Assinaturas**.  
  
3.  Cada assinatura é identificada pelo tipo de entrega. Clique no tipo de assinatura para exibir e alterar as propriedades existentes.  
  
###  <a name="bkmk_to_delete_subscription"></a> Para excluir uma assinatura  
  
1.  Navegue para uma biblioteca do SharePoint que contém o relatório.  
  
2.  Clique na seta para baixo ao lado do relatório e, sem seguida, clique em **Gerenciar Assinaturas**.  
  
3.  Clique na caixa de seleção próxima à assinatura e clique em **Excluir**.  
  
## <a name="see-also"></a>Consulte também  
 [Assinaturas e entrega de &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [Entrega de email no Reporting Services](e-mail-delivery-in-reporting-services.md)   
 [File Share Delivery in Reporting Services](file-share-delivery-in-reporting-services.md)   
 [Entrega da biblioteca do SharePoint no Reporting Services](sharepoint-library-delivery-in-reporting-services.md)   
 [Configurar um servidor de relatório para entrega de email &#40;Configuration Manager do SSRS&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
  
  
