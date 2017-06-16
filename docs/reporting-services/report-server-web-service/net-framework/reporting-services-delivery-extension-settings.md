---
title: "Reporting Services as configurações de extensão de entrega | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
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
caps.latest.revision: 36
author: sabotta
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 668c3d31af5f287d7d254c2dc666e20a5f6328fa
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="reporting-services-delivery-extension-settings"></a>Configurações da extensão de entrega do Reporting Services
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]inclui uma extensão de entrega de email e uma extensão de entrega de compartilhamento de arquivos. A entrega de email oferece um modo de enviar um relatório a usuários individuais ou a grupos por email. A entrega de compartilhamento de arquivo permite que você envie automaticamente relatórios renderizados para um compartilhamento em sua rede. Você pode usar qualquer uma das duas extensões de entrega suportadas com assinaturas padrão ou assinaturas controladas por dados. Você passa as configurações de entrega específicas ao tipo de extensão de entrega sempre que chama os métodos <xref:ReportService2010.ReportingService2010.CreateSubscription%2A>, <xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A>, <xref:ReportService2010.ReportingService2010.SetSubscriptionProperties%2A> e <xref:ReportService2010.ReportingService2010.SetDataDrivenSubscriptionProperties%2A>. Para recuperar uma lista de configurações de entrega programaticamente, use o método <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A>.  
  
> [!NOTE]  
>  As configurações de extensão de entrega fazem diferenciação de maiúsculas e minúsculas.  
  
## <a name="e-mail-delivery-settings"></a>Configurações de entrega de email  
 A tabela a seguir lista as configurações de entrega de email para assinaturas que usam o email do servidor de relatório.  
  
|Configuração|Valor|  
|-------------|-----------|  
|**PARA**|O endereço de email que aparece no **para** linha da mensagem de email. Vários endereços de email são separados por ponto-e-vírgulas. Obrigatórios.|  
|**CC**|O endereço de email que aparece no **Cc** linha da mensagem de email. Vários endereços de email são separados por ponto-e-vírgulas. Opcional.|  
|**CCO**|O endereço de email que aparece no **Cco** linha da mensagem de email. Vários endereços de email são separados por ponto-e-vírgulas. Opcional.|  
|**ReplyTo**|O endereço de email que aparece no **responder** cabeçalho da mensagem de email. O valor deve ser um único endereço de email. Opcional.|  
|**IncludeReport**|Um valor que indica se será preciso incluir o relatório na entrega do email. Um valor de **true** indica que o relatório será entregue no corpo da mensagem de email.|  
|**RenderFormat**|O nome da extensão de renderização a ser usado na geração do relatório renderizado. O nome deve corresponder a uma das extensões de renderização visíveis instaladas no servidor de relatório. Esse valor é necessário se o **IncludeReport** configuração é definida como um valor de **true**.|  
|**Prioridade**|A prioridade com que a mensagem é enviada. Os valores válidos são **baixo**, **NORMAL**, e **alta**. O valor padrão é **NORMAL**.|  
|**Assunto**|O texto da linha de assunto da mensagem.|  
|**Comentário**|O texto incluído no corpo da mensagem.|  
|**IncludeLink**|Um valor que indica se será preciso incluir um link para o relatório no corpo do email.|  
  
## <a name="file-share-delivery-settings"></a>Configurações de entrega de compartilhamento de arquivo  
 A tabela a seguir lista as configurações de entrega de compartilhamento de arquivo para assinaturas.  
  
|Configuração|Valor|  
|-------------|-----------|  
|**NOME DE ARQUIVO**|O nome do arquivo salvo no disco.|  
|**FILEEXTN**|Indica se será preciso incluir uma extensão de arquivo para o relatório renderizado. O valor é **true** ou **false**.|  
|**CAMINHO**|O caminho de pasta ou o caminho do compartilhamento de arquivo UNC nos quais salvar o relatório.|  
|**RENDER_FORMAT**|O formato do relatório salvo no disco.|  
|**NOME DE USUÁRIO**|O nome de usuário exigido para o acesso ao recurso de rede ou disco.|  
|**SENHA**|A senha exigida para o acesso ao recurso de rede ou disco.|  
|**WRITEMODE**|O modo de gravação a ser usado durante o acesso ao disco. Os valores válidos são **nenhum**, **substituir**, e **AutoIncrement**.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência técnica &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)   
 [Criando aplicativos que usam o serviço Web e o .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
