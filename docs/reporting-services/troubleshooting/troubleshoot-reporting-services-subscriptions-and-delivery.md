---
title: Solução de problemas de assinaturas e entrega do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: troubleshooting
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ae1775f7-9919-48ca-8bd7-cc16df274e2c
caps.latest.revision: 16
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 901e9b6530dcae026ab6f3a4989260ff237c758a
ms.sourcegitcommit: 0ab652fd02039a014c9661f3c5ccf4281cfb025b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "40406666"
---
# <a name="troubleshoot-reporting-services-subscriptions-and-delivery"></a>Solucionar problemas de assinaturas e entrega do Reporting Services
  
    
Use este tópico para solucionar os problemas encontrados ao trabalhar com as assinaturas, agendas e entrega de relatório [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] .  
## <a name="log-information"></a>Informações do log
 
A página Assinatura no [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] inclui um status de uma assinatura, mas se houver um problema com a assinatura, as informações detalhadas estarão nos logs do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] . 
![ssrs_tutorial_datadriven_subscription_status_ReportManager](../../reporting-services/media/ssrs-tutorial-datadriven-subscription-status-reportmanager.png)

**Logs de rastreamento:** os logs de rastreamento são gravados de arquivos de texto: `\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles`

Veja a seguir um exemplo de entrada de log:

```
   subscription WindowsService_10   4c7c    05/24/2016-01:05:06  e ERROR     Failure writing file \\ServerName\SalesReports\so71949.xls : Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareProvider+NetworkErrorException: An impersonation error occurred using the security context of the current user. ---> System.ArgumentException: Value does not fall within the expected range.  05/24/2016
```
Para obter mais informações sobre os logs de rastreamento do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , consulte: 
+ [Log de rastreamento do Servidor de Relatório](../../reporting-services/report-server/report-server-service-trace-log.md).
+ [Arquivos de log do Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).

**Exibições de log de execução:**

Os logs de execução são exibições no banco de dados SQL ReportServer para obter mais informações sobre [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , consulte [Exibições ExecutionLog e ExecutionLog3 do Reporting Services](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  

----------
## <a name="unable-to-send-reports-using-e-mail-with-windows-server-2003-and-pop3"></a>Não é possível enviar relatórios por email com o Windows Server 2003 e POP3  
Se você estiver executando um aplicativo de email com o POP3 (Post Office Protocol, versão 3) no Microsoft Windows Server 2003, talvez não seja possível enviar relatórios usando o servidor POP3 local. Se o servidor de relatório estiver configurado para enviar email com o Servidor POP3 local e criar uma assinatura que envie um relatório, talvez a seguinte mensagem de erro seja exibida:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`Failure sending mail: <error message>`  
  
em que \<error message> é substituído pelas informações de mensagem de erro adicionais retornadas do CDO (Collaboration Data Objects).  
  
### <a name="to-resolve-this-problem"></a>Para resolver esse problema:  
* Defina o valor do elemento `SendUsing` no arquivo **Rsreportserver. config** para 1.  
* Limpe o valor da propriedade `SMTPServer` para que ele fique vazio. Também será necessário fornecer um valor para a propriedade `SMTPServerPickupDirectory` .   
  
Para obter mais informações sobre como usar um serviço de SMTP local para a entrega de relatórios por email, consulte Configurando um Servidor de Relatório para a Entrega por EMail.  
  
## <a name="failure-sending-mail-the-server-rejected-the-sender-address-the-server-response-was-454-573-client-does-not-have-permission-to-submit-mail-to-this-server"></a>Falha ao enviar email: o servidor rejeitou o endereço do remetente. A resposta do servidor era: 454 5.7.3 Cliente não tem permissão para enviar email para este servidor  
Esse erro ocorre quando as configurações da política de segurança no servidor SMTP permitem que somente usuários autenticados enviem email para entrega posterior. Se o servidor SMTP não aceitar envios de email de usuários anônimos, consulte o administrador do sistema para saber como obter permissão para usar o servidor.  
> Esse erro também pode ocorrer quando você especifica um nome de servidor do Exchange como a Servidor SMTP. Para usar um servidor do Exchange para entrega de email, é necessário especificar o nome do gateway do SMTP configurado para o servidor do Exchange. Consulte o administrador do Exchange para obter informações a respeito.  
  
## <a name="subscriptions-are-not-processing"></a>As assinaturas não estão processando  
Assinaturas podem falhar sob estas condições.   
* A agenda usada para acionar o relatório expirou. Para assinaturas que disparam de uma atualização de instantâneo de relatório, a agenda usada para atualizar o instantâneo talvez tenha expirado.  
  
* O servidor de relatório, o SQL Server Agent ou o aplicativo de servidor de email não está em execução.  
* O relatório não pode ser entregue (por ser muito grande, por exemplo). Para determinar se a entrega está falhando devido ao tamanho do relatório, salve o relatório em um arquivo e depois envie o email novamente. Certifique-se de escolher o mesmo formato de renderização especificado na assinatura. Se um erro de entrega for exibido, use a extensão de entrega do Compartilhamento de Arquivo em vez do Email do Servidor de Relatório.  
* O computador usado para a entrega do compartilhamento de arquivo não está sendo executado ou foi configurado para acesso do tipo somente leitura.  
* A extensão de entrega especificada na assinatura foi desinstalada ou desabilitada.  
* As configurações de credencial foram alteradas de valores armazenados para valores integrados ou solicitados.  
* O nome de um parâmetro ou tipo de dados foi alterado na definição do relatório e o relatório foi republicado. Se uma assinatura incluir um parâmetro que não seja mais válido, ela se tornará inativa.  
  
Para obter mais informações, consulte a [Solução de problemas e erros com o Reporting Services](http://social.technet.microsoft.com/wiki/contents/articles/1633.ssrs-troubleshoot-issues-and-errors-with-reporting-services.aspx)no TechNet Wiki.  
  
  
    
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

