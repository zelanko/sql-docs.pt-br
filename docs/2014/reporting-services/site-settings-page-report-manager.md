---
title: Página de configurações (Gerenciador de relatórios) do site | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4d67a01c-eae4-49ba-a6e8-8e983c0248f5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 07fc0207020887d7e3ceb8716ee76c78a55d2bac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101116"
---
# <a name="site-settings-page-report-manager"></a>Página Configurações de Site (Gerenciador de Relatórios)
  Use a página Configurações de Site para alterar o título do aplicativo, definir padrões do servidor para limites de histórico do relatório e valores de tempo limite de processamento de relatório, gerenciar atribuições de funções de nível de sistema e agendamentos compartilhados. Você deve ter permissões de Gerenciador de Conteúdo e de Administrador de Sistema para exibir essa página.  
  
> [!NOTE]  
>  Os recursos a seguir não estão disponíveis em todas as edições do SQL Server: histórico de relatório, execução de relatório e agendas compartilhadas. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
### <a name="to-open-the-site-settings-page"></a>Página abrir a página Configurações de Site  
  
1.  Abra o Gerenciador de Relatórios.  
  
2.  Na parte superior da página, clique em **Configurações de Site**. Esse procedimento abre a página Propriedades Gerais do site.  
  
     **Observação:** Se você não vir as **configurações de Site** opção no menu, você não tem as permissões necessárias, para obter mais informações, consulte a seção "configurações do site" de [configurar um servidor de relatório do modo nativo para administração Local &#40;SSRS&#41;](report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
## <a name="options"></a>Opções  
 **Nome**  
 Especifique o título a ser usado para essa instância do Gerenciador de Relatórios do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Por padrão, o título é "[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]".  
  
 **Selecione as configurações padrão para o histórico de relatórios**  
 Selecione um valor padrão para o número de cópias do histórico de relatório a serem mantidas. O valor padrão fornece uma configuração inicial que estabelece limites de histórico de relatório. Você pode variar essas configurações no relatório. Para obter mais informações, consulte [Página de propriedades Opções de Instantâneo &#40;Gerenciador de Relatórios&#41;](../../2014/reporting-services/snapshot-options-properties-page-report-manager.md).  
  
 Se, posteriormente, você limitar o histórico de relatório, quando o histórico existente exceder o limite especificado, o servidor de relatório reduzirá o histórico existente ao novo limite. Os instantâneos de relatórios mais antigos são excluídos primeiro. Se o histórico de relatórios estiver vazio ou abaixo do limite, novos instantâneos de relatório serão adicionados. Quando o limite é alcançado, o instantâneo mais antigo é excluído e um novo instantâneo de relatório é adicionado.  
  
 **Tempo limite de execução de relatório**  
 Especifique se o tempo limite do relatório chega ao fim depois de um certo número de segundos.  
  
 Esse valor se aplica ao processamento de relatório em um servidor de relatório. Ele não afeta o processamento de dados no servidor de banco de dados que fornece os dados para o seu relatório.  
  
 O relógio do timer do processamento de relatórios é acionado quando o relatório é selecionado e desativado quando o relatório é aberto. Quando você definir esse valor, especifique tempo suficiente para concluir o processamento de dados e do relatório.  
  
 **URL de inicialização personalizada do construtor de relatórios**  
 Especifique uma URL personalizada quando o servidor de relatórios não usar a URL padrão do Construtor de Relatórios. Essa configuração é opcional. Se você não especificar um valor, a URL padrão será usada, o que inicia o Construtor de Relatórios como um aplicativo ClickOnce. A URL padrão é uma das seguintes:  
  
 **Servidor de relatório do modo nativo:** Em uma instalação de modo nativo, a URL padrão terá o formato http://\<*computername*> / reportserver/ReportBuilder/ReportBuilder_3_0_0_0.application.  
  
 Modo integrado do SharePoint: A URL padrão terá o formato http://\<*Site_do_sharepoint*> / _vti_bin/ReportBuilder/ReportBuilder_3_0_0_0.application. "  
  
 **Aplicar**  
 Clique para salvar as alterações no servidor de relatórios.  
  
 **Segurança**  
 Clique nesse link para abrir a página Atribuições de Função do Sistema, na qual você pode atribuir usuário e contas de grupo a funções do sistema predefinidas.  
  
 **Agendas**  
 Clique nesse link para abrir a página Agendas, na qual você pode predefinir agendas compartilhadas que os usuários poderão selecionar para seus relatórios e suas assinaturas.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Concedendo permissões em um servidor de relatório no modo nativo](security/granting-permissions-on-a-native-mode-report-server.md)   
 [funções predefinidas](security/role-definitions-predefined-roles.md)   
 [Ajuda F1 do Gerenciador de Relatórios](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
