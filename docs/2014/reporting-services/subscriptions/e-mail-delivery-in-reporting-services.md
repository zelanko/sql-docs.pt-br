---
title: Entrega de email no Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], e-mail
- e-mail [Reporting Services]
- mail [Reporting Services]
ms.assetid: fda2f130-97b9-4258-9dbb-e93a70f4d08a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 68024e36dd5f8188097ebcc673056c1b6d11e59b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66100892"
---
# <a name="e-mail-delivery-in-reporting-services"></a>Entrega de email no Reporting Services
  O SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui uma extensão de entrega de email que fornece um modo de enviar um relatório por email a usuários individuais ou a grupos. A extensão de entrega de email é configurada pela ferramenta Gerenciador de Configurações do Reporting Services e pela edição dos arquivos de configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Para distribuir ou receber um relatório por email, defina uma assinatura padrão ou uma assinatura controlada por dados. Você pode assinar ou distribuir apenas um relatório por vez. Você não pode criar uma assinatura que entregue vários relatórios em uma única mensagem de email. Para obter mais informações sobre assinaturas, consulte [criar, modificar e excluir assinaturas padrão &#40;Reporting Services no modo nativo&#41;](create-and-manage-subscriptions-for-native-mode-report-servers.md).  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo do SharePoint &#124; SharePoint 2010 e SharePoint 2013<br /><br /> **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo|  
  
## <a name="e-mail-delivery-options"></a>Opções de entrega de email  
 A entrega de email do servidor de relatório pode entregar emails das seguintes maneiras:  
  
-   Enviando uma notificação e um hiperlink para o relatório gerado.  
  
-   Enviando uma notificação na linha Assunto: de uma mensagem de email. Por padrão, a linha Assunto: na definição de assinatura inclui as seguintes variáveis que são substituídas por informações específicas do relatório quando a assinatura é processada:  
  
     **@ReportName** especifica o nome do relatório.  
  
     **@ExecutionTime** especifica quando o relatório foi executado.  
  
     Você pode combinar essas variáveis com texto estático ou pode modificar o texto na linha Assunto: para cada assinatura.  
  
-   Envie um relatório inserido ou anexo. O formato de renderização e o navegador determinam se o relatório será inserido ou anexado.  
  
     Se o navegador oferecer suporte a HTML 4.0 e MHTML, e você escolher o formato de renderização de arquivo da Web, o relatório será inserido como parte da mensagem. Todos os outros formatos de renderização (CSV, PDF etc.) entregam os relatórios como anexos. Você pode desabilitar essa funcionalidade no arquivo de configuração de RSReportServer.  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não verifica o tamanho do anexo ou mensagem antes de enviar o relatório. Se o anexo ou a mensagem exceder o limite máximo permitido pelo servidor de email, o relatório não será entregue. Escolha uma das outras opções de entrega (por exemplo, URL ou notificação) para relatórios grandes.  
  
 Você define opções de entrega que determinam como um relatório é entregue ao criar a assinatura. Por exemplo, se você selecionar **Incluir Link** na assinatura, a mensagem de email incluirá um hiperlink para o relatório.  
  
## <a name="role-based-e-mail-settings"></a>Configurações de email com base em função  
 Ao assinar um relatório, as configurações de entrega de email com as quais você trabalha dependerão de se sua função inclui a tarefa "Gerenciar assinaturas individuais" ou a tarefa "Gerenciar todas as assinaturas".  
  
|Tarefa|Configurações disponíveis|  
|----------|------------------------|  
|Administrar assinaturas individuais|Mostra campos que permitem que um usuário automatize e entregue um relatório a si mesmo. Neste modo, os campos que aceitam aliases de email não estão disponíveis.|  
|Gerenciar todas as assinaturas|Mostra campos que suportam uma distribuição mais ampla, incluindo Para:, Cc:, Bcc: e Responder, fornecendo mais maneiras de encaminhar um relatório a mais assinantes. A disponibilidade de campos de alias de email é definida pelas configurações do arquivo RSReportServer.|  
  
## <a name="specifying-e-mail-addresses-in-a-subscription"></a>Especificando endereços de email em uma assinatura  
 Se você estiver distribuindo relatórios em uma intranet e estiver usando um gateway SMTP para um servidor do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange, digite o alias de email (como se você estivesse enviando um email para um colega). Se a entrega for para uma conta de email externa, digite o endereço de email completo. Se você especificar mais endereços de email para adicionar outros à sua assinatura, os assinantes obterão uma cópia exata do relatório produzido por essa assinatura.  
  
 O servidor de relatório não valida endereços de email ou obtém endereços de email de um servidor de email. Você deve saber antecipadamente quais endereços de email deseja usar. Por padrão, você pode enviar relatórios por email a qualquer conta de email válida dentro ou fora de sua organização. Porém, podem ser usadas definições de configuração para restringir a entrega de email a hosts de servidores de email identificados por nome. Você pode especificar hosts adicionais se desejar oferecer suporte à entrega de email a pessoas que não sejam membros de sua organização.  
  
 A mensagem de email usada para entregar o relatório deve ser enviada de uma conta de email definida no servidor de emails. Uma definição de configuração especifica a conta de email. A conta de email é usada para todos os relatórios entregues pela extensão de entrega de email; você não pode especificar várias contas ou mudar a conta para relatórios individuais.  
  
## <a name="e-mail-server-configuration"></a>Configuração de servidor de email  
 O servidor de relatório conecta-se a um servidor de email por meio de uma conexão padrão. Ele não usa comunicação criptografada pelo protocolo SSL. O servidor de email deve ser um servidor SMTP local ou remoto na mesma rede que o servidor de relatório.  
  
 Para obter informações sobre como configurar um servidor de relatório de modo nativo, consulte o seguinte:  
  
-   [Configurar um servidor de relatório para entrega de email &#40;Configuration Manager do SSRS&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
  
-   [Configurações de email – Configuration Manager &#40;modo nativo do SSRS&#41;](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)  
  
 Para obter informações sobre como configurar um servidor de relatório do modo do SharePoint, consulte o seguinte:  
  
-   [Configurar o email para um serviço de aplicativo do Reporting Services &#40;SharePoint 2010 e SharePoint 2013&#41;](../install-windows/configure-e-mail-for-a-reporting-services-service-application.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e permissões](../security/tasks-and-permissions.md)   
 [Assinaturas e entrega &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [Assinaturas controladas por dados](data-driven-subscriptions.md)   
 [Atribuições de função](../security/role-assignments.md)  
  
  
