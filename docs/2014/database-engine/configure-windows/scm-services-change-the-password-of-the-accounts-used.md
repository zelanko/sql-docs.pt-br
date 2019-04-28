---
title: Alterar a senha das contas usadas pelo SQL Server (SQL Server Configuration Manager) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- expired password [SQL Server], SQL Server Agent
- passwords [SQL Server], SQL Server Agent service
- passwords [SQL Server], changing
- expired password [SQL Server], Database Engine
- passwords [SQL Server], SQL Server service
- Database Engine [SQL Server], passwords
- changing passwords used by SQL Server
- modifying passwords
ms.assetid: 5b6dcc03-6cae-45d3-acef-6f85ca6d615f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 865c23dc88571e0c9ee317eca280286a6c37118f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62810430"
---
# <a name="change-the-password-of-the-accounts-used-by-sql-server-sql-server-configuration-manager"></a>Alterar a senha das contas usadas pelo SQL Server (SQL Server Configuration Manager)
  Este tópico descreve como alterar a senha das contas usadas pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] e pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o SQL Server Configuration Manager. O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent são executados em um computador como um serviço usando credenciais fornecidas inicialmente durante a instalação. Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver sendo executada na conta de domínio e a senha para aquela conta for alterada, a senha usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverá ser atualizada para a senha nova. Se a senha não for atualizada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá perder acesso a alguns recursos de domínio e se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parar, o serviço não será reinicializado até que a senha seja atualizada.  
  
 Para alterar senhas da Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , confira [Senha expirada](../password-expired.md).  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é a ferramenta criada e autorizada para alterar as configurações de serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Alterar um serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o aplicativo Gerenciador de Controle de Serviço do Windows (**services.msc**) nem sempre altera todas as configurações necessárias e pode impedir que o serviço funcione corretamente. No entanto, em um ambiente clusterizado, depois de alterar a senha no nó ativo usando o Gerenciador de Configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você deverá alterar a senha no nó passivo usando o Gerenciador de Controle de Serviços.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ser um administrador do computador para alterar a senha usada por um serviço.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### <a name="to-change-the-password-used-by-the-sql-server-database-engine-service"></a>Para alterar a senha usada pelo serviço SQL Server (Mecanismo de Banco de Dados)  
  
1.  Clique no botão **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], para **Ferramentas de Configuração**e, em seguida, clique em **SQL Server Configuration Manager**.  
  
    > [!NOTE]  
    >  Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager é um snap-in do programa Console de Gerenciamento [!INCLUDE[msCoName](../../includes/msconame-md.md)] e não um programa autônomo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager não aparece como um aplicativo nas versões mais recentes do Windows.  
    >   
    >  -   **Windows 10**:  
    >          Para abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no **página inicial**, digite SQLServerManager12.msc (para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]). Para versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] substitua 12 por um número menor. Clicar SQLServerManager12.msc abre o Configuration Manager. Para fixar o Configuration Manager para a página inicial ou na barra de tarefas, clique com botão direito SQLServerManager12.msc e, em seguida, clique em **abrir local do arquivo**. No Explorador de arquivos do Windows, clique com botão direito SQLServerManager12.msc e, em seguida, clique em **Fixar na tela inicial** ou **Fixar na barra de tarefas**.  
    > -   **Windows 8**:  
    >          Para abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Configuration Manager, no **pesquisa** botão, em **aplicativos**, digite **SQLServerManager\<versão >. msc** como `SQLServerManager12.msc`, em seguida, pressione **Enter**.  
  
2.  No SQL Server Configuration Manager, clique em **Serviços do SQL Server**.  
  
3.  No painel de detalhes, clique com o botão direito do mouse em **SQL Server (**\<instancename>**)** e, depois, clique em **Propriedades**.  
  
4.  Na caixa de diálogo **Propriedades do SQL Server (**\<instancename>**)**, na guia Logon, para a conta listada na caixa **Nome da Conta**, digite a nova senha nas caixas **Senha** e **Confirmar Senha** e, depois, clique em **OK**.  
  
     A senha entra em vigor imediatamente, sem reinicializar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
#### <a name="to-change-the-password-used-by-the-sql-server-agent-service"></a>Para alterar a senha usada pelo serviço SQL Server Agent  
  
1.  Clique no botão **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], para **Ferramentas de Configuração**e, em seguida, clique em **SQL Server Configuration Manager**.  
  
2.  No SQL Server Configuration Manager, clique em **Serviços do SQL Server**.  
  
3.  No painel de detalhes, clique com o botão direito do mouse em **SQL Server Agent (**\<instancename>**)** e, depois, clique em **Propriedades**.  
  
4.  Na caixa de diálogo **Propriedades do SQL Server Agent (**\<instancename>**)**, na guia Logon, para a conta listada na caixa **Nome da Conta**, digite a nova senha nas caixas **Senha** e **Confirmar Senha** e, depois, clique em **OK**.  
  
     Em uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a senha entra em vigor imediatamente, sem reinicializar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Em uma instância clusterizada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderia usar o recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offline, e exigir uma reinicialização.  
  
## <a name="see-also"></a>Consulte também  
 [Tópicos de instruções sobre gerenciamento de serviços &#40;SQL Server Configuration Manager&#41;](../managing-services-how-to-topics-sql-server-configuration-manager.md)  
  
  
