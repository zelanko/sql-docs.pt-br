---
title: Assistente de alteração de credenciais (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.changecredentialswizard.F1
helpviewer_keywords:
- Change Credentials Wizard
- report server database, reconfigure
ms.assetid: 9eb4060a-9c3e-41e0-8767-3cfaebc45de7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 07ca904ab8f98dd4dcbdba3f18f4a6fc6469f26a
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952326"
---
# <a name="change-credentials-wizard-ssrs-native-mode"></a>Assistente para Alterar Credenciais (modo nativo do SSRS)
  A ferramenta Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece o Assistente para Alterar Credenciais para guiá-lo pelas etapas de reconfiguração da conta usada pelo servidor de relatório para se conectar ao banco de dados do servidor de relatório. Quando você alterar credenciais, o Gerenciador de Configurações atualizará todas as permissões e informações de logon do banco de dados no servidor de banco de dados para o banco de dados do servidor de relatório que é usado ativamente pelo servidor de relatório.  
  
 Para iniciar o assistente, clique em **Alterar Credenciais** na página Banco de Dados do Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter instruções sobre como iniciar o Configuration Manager [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Gerenciador de configurações do Reporting Services &#40;modo&#41;nativo](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
## <a name="options"></a>Opções  
 **Servidor de banco de dados**  
 Especifica o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] que hospeda o banco de dados do servidor de relatório.  
  
 Para se conectar à instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , use credenciais com permissão para efetuar logon no servidor e atualizar informações do banco de dados. O Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa suas credenciais atuais do Windows, mas se você não tiver um logon ou permissões de banco de dados, poderá especificar um logon de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Não é possível especificar credenciais diferentes do Windows. Para conectar-se como um usuário diferente do Windows, faça logon como esse usuário e inicie o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 **Credenciais**  
 Especifica a conta pela qual o servidor de relatório se conecta ao banco de dados do servidor de relatório. Os valores válidos incluem a conta de serviço do serviço Web Servidor de Relatório, um logon de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definido na instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que está sendo utilizada para hospedar o servidor de relatório ou uma conta do Windows. Se você estiver usando uma conta do Windows, poderá especificar uma conta local ( *\<computername > \\ < nome de usuário @ no__t-3*) se o servidor de relatório e o banco de dados estiverem no mesmo computador, ou em uma conta de domínio ( *\<domain > \\ < nomedeusuário @ no__t-7*) se estiverem em computadores diferentes no mesmo domínio.  
  
 O servidor de relatório criará um logon de banco de dados e atribuirá permissões de banco de dados para a conta especificada.  
  
 O servidor de relatório não cria a própria conta. A conta especificada já deve existir e deve ser válida para sua configuração de implantação. Especificamente, se o banco de dados estiver em um computador remoto e você deseja usar uma conta do Windows, deverá especificar uma conta que tenha permissões de logon nesse computador.  
  
 Se o computador estiver em um domínio diferente ou não confiável, considere o uso de um logon de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações sobre como escolher uma conta, consulte [Configurar uma conexão &#40;de banco de&#41;dados do servidor de relatório SSRS Configuration Manager](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
 **Resumo**  
 Verifique as configurações antes que o assistente seja executado.  
  
 **Progresso e conclusão**  
 Monitore o progresso de cada tarefa.  
  
## <a name="see-also"></a>Consulte também  
 [ &#40;Modo&#41;nativo do SSRS do banco de dados](../../../2014/sql-server/install/database-ssrs-native-mode.md)   
 [Assistente para &#40;alterar banco de dados&#41;modo nativo do SSRS](../../../2014/sql-server/install/change-database-wizard-ssrs-native-mode.md)   
 [Criar um banco de dados de servidor de relatório do modo nativo &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Gerenciador de configurações do Reporting Services F1 tópicos &#40;de ajuda sobre o&#41;modo nativo do SSRS](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Configurar uma conexão de banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  
