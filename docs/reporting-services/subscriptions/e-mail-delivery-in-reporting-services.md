---
title: Entrega de email no Reporting Services | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: subscriptions
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subscriptions [Reporting Services], e-mail
- e-mail [Reporting Services]
- mail [Reporting Services]
ms.assetid: fda2f130-97b9-4258-9dbb-e93a70f4d08a
caps.latest.revision: "45"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: cbf8b0a5e84efd67ffa41c4518b6432c2d3283e5
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="e-mail-delivery-in-reporting-services"></a>Entrega de email no Reporting Services
  O SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui uma extensão de entrega de email que fornece um modo de enviar um relatório por email a usuários individuais ou a grupos. Para distribuir um relatório por email, 1) configure o servidor de relatório para entrega de email e 2) defina uma assinatura padrão ou uma assinatura controlada por dados. Uma única assinatura não pode entregar vários relatórios em uma única mensagem de email. No entanto, você pode criar várias assinaturas.  
  
 O servidor de relatório conecta-se a um servidor de email por meio de uma conexão padrão. Ele não usa comunicação criptografada pelo protocolo SSL. O servidor de email deve ser um servidor SMTP local ou remoto na mesma rede que o servidor de relatório.  
  
 Para obter as etapas detalhadas que orientarão você na criação de uma assinatura, confira o seguinte:  
  
-   [Crie e gerencie assinaturas de servidores de relatório no modo Nativo](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)  
  
-   [Criar e gerenciar assinaturas de servidores de relatório no modo SharePoint](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo SharePoint &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo|  
  
## <a name="e-mail-delivery-options"></a>Opções de entrega de email  
 A entrega de email do servidor de relatório pode entregar emails das seguintes maneiras  
  
-   Enviando uma notificação e um hiperlink para o relatório gerado.  
  
-   Enviando uma notificação na linha Assunto: de uma mensagem de email. Por padrão, a linha Assunto: na definição de assinatura inclui as seguintes variáveis que são substituídas por informações específicas do relatório quando a assinatura é processada:  
  
     **@ReportName** especifica o nome do relatório.  
  
     **@ExecutionTime** especifica quando o relatório foi executado.  
  
     Você pode combinar essas variáveis com texto estático ou pode modificar o texto na linha Assunto: para cada assinatura.  
  
-   Envie um relatório inserido ou anexo. O formato de renderização e o navegador determinam se o relatório será inserido ou anexado.  
  
     Se o navegador oferecer suporte a HTML 4.0 e MHTML, e você escolher o formato de renderização de arquivo da Web, o relatório será inserido como parte da mensagem. Todos os outros formatos de renderização (CSV, PDF etc.) entregam os relatórios como anexos. Para os servidores de relatório de modo nativo, você pode desabilitar essa funcionalidade no arquivo de configuração RSReportServer.config.  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não verifica o tamanho do anexo ou mensagem antes de enviar o relatório. Se o anexo ou a mensagem exceder o limite máximo permitido pelo servidor de email, o relatório não será entregue. Escolha uma das outras opções de entrega (por exemplo, URL ou notificação) para relatórios grandes.  
  
 Você define opções de entrega que determinam como um relatório é entregue ao criar a assinatura. Por exemplo, se você selecionar **Incluir Link** na assinatura, a mensagem de email incluirá um hiperlink para o relatório.  
  
## <a name="native-mode-role-based-e-mail-settings"></a>Configurações de email com base em função de modo nativo  
 Em um ambiente de servidor de relatório de modo Nativo, as configurações de entrega de email com as quais você trabalha dependerão de se sua função inclui a tarefa "Gerenciar assinaturas individuais" ou a tarefa "Gerenciar todas as assinaturas".  
  
|Tarefa|Configurações disponíveis|  
|----------|------------------------|  
|Administrar assinaturas individuais|Mostra campos que permitem que um usuário automatize e entregue um relatório a si mesmo. Neste modo, os campos que aceitam aliases de email não estão disponíveis.|  
|Gerenciar todas as assinaturas|Mostra campos que suportam uma distribuição mais ampla, incluindo Para:, Cc:, Bcc: e Responder, fornecendo mais maneiras de encaminhar um relatório a mais assinantes. A disponibilidade de campos de alias de email é definida pelas configurações do arquivo RSReportServer.|  
  
## <a name="specifying-e-mail-addresses-in-a-subscription"></a>Especificando endereços de email em uma assinatura  
 Se você estiver distribuindo relatórios em uma intranet e estiver usando um gateway SMTP para um servidor do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange, digite o alias de email (como se você estivesse enviando um email para um colega). Se a entrega for para uma conta de email externa, digite o endereço de email completo. Se você especificar mais endereços de email para adicionar outros à sua assinatura, os assinantes obterão uma cópia exata do relatório produzido por essa assinatura.  
  
 O servidor de relatório não valida endereços de email ou obtém endereços de email de um servidor de email. Você deve saber antecipadamente quais endereços de email deseja usar. Por padrão, você pode enviar relatórios por email a qualquer conta de email válida dentro ou fora de sua organização. Porém, podem ser usadas definições de configuração para restringir a entrega de email a hosts de servidores de email identificados por nome. Você pode especificar hosts adicionais se desejar oferecer suporte à entrega de email a pessoas que não sejam membros de sua organização.  
  
 A mensagem de email usada para entregar o relatório deve ser enviada de uma conta de email definida no servidor de emails. Uma definição de configuração especifica a conta de email. A conta de email é usada para todos os relatórios entregues pela extensão de entrega de email; você não pode especificar várias contas ou mudar a conta para relatórios individuais.  
  
## <a name="controlling-e-mail-delivery"></a>Controlando a entrega de emails  
 Você pode configurar um servidor de relatório para limitar a distribuição de emails a domínios host específicos. Por exemplo, é possível impedir que um servidor de relatório Nativo entregue um relatório para todos os domínios, com exceção dos listados no arquivo de configuração **RSReportServer.config** .  
  
 Você também pode definir configurações para ocultar o campo **Para** em uma assinatura. Neste caso, os relatórios são entregues somente ao usuário que define a assinatura. No entanto, depois que um relatório é enviado a um usuário, você não pode impedir explicitamente seu encaminhamento.  
  
 A maneira mais eficaz de controlar a distribuição de relatórios é configurar um servidor de relatório para enviar somente uma URL de servidor de relatório. O servidor de relatório usa a Autenticação do Windows e um modelo de autorização baseado em funções para controlar o acesso a um relatório. Se o usuário receber automaticamente por email um relatório que não tem autorização para exibir, o servidor de relatório não exibirá o relatório. Para saber mais sobre assinaturas, veja o seguinte.  
  
## <a name="e-mail-server-configuration"></a>Configuração de servidor de email  
 Para um servidor de relatório de modo Nativo, a extensão de entrega de email é configurada pela ferramenta Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de modo Nativo e pela edição dos arquivos de configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para um servidor de relatório do modo do SharePoint, a extensão de entrega de email é configurada nas páginas de gerenciamento do SharePoint e em scripts do PowerShell.  
  
 
 Para obter informações sobre como configurar um servidor de relatório no modo nativo, consulte [Configurações de email – modo nativo do Reporting Services (Gerenciador de Configurações)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)
 
 
 Para obter informações sobre como configurar um servidor de relatório do modo do SharePoint, consulte o seguinte:  
  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas e permissões](../../reporting-services/security/tasks-and-permissions.md)   
 [Assinaturas e entrega &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Assinaturas controladas por dados](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [Atribuições de função](../../reporting-services/security/role-assignments.md)  
  
  
