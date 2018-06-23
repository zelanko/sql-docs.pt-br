---
title: Assistente para alterar credenciais (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.rsconfigtool.changecredentialswizard.F1
helpviewer_keywords:
- Change Credentials Wizard
- report server database, reconfigure
ms.assetid: 9eb4060a-9c3e-41e0-8767-3cfaebc45de7
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: c742a02d3accf2a51c2c31bac598064ca34f14c3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116302"
---
# <a name="change-credentials-wizard-ssrs-native-mode"></a>Assistente para Alterar Credenciais (modo nativo do SSRS)
  A ferramenta Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece o Assistente para Alterar Credenciais para guiá-lo pelas etapas de reconfiguração da conta usada pelo servidor de relatório para se conectar ao banco de dados do servidor de relatório. Quando você alterar credenciais, o Gerenciador de Configurações atualizará todas as permissões e informações de logon do banco de dados no servidor de banco de dados para o banco de dados do servidor de relatório que é usado ativamente pelo servidor de relatório.  
  
 Para iniciar o assistente, clique em **alterar credenciais** na página banco de dados de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do Configuration Manager. Para obter instruções sobre como iniciar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager, consulte [Reporting Services Configuration Manager &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
## <a name="options"></a>Opções  
 **Servidor de banco de dados**  
 Especifica o nome do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] instância que executa o banco de dados do servidor de relatório.  
  
 Para conectar-se para a [!INCLUDE[ssDE](../../includes/ssde-md.md)] instância, você deve usar credenciais que têm permissão para fazer logon para os servidor e atualizar informações do banco de dados. O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do Configuration Manager usa suas credenciais atuais do Windows, mas se você não tiver permissões de logon ou de banco de dados, você pode especificar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon de banco de dados.  
  
 Não é possível especificar credenciais diferentes do Windows. Se você quiser se conectar como um usuário diferente do Windows, faça logon como esse usuário e, em seguida, inicie o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do Configuration Manager.  
  
 **Credenciais**  
 Especifica a conta pela qual o servidor de relatório se conecta ao banco de dados do servidor de relatório. Os valores válidos incluem a conta de serviço do serviço Web servidor de relatório, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon de banco de dados definido na [!INCLUDE[ssDE](../../includes/ssde-md.md)] instância que você está usando para hospedar o servidor de relatório ou uma conta do Windows. Se você estiver usando uma conta do Windows, você pode especificar uma conta local (*\<computername >\\< nome de usuário\>*) se o servidor de relatório e o banco de dados estiverem no mesmo computador ou um usuário de domínio conta (*\<domínio >\\< nome de usuário\>*) se eles estiverem em computadores diferentes no mesmo domínio.  
  
 O servidor de relatório criará um logon de banco de dados e atribuirá permissões de banco de dados para a conta especificada.  
  
 O servidor de relatório não cria a própria conta. A conta especificada já deve existir e deve ser válida para sua configuração de implantação. Especificamente, se o banco de dados estiver em um computador remoto e você deseja usar uma conta do Windows, deverá especificar uma conta que tenha permissões de logon nesse computador.  
  
 Se o computador está em um domínio diferente ou não confiável, considere usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon de banco de dados. Para obter mais informações sobre como escolher uma conta, consulte [configurar uma Conexão de banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
 **Resumo**  
 Verifique as configurações antes que o assistente seja executado.  
  
 **Progresso e conclusão**  
 Monitore o progresso de cada tarefa.  
  
## <a name="see-also"></a>Consulte também  
 [Banco de dados &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/database-ssrs-native-mode.md)   
 [Assistente de banco de dados para alterar &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/change-database-wizard-ssrs-native-mode.md)   
 [Criar um banco de dados de servidor de relatório do modo nativo &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Tópicos de Ajuda F1 do Configuration Manager do Reporting Services &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Configurar uma Conexão de banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  