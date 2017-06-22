---
title: "Escrever eventos de auditoria do SQL Server no log de segurança | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logs [SQL Server], Security Log
- server audit [SQL Server]
- audits [SQL Server], writing to Security Log
- security logs [SQL Server]
ms.assetid: 6fabeea3-7a42-4769-a0f3-7e04daada314
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 268f1fbd8ea57db8626c84999a3454e4c4459511
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="write-sql-server-audit-events-to-the-security-log"></a>Gravar eventos de auditoria do SQL Server no log de segurança
  em um ambiente de alta segurança, o log de Segurança do Windows é o local apropriado para gravar eventos que registram o acesso a objetos. Outros locais de auditoria têm suporte, mas estão mais sujeitos a falsificações.  
  
 Há dois requisitos principais para gravar auditorias do servidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no log de Segurança do Windows:  
  
-   É necessário configurar o acesso ao objeto de auditoria para capturar os eventos. A ferramenta de política de auditoria (`auditpol.exe`) expõe uma variedade de configurações de subpolíticas na categoria **acesso ao objeto de auditoria** . Para permitir que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] audite o acesso a objetos, defina a configuração de **aplicativo gerado** .  
  
-   A conta que o serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está executando deve ter a permissão **gerar auditorias de segurança** para gravar no log de Segurança do Windows. Por padrão, as contas LOCAL SERVICE e NETWORK SERVICE têm essa permissão. Esta etapa não será necessária se o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] estiver sendo executado em uma dessas contas.  
  
 A política de auditoria do Windows poderá afetar a auditoria do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se estiver configurada para gravar no log de segurança do Windows, com a possibilidade de se perder eventos se a política de auditoria não estiver configurada corretamente. Normalmente, o log de segurança do Windows é definido para substituir os eventos mais antigos. Isso preserva os eventos mais recentes. No entanto, se o log de segurança do Windows não estiver definido para substituir eventos mais antigos, quando ele estiver cheio, o sistema emitirá o evento 1104 do Windows (O log está cheio). Nesse momento:  
  
-   Nenhum outro evento de segurança será registrado  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não conseguirá detectar que o sistema não pode registrar os eventos no log de segurança, o que resultará na possível perda de eventos de auditoria  
  
-   Depois que o administrador do computador corrigir o log de segurança, o comportamento de log voltará ao normal.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para gravar eventos de auditoria do SQL Server no log de segurança:**  
  
     [Definir a configuração de acesso ao objeto de auditoria no Windows usando auditpol](#auditpolAccess)  
  
     [Definir a configuração de acesso ao objeto de auditoria no Windows usando secpol](#secpolAccess)  
  
     [Conceder a permissão gerar auditorias de segurança a uma conta usando secpol](#secpolPermission)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 Os administradores do computador com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devem entender que as configurações locais do log de segurança podem ser substituídas por uma política de domínio. Nesse caso, a política de domínio poderá substituir a configuração de subcategoria (**auditpol /get /subcategory:"application generated"**). Isso pode afetar a capacidade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de registrar eventos em log, sem que haja uma maneira de detectar que os eventos que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está tentando auditar não serão registrados.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ser um administrador do Windows para definir essas configurações.  
  
##  <a name="auditpolAccess"></a> Para definir a configuração de acesso ao objeto de auditoria no Windows usando auditpol  
  
1.  Abra um prompt de comando com permissões administrativas.  
  
    1.  No menu **Iniciar** , aponte para **Todos os Programas**, para **Acessórios**, clique com o botão direito do mouse no **Prompt de Comando**e clique em **Executar como administrador**.  
  
    2.  Se a caixa de diálogo **Controle de Conta de Usuário** for aberta, clique em **Continuar**.  
  
2.  Execute a instrução a seguir para habilitar a auditoria de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
    ```  
    auditpol /set /subcategory:"application generated" /success:enable /failure:enable  
    ```  
  
3.  Feche a janela do prompt de comando.  
  
##  <a name="secpolAccess"></a> Para conceder a permissão gerar auditorias de segurança a uma conta usando secpol  
  
1.  Para qualquer sistema operacional Windows, no menu **Iniciar** , clique em **Executar**.  
  
2.  Digite **secpol.msc** e clique em **OK**. Se a caixa de diálogo **Controle de Acesso de Usuário** aparecer, clique em **Continuar**.  
  
3.  Na ferramenta Política de Segurança Local, expanda **Configurações de Segurança**, **Políticas Locais**e clique em **Atribuição de Direitos de Usuário**.  
  
4.  No painel de resultados, clique duas vezes em **Gerar auditoria de segurança**.  
  
5.  Na guia **Configuração de Segurança Local** , clique em **Adicionar Usuário ou Grupo**.  
  
6.  Na caixa de diálogo **Selecionar Usuários, Computadores ou Grupos** , digite o nome da conta de usuário, como **domain1\user1** e clique em **OK**ou em **Avançado** e procure a conta.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
8.  Feche a ferramenta Política de Segurança.  
  
9. Reinicie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para habilitar essa configuração.  
  
##  <a name="secpolPermission"></a> Para definir a configuração de acesso ao objeto de auditoria no Windows usando secpol  
  
1.  Se o sistema operacional for anterior ao [!INCLUDE[wiprlhext](../../../includes/wiprlhext-md.md)] ou Windows Server 2008, no menu **Iniciar** , clique em **Executar**.  
  
2.  Digite **secpol.msc** e clique em **OK**. Se a caixa de diálogo **Controle de Acesso de Usuário** aparecer, clique em **Continuar**.  
  
3.  Na ferramenta Política de Segurança Local, expanda **Configurações de segurança**, **Políticas Locais**e clique em **Política de Auditoria**.  
  
4.  No painel de resultados, clique duas vezes em **Auditar acesso ao objeto**.  
  
5.  Na guia **Configuração de Segurança Local** , na área **Fazer a auditoria dessas tentativas** , selecione **Êxito** e **Falha**.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  Feche a ferramenta Política de Segurança.  
  
## <a name="see-also"></a>Consulte também  
 [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)  
  
  
