---
title: Monitorar assinaturas do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: subscriptions
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], inactive
- subscriptions [Reporting Services], status
- monitoring [Reporting Services], subscriptions
- status information [Reporting Services]
- inactive subscriptions [Reporting Services]
ms.assetid: 054c4a87-60bf-4556-9a8c-8b2d77a534e6
caps.latest.revision: 36
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1b81bf16cc4f9352da7b0a4c37cac91dd73f5eff
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="monitor-reporting-services-subscriptions"></a>Monitorar assinaturas do Reporting Services
  Você pode monitorar assinaturas [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] da interface do usuário, do Windows PowerShell ou arquivos de log. As opções disponíveis para monitoramento dependem de qual modo de servidor de relatório está em execução.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo do SharePoint.|  
  
 **Neste tópico:**  
  
-   [Interface do usuário de modo nativo](#bkmk_native_mode)  
  
-   [Modo do SharePoint](#bkmk_sharepoint_mode)  
  
-   [Use o PowerShell para monitorar assinaturas](#bkmk_use_powershell)  
  
-   [Gerenciando assinaturas inativas](#bkmk_manage_inactive)  
  
##  <a name="bkmk_native_mode"></a> Interface do usuário de modo nativo  
 Usuários individuais [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podem monitorar o status de uma assinatura usando a página **Minhas assinaturas** ou a guia **Assinaturas** no Gerenciador de relatórios. As páginas de assinatura incluem colunas que indicam quando a assinatura foi executada pela última vez e seu status. As mensagens de status são atualizadas quando a assinatura é agendada para ser processada. Se o gatilho nunca ocorrer (por exemplo, um instantâneo de execução de relatório nunca for atualizado ou um agendamento nunca ocorrer), a mensagem de status não será atualizada.  
  
 A tabela a seguir descreve os possíveis valores para a coluna **Status** .  
  
|Status|Description|  
|------------|-----------------|  
|Nova assinatura|Aparece quando você cria a assinatura.|  
|Inativa|Aparece quando uma assinatura não pode ser processada. Para obter mais informações, consulte "Gerenciando assinaturas inativas" posteriormente neste tópico.|  
|Concluído: \<*number*> processados de um total de \<*number*>; \<*number*> erros.|Mostra o status de uma execução de assinatura controlada por dados; essa mensagem é proveniente do Processador de Agendamento e Entrega.|  
|\<*number*> processados|O número de notificações que o Processador de Agendamento e Entrega entregou com êxito ou que não está mais tentando entregar. Quando uma entrega controlada por dados for concluída, o número de notificações processadas deve ser igual ao número total de notificações geradas.|  
|\<*number*> total|O número total de notificações geradas para a última entrega para a assinatura.|  
|\<*number*> erro|O número de notificações que o Processador de Agendamento e Entrega não pôde entregar ou que não está mais tentando entregar.|  
|Falha ao enviar mensagem: falha no transporte ao se conectar ao servidor.|Indica que o servidor de relatório não se conectou ao servidor de email; essa mensagem é emitida pela extensão de entrega de email.|  
|O arquivo \<*filename*> foi gravado em \<path>.|Indica que a entrega no local de compartilhamento de arquivos teve êxito; esta mensagem é emitida pela extensão de entrega do compartilhamento de arquivos.|  
|Erro desconhecido ao gravar o arquivo.|Indica que a entrega no local de compartilhamento de arquivos não teve êxito; esta mensagem é emitida pela extensão de entrega do compartilhamento de arquivos.|  
|Falha ao conectar-se à pasta de destino, \<path>. Verifique se a pasta de destino ou o compartilhamento de arquivos existe.|Indica que a pasta especificada não foi localizada; esta mensagem é emitida pela extensão de entrega do compartilhamento de arquivos.|  
|O arquivo \<filename> não pôde ser gravado em \<path>. Tentando repetir.|Indica que o arquivo não pôde ser atualizado com uma versão mais recente; esta mensagem é emitida pela extensão de entrega do compartilhamento de arquivos.|  
|Falha ao gravar o arquivo \<filename>: \<message>|Indica que a entrega no local de compartilhamento de arquivos não teve êxito; esta mensagem é emitida pela extensão de entrega do compartilhamento de arquivos.|  
|\<custom status messages>|Mensagens de status sobre êxito e falha de entrega, fornecidas pelas extensões de entrega. Se você estiver usando uma extensão de entrega personalizada ou de terceiros, poderão ser fornecidas mensagens de status adicionais.|  
  
 Os administradores de servidor de relatório também podem monitorar assinaturas padrão que estão sendo processadas no momento. As assinaturas controladas por dados não podem ser monitoradas. Para obter mais informações, consulte [Gerenciar um processo em execução](../../reporting-services/subscriptions/manage-a-running-process.md).  
  
 Se uma assinatura não puder ser entregue (por exemplo, se o servidor de email não estiver disponível), a extensão de entrega repete a entrega. Uma configuração especifica o número de tentativas que serão feitas. O valor padrão é nenhuma tentativa. Em alguns casos, o relatório pode ter sido processado sem dados (por exemplo, se a fonte de dados estiver offline). Nesse caso, o texto sobre isso é fornecido no corpo da mensagem.  
  
### <a name="native-mode-log-files"></a>Arquivos de log de modo nativo  
 Se ocorrer um erro durante a entrega, será inserida uma entrada no log de rastreamento do servidor de relatório.  
  
 Os administradores do servidor de relatório podem examinar os arquivos **reportserverservice_\*.log** para determinar o status da entrega de assinatura. Para entrega de email, os arquivos de log do servidor de relatórios incluem um registro do processamento e das entregas para contas de email específicas. Este é o local padrão dos arquivos de log:  
  
 `C:\Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\LogFiles`  
  
 A seguir, é mostrado nome de arquivo de log de exemplo:  
  
 `ReportServerService__05_21_2014_00_05_07.log`  
  
 Esta é uma mensagem de erro de exemplo do arquivo de log de rastreamento, relacionada a assinaturas:  
  
-   library!WindowsService_7!b60!05/20/2014-22:34:36:: i INFO: Inicializando EnableExecutionLogging como 'True' conforme especificado no sistema do Servidor properties.emailextension!WindowsService_7!b60!05/20/2014-22:34:41:: e ERROR: **Erro ao enviar email**. Exceção: System.Net.Mail.SmtpException: o servidor SMTP requer uma conexão segura ou o cliente não foi autenticado. A resposta do servidor foi: o cliente 5.7.1 não foi autenticado em System.Net.Mail.MailCommand.CheckResponse(SmtpStatusCode statusCode, String response)  
  
 O arquivo de log não informa se o relatório foi aberto ou se a entrega teve êxito realmente. Entrega bem-sucedida significa que não houve erros gerados pelo Processador de Agendamento e Entrega e que o servidor de relatório se conectou ao servidor de email. Se o email resultou em um erro de mensagem que não pode ser entregue na caixa de correio do usuário, essa informação não será incluída no arquivo de log. Para obter mais informações sobre arquivos de log, consulte [Fontes e arquivos de log do Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).  
  
##  <a name="bkmk_sharepoint_mode"></a> Modo do SharePoint  
 Para monitorar uma assinatura no modo do SharePoint: o status da assinatura pode ser monitorado na página **Gerenciar Assinaturas** .  
  
1.  navegue até a biblioteca de documentos que contém o relatório  
  
2.  Abra o menu de contexto do relatório (**…**).  
  
3.  Selecione a opção de menu expandido (**…**).  
  
4.  Selecione **Gerenciar assinaturas**  
  
### <a name="sharepoint-uls-log-files"></a>Arquivos de log do SharePoint ULS  
 As informações relacionadas a assinaturas são gravadas no log do SharePoint ULS. Para obter mais informações sobre como configurar eventos [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para o log do ULS, consulte [Ativar eventos do Reporting Services para o log de rastreamento do SharePoint &#40;ULS&#41;](../../reporting-services/report-server/turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md).  A seguir está um exemplo de entrada de log ULS relacionado a assinaturas [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
||||||||  
|-|-|-|-|-|-|-|  
|data|Processar|Área|Categoria|Nível|Correlation|Mensagem|  
|5/21/2014 14:34:06:15|Pool de Aplicativos: a0ba039332294f40bc4a81544afde01d|SQL Server Reporting Services|Extensão de email do servidor de relatório|Inesperado|(vazio)|**Erro ao enviar email.** Exceção: System.Net.Mail.SmtpException: caixa de correio indisponível. A resposta do servidor foi: o cliente 5.7.1 não tem permissões para enviar como esse remetente no System.Net.Mail.DataStopCommand.CheckResponse(SmtpStatusCode statusCode, String serverResponse) em System.Net.Mail.DataStopCommand.Send(SmtpConnection conn) em System.Net.Mail.SmtpClient.Send(MailMessage message) em Microsoft.ReportingServices.EmailDeliveryProvider.EmailProvider.Deliver(Notification notification)|  
  
##  <a name="bkmk_use_powershell"></a> Use o PowerShell para monitorar assinaturas  
 Por exemplo, scripts do PowerShell que você pode usar para verificar o status do modo nativo ou assinaturas de modo do SharePoint, consulte [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md).  
  
##  <a name="bkmk_manage_inactive"></a> Gerenciando assinaturas inativas  
 Se uma assinatura se tornar inativa, você deverá excluí-la ou reativá-la resolvendo as condições subjacentes que impedem que ela seja processada. As assinaturas podem se tornar inativas se ocorrerem condições que impeçam o processamento. Essas condições incluem:  
  
-   Remoção ou desinstalação da extensão de entrega especificada na assinatura.  
  
-   Alteração das configurações de credencial de valores armazenados para valores integrados ou solicitados.  
  
-   Alteração do nome de um parâmetro ou tipo de dados na definição do relatório e, em seguida, a republicação de um relatório. Se uma assinatura incluir um parâmetro que não seja mais válido, ela se tornará inativa.  
  
-   Alteração do modo de execução de um relatório (por exemplo, modificando um relatório sob demanda para que ele seja executado como um instantâneo de execução do relatório). Para obter mais informações, consulte [Definir as propriedades do processamento de relatórios](../../reporting-services/report-server/set-report-processing-properties.md).  
  
 Uma assinatura inativa é indicada por uma mensagem na própria assinatura. A mensagem inclui informações sobre a causa e quais etapas você deveria executar para reativar a assinatura.  
  
 Quando as condições fazem com que a assinatura se torne inativa, a assinatura reflete esse fato quando o servidor de relatório executa a assinatura. Se uma assinatura for agendada para entregar um relatório todas as sextas-feiras às 2 da manhã, e a extensão da entrega usada foi desinstalada às segundas-feiras às 9 da manhã, a assinatura não refletirá seu estado inativo até sexta-feira às 2 da manhã.  
  
## <a name="see-also"></a>Consulte Também  
 [old_Crie e gerencie assinaturas de servidores de relatório no modo nativo](http://msdn.microsoft.com/en-us/7f46cbdb-5102-4941-bca2-5e0ff9012c6b)   
 [Assinaturas e entrega &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)  
  
  
