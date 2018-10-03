---
title: Assistente para alterar credenciais (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.changecredentialswizard.F1
helpviewer_keywords:
- Change Credentials Wizard
- report server database, reconfigure
ms.assetid: 9eb4060a-9c3e-41e0-8767-3cfaebc45de7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 632cfe6f1ea61612f59225f38a665ef73da0d898
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48078486"
---
# <a name="change-credentials-wizard-ssrs-native-mode"></a>Assistente para Alterar Credenciais (modo nativo do SSRS)
  A ferramenta Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece o Assistente para Alterar Credenciais para guiá-lo pelas etapas de reconfiguração da conta usada pelo servidor de relatório para se conectar ao banco de dados do servidor de relatório. Quando você alterar credenciais, o Gerenciador de Configurações atualizará todas as permissões e informações de logon do banco de dados no servidor de banco de dados para o banco de dados do servidor de relatório que é usado ativamente pelo servidor de relatório.  
  
 Para iniciar o assistente, clique em **alterar credenciais** na página de banco de dados no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do Configuration Manager. Para obter instruções sobre como iniciar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager, consulte [Reporting Services Configuration Manager &#40;nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
## <a name="options"></a>Opções  
 **Servidor de banco de dados**  
 Especifica o nome da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] instância que executa o banco de dados do servidor de relatório.  
  
 Para conectar-se para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] instância, você deve usar as credenciais que têm permissão para fazer logon, as informações de banco de dados do servidor e atualizar. O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager usa suas credenciais atuais do Windows, mas se você não tiver permissões de logon ou o banco de dados, você pode especificar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon de banco de dados.  
  
 Não é possível especificar credenciais diferentes do Windows. Se você quiser conectar-se como um usuário diferente do Windows, faça logon como esse usuário e, em seguida, inicie o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do Configuration Manager.  
  
 **Credenciais**  
 Especifica a conta pela qual o servidor de relatório se conecta ao banco de dados do servidor de relatório. Os valores válidos incluem a conta de serviço do serviço Web servidor de relatório, uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon de banco de dados definido no [!INCLUDE[ssDE](../../includes/ssde-md.md)] instância que você está usando para hospedar o servidor de relatório ou uma conta do Windows. Se você estiver usando uma conta do Windows, você pode especificar uma conta local (*\<computername >\\< nome de usuário\>*) se o servidor de relatório e o banco de dados estiverem no mesmo computador ou um usuário de domínio conta (*\<domínio >\\< nome de usuário\>*) se eles estiverem em computadores diferentes no mesmo domínio.  
  
 O servidor de relatório criará um logon de banco de dados e atribuirá permissões de banco de dados para a conta especificada.  
  
 O servidor de relatório não cria a própria conta. A conta especificada já deve existir e deve ser válida para sua configuração de implantação. Especificamente, se o banco de dados estiver em um computador remoto e você deseja usar uma conta do Windows, deverá especificar uma conta que tenha permissões de logon nesse computador.  
  
 Se o computador está em um domínio diferente ou não confiável, considere usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon de banco de dados. Para obter mais informações sobre como escolher uma conta, consulte [configurar uma Conexão de banco de dados do servidor de relatório &#40;Configuration Manager do SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
 **Resumo**  
 Verifique as configurações antes que o assistente seja executado.  
  
 **Progresso e conclusão**  
 Monitore o progresso de cada tarefa.  
  
## <a name="see-also"></a>Consulte também  
 [Banco de dados &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/database-ssrs-native-mode.md)   
 [Alterar o Assistente de banco de dados &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/change-database-wizard-ssrs-native-mode.md)   
 [Criar um banco de dados de servidor de relatório do modo nativo &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Tópicos de Ajuda F1 do Configuration Manager do Reporting Services &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Configurar uma Conexão de banco de dados do servidor de relatório &#40;Configuration Manager do SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  
