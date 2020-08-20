---
title: Conectar-se ao SQL Server quando os administradores do sistema estão bloqueados | Microsoft Docs
description: Saiba como reobter o acesso ao SQL Server como administrador do sistema se você tiver sido bloqueado por engano.
ms.custom: contperfq4
ms.date: 05/20/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- sa account
- connecting when locked out [SQL Server]
- locked out [SQL Server]
ms.assetid: c0c0082e-b867-480f-a54b-79f2a94ceb67
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 801602c78193f9fc3fa9cdab40b98c3dc3dd42e0
ms.sourcegitcommit: 291ae8f6b72fd355f8f24ce5300339306293ea7e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2020
ms.locfileid: "88512308"
---
# <a name="connect-to-sql-server-when-system-administrators-are-locked-out"></a>Conectar-se ao SQL Server quando os administradores do sistema estão bloqueados 
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
Este artigo descreve como você poderá recuperar o acesso ao [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] como administrador do sistema se você tiver sido bloqueado.  Um administrador do sistema pode perder o acesso a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devido a um dos seguintes motivos:  
  
-   Todos os logons que são membros da função de servidor fixa sysadmin foram removidos por engano.  
  
-   Todos os Grupos do Windows que são membros da função de servidor fixa sysadmin foram removidos por engano.  
  
-   Os logons que são membros da função de servidor fixa sysadmin são para indivíduos que deixaram a empresa ou que não estão disponíveis.  
  
-   A conta sa está desabilitada ou ninguém sabe a senha.  
  
## <a name="resolution"></a>Resolução

Para resolver o problema de acesso, recomendamos que você inicie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único. Esse modo impede que outras conexões ocorram enquanto você tenta restabelecer o acesso. Daqui em diante, você pode se conectar à instância do SQL Server e adicionar o seu logon à função de servidor **sysadmin**. As etapas detalhadas para essa solução são fornecidas na seção [etapas passo a passo](#step-by-step-instructions).


Você pode iniciar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único com as opções `-m` ou `-f` da linha de comando. Qualquer membro do grupo de Administradores locais do computador pode conectar-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como membro da função de servidor fixa **sysadmin**.  

Ao iniciar uma instância no modo de usuário único, primeiro interrompa o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Caso contrário, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent pode se conectar primeiro, usando a única conexão disponível ao servidor e impedindo que você faça logon.

Também é possível que um aplicativo cliente desconhecido assuma a única conexão disponível antes de você poder fazer logon. Para evitar que isso aconteça, você pode usar a opção `-m` seguida por um nome de aplicativo para limitar as conexões a uma conexão no aplicativo especificado. Por exemplo, iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com `-mSQLCMD` limita as conexões a uma conexão que se identifica como o programa cliente **sqlcmd**. Para conectar-se pelo Editor de Consulta no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], use `-m"Microsoft SQL Server Management Studio - Query"`.  


> [!IMPORTANT]  
> Não use `-m` com um nome de aplicativo como um recurso de segurança. Os aplicativos cliente especificam o nome do aplicativo por meio das configurações de cadeia de conexão, para ele que possa ser falsificado com um nome falso sem dificuldades.

A tabela a seguir resume as diferentes maneiras de iniciar a sua instância no modo de usuário único na linha de comando.

| Opção | Descrição | Quando usar |
|:---|:---|:---|
|`-m` | Limita as conexões a uma conexão | Quando não há outros usuários tentando se conectar à instância ou você não tem certeza do nome do aplicativo que está usando para se conectar à instância. |
|`-mSQLCMD`| Limita conexões a uma conexão que precisa se identificar como o programa cliente **sqlcmd**| Quando você planeja se conectar à instância com **sqlcmd** e deseja impedir que outros aplicativos usem a única conexão disponível. |
|`-m"Microsoft SQL Server Management Studio - Query"`| Limita as conexões a uma conexão que precisa se identificar como o aplicativo **Microsoft SQL Server Management Studio – Consulta**.| Quando você planeja se conectar à instância com o Editor de Consulta no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e deseja impedir que outros aplicativos usem a única conexão disponível. |
|`-f`| Limita as conexões a uma conexão e inicia a instância na configuração mínima | Quando alguma outra configuração está impedindo a inicialização. |
| &nbsp; | &nbsp; | &nbsp; |
  
Para obter instruções passo a passo sobre como iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único, confira [Iniciar o SQL Server no Modo de Usuário Único](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md).

## <a name="step-by-step-instructions"></a>Instruções passo a passo

As instruções passo a passo a seguir descrevem como conceder permissões de administrador do sistema a um logon de SQL Server que não tem mais acesso por engano.

Essas instruções presumem que,

* O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executado no Windows 8 ou superior. São fornecidos pequenos ajustes para as versões anteriores do SQL Server ou do Windows, quando aplicáveis.

* O [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] está instalado no computador.  

Execute estas instruções enquanto estiver conectado ao Windows como membro do grupo de administradores local.

