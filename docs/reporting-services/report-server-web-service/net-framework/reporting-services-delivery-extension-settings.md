---
title: Configurações de extensão de entrega do Reporting Services | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- XML Web service [Reporting Services], delivery extension settings
- Report Server Web service, delivery extension settings
- delivery [Reporting Services]
- network share delivery [Reporting Services]
- file share delivery [Reporting Services]
- e-mail [Reporting Services]
- mailing reports [Reporting Services]
- sharing reports
- extensions [Reporting Services], delivery
- mail [Reporting Services]
- Web service [Reporting Services], delivery extension settings
ms.assetid: 68c31a85-261c-4ec4-b8df-1f9842b46f8a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b801fc7ada9e370d12388ba341259f1c13c7a0f6
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "63128847"
---
# <a name="reporting-services-delivery-extension-settings"></a>Configurações da extensão de entrega do Reporting Services
  O [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] inclui uma extensão de entrega de email e uma extensão de entrega de compartilhamento de arquivos. A entrega de email oferece um modo de enviar um relatório a usuários individuais ou a grupos por email. A entrega de compartilhamento de arquivo permite que você envie automaticamente relatórios renderizados para um compartilhamento em sua rede. Você pode usar qualquer uma das duas extensões de entrega suportadas com assinaturas padrão ou assinaturas controladas por dados. Você passa as configurações de entrega específicas ao tipo de extensão de entrega sempre que chama os métodos <xref:ReportService2010.ReportingService2010.CreateSubscription%2A>, <xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A>, <xref:ReportService2010.ReportingService2010.SetSubscriptionProperties%2A> e <xref:ReportService2010.ReportingService2010.SetDataDrivenSubscriptionProperties%2A>. Para recuperar uma lista de configurações de entrega programaticamente, use o método <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A>.  
  
> [!NOTE]  
>  As configurações de extensão de entrega fazem diferenciação de maiúsculas e minúsculas.  
  
## <a name="e-mail-delivery-settings"></a>Configurações de entrega de email  
 A tabela a seguir lista as configurações de entrega de email para assinaturas que usam o email do servidor de relatório.  
  
|Configuração|Valor|  
|-------------|-----------|  
|**TO**|O endereço de email exibido na linha **To** da mensagem de email. Vários endereços de email são separados por ponto-e-vírgulas. Obrigatórios.|  
|**CC**|O endereço de email exibido na linha **Cc** da mensagem de email. Vários endereços de email são separados por ponto-e-vírgulas. Opcional.|  
|**BCC**|O endereço de email exibido na linha **Bcc** da mensagem de email. Vários endereços de email são separados por ponto-e-vírgulas. Opcional.|  
|**ReplyTo**|O endereço de email exibido no cabeçalho **Reply-To** da mensagem de email. O valor deve ser um único endereço de email. Opcional.|  
|**IncludeReport**|Um valor que indica se será preciso incluir o relatório na entrega do email. Um valor igual a **true** indica que o relatório é entregue no corpo da mensagem de email.|  
|**RenderFormat**|O nome da extensão de renderização a ser usado na geração do relatório renderizado. O nome deve corresponder a uma das extensões de renderização visíveis instaladas no servidor de relatório. Esse valor é necessário se a configuração **IncludeReport** é definida como um valor igual a **true**.|  
|**Prioridade**|A prioridade com que a mensagem é enviada. Os valores válidos são **LOW**, **NORMAL** e **HIGH**. O valor padrão é **NORMAL**.|  
|**Assunto**|O texto da linha de assunto da mensagem.|  
|**Comentário**|O texto incluído no corpo da mensagem.|  
|**IncludeLink**|Um valor que indica se será preciso incluir um link para o relatório no corpo do email.|  
  
## <a name="file-share-delivery-settings"></a>Configurações de entrega de compartilhamento de arquivo  
 A tabela a seguir lista as configurações de entrega de compartilhamento de arquivo para assinaturas.  
  
|Configuração|Valor|  
|-------------|-----------|  
|**FILENAME**|O nome do arquivo salvo no disco.|  
|**FILEEXTN**|Indica se será preciso incluir uma extensão de arquivo para o relatório renderizado. O valor é **true** ou **false**.|  
|**PATH**|O caminho de pasta ou o caminho do compartilhamento de arquivo UNC nos quais salvar o relatório.|  
|**RENDER_FORMAT**|O formato do relatório salvo no disco.|  
|**USERNAME**|O nome de usuário exigido para o acesso ao recurso de rede ou disco.|  
|**PASSWORD**|A senha exigida para o acesso ao recurso de rede ou disco.|  
|**WRITEMODE**|O modo de gravação a ser usado durante o acesso ao disco. Os valores válidos são **None**, **Overwrite** e **AutoIncrement**.|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência técnica &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)   
 [Compilar aplicativos usando o Serviço Web e o .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
