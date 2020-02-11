---
title: Conceder funções DQS a usuários
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: afb445b5-bdbe-4bfe-844f-344766cdc2b2
author: swinarko
ms.author: sawinark
ms.openlocfilehash: d5ceef0a129989eedf75d79429e8d38c999f4257
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75254765"
---
# <a name="grant-dqs-roles-to-users"></a>Conceder funções DQS a usuários

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Este tópico descreve como criar logons do SQL Server com base em uma entidade do Windows e conceder as funções de [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] no banco de dados DQS_MAIN.  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   Você precisa ter concluído a instalação do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] executando o arquivo DQSInstaller.exe. Para obter mais informações, consulte [Executar o DQSInstaller.exe para concluir a instalação do Data Quality Server](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
-   Sua conta de usuário do Windows deve ser membro da função de servidor fixa apropriada (como securityadmin, serveradmin ou sysadmin) para criar um logon do SQL login e conceder a ele as funções de DQS.  
  
### <a name="to-create-sql-login-and-grant-dqs-roles"></a>Para criar logon de SQL e conceder funções de DQS  
  
1.  Inicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda sua instância do SQL Server e expanda **Segurança**.  
  
3.  Clique com o botão direito do mouse na pasta **Segurança** , aponte para **Novo**e clique em **Logon**.  
  
4.  Na caixa de diálogo **Logon – Novo**, especifique o nome de um usuário do Windows na caixa **Nome de Logon**, especifique o tipo de autenticação como **Autenticação do Windows** e clique em **Pesquisar** para validar o usuário.  
  
5.  Depois que o usuário for validado, clique na página **Mapeamento de Usuário** no painel esquerdo.  
  
6.  No painel direito, marque a caixa de seleção sob a coluna **Mapa** do banco de dados **DQS_MAIN** e marque a caixa de seleção **dqs_administrator**, **dqs_kb_editor**ou **dqs_kb_operator** no painel **Associação à função de banco de dados para: DQS_MAIN** , dependendo do nível de acesso necessário ao usuário. Para obter mais informações sobre as três funções DQS, consulte [Segurança DQS](../../data-quality-services/dqs-security.md).  
  
7.  Na caixa de diálogo **Logon – Novo**, clique em **OK** para aplicar as alterações.  
  
    > [!NOTE]  
    >  Se você conceder a função **dqs_administrator** a um usuário, aplique as alterações e verifique novamente as permissões de usuário; as outras duas caixas de seleção de funções DQS (**dq_kb_editor** e **dqs_kb_operator**) também serão marcadas.  
  
## <a name="next-steps"></a>Próximas etapas  
 Tente fazer logon no [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] usando a conta de usuário do Windows para a qual você acabou de criar o logon SQL e à qual concedeu uma função DQS.  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar o Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [Criar um logon](../../relational-databases/security/authentication-access/create-a-login.md)  
  
  