1.  No menu Iniciar do Windows, clique com o botão direito do mouse no ícone [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager e selecione **Executar como administrador** para passar as suas credenciais de administrador para o Configuration Manager.  
  
2.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no painel esquerdo, selecione **Serviços do SQL Server**. No painel direito, localize a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. (A instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui **(MSSQLSERVER)** após o nome do computador. As instâncias nomeadas aparecem em maiúsculas com o mesmo nome apresentado na área Servidores Registrados.) Clique com o botão direito do mouse na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e clique em **Propriedades**.  
  
3.  Na guia **Parâmetros de Inicialização**, na caixa **Especificar um parâmetro de inicialização**, digite `-m` e clique em **Adicionar**. (É um traço seguido da letra m minúscula.)  
  
    > [!NOTE]  
    >  Em algumas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , não há nenhuma guia **Parâmetros de Inicialização** . Nesse caso, na guia **Avançado** , clique duas vezes em **Parâmetros de Inicialização**. Os parâmetros são abertos em uma janela muito pequena. Tenha cuidado para não alterar os parâmetros existentes. No final, adicione um novo parâmetro `;-m` e clique em **OK**. (É um ponto-e-vírgula seguido da letra m minúscula.)  
  
4.  Clique em **OK**e, após a mensagem de reinicialização, clique com o botão direito do mouse no nome do servidor e clique em **Reiniciar**.  
  
5.  Depois que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reiniciar, o servidor estará no modo de usuário único. Verifique se o Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não está em execução. Se for iniciado, ele usará sua única conexão.  
  
6.  No menu Iniciar do Windows, clique com o botão direito do mouse no ícone do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e selecione **Executar como administrador**. As credenciais do administrador serão passadas para o SSMS.
  
    > [!NOTE]  
    >  Nas versões anteriores do Windows, a opção **Executar como administrador** aparece como um submenu.  
  
     Em algumas configurações, o SSMS tentará criar várias conexões. Várias conexões falharão porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está no modo de usuário único. De acordo com o seu cenário, execute uma das ações a seguir.  
  
    1.  Conecte-se ao Pesquisador de Objetos usando a Autenticação do Windows, que inclui as credenciais do Administrador. Expanda **Segurança**, expanda **Logons**e clique duas vezes no seu próprio logon. Na página **Funções de Servidor** , selecione **sysadmin**e clique em **OK**.  
  
    2.  Em vez de conectar-se ao Pesquisador de Objetos, conecte-se à Janela de Consulta usando a autenticação do Windows (que inclui as credenciais do administrador). (Você só poderá se conectar dessa maneira se não tiver se conectado ao Pesquisador de Objetos.) Execute o código da seguinte maneira para adicionar um novo logon de autenticação do Windows que é membro da função de servidor fixa **sysadmin** . O exemplo a seguir adiciona um usuário de domínio chamado `CONTOSO\PatK`.  
  
        ```  
        CREATE LOGIN [CONTOSO\PatK] FROM WINDOWS;  
        ALTER SERVER ROLE sysadmin ADD MEMBER [CONTOSO\PatK];  
        ```  
  
    3.  Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver sendo executado no modo de autenticação mista, conecte-se a uma Janela de Consulta usando a autenticação do Windows (que inclui as credenciais do administrador). Execute o código da maneira exibida a seguir para criar um logon de autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é membro da função de servidor fixa **sysadmin**.  
  
        ```  
        CREATE LOGIN TempLogin WITH PASSWORD = '************';  
        ALTER SERVER ROLE sysadmin ADD MEMBER TempLogin;  
        ```  
  
        > [!WARNING]  
        >  Substitua ************ por uma senha forte.  
  
    4.  Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver sendo executado no modo de autenticação mista e você quiser redefinir a senha da conta **sa** , conecte-se a uma Janela de Consulta usando a Autenticação do Windows (que inclui as credenciais do Administrador). Alterar a senha da conta **sa** com a sintaxe a seguir.  
  
        ```  
        ALTER LOGIN sa WITH PASSWORD = '************';  
        ```  
  
        > [!WARNING]  
        >  Substitua ************ por uma senha forte.  

7. Feche o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
8. As próximas etapas retornam o SQL Server para o modo de vários usuários. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no painel esquerdo, selecione **Serviços do SQL Server**.

9. No painel direito, clique com o botão direito do mouse na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e clique em **Propriedades**.  
  
10. Na guia **Parâmetros de Inicialização** , na caixa **Parâmetros existentes** , selecione `-m` e clique em **Remover**.  
  
    > [!NOTE]  
    >  Em algumas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , não há nenhuma guia **Parâmetros de Inicialização** . Nesse caso, na guia **Avançado** , clique duas vezes em **Parâmetros de Inicialização**. Os parâmetros são abertos em uma janela muito pequena. Remova o `;-m` que você adicionou anteriormente e clique em **OK**.  
  
11. Clique com o botão direito do mouse no nome do servidor e clique em **Reiniciar**. Certifique-se de iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent novamente, se você o tiver interrompido antes de iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único.
  
Você poderá se conectar normalmente a uma das contas, que agora é membro da função de servidor fixa de **sysadmin** .  
  
## <a name="see-also"></a>Consulte Também  

* [Configurar opções de inicialização do servidor](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)
* [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md)  
