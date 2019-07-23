---
title: Configurar a opção de configuração de servidor user connections | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- simultaneous connections [SQL Server]
- user connections option [SQL Server]
- users [SQL Server], simultaneous connections
- maximum number of simultaneous user connections
- connections [SQL Server], simultaneous
ms.assetid: 53beee6e-59fe-4276-9abb-8f1cec2a3508
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 09062541d167be92c40877033e46eec6ebd1c98f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68012173"
---
# <a name="configure-the-user-connections-server-configuration-option"></a>Configurar a opção de configuração de servidor user connections
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como definir a opção de configuração de servidor **user connections** no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A opção **user connections** especifica o número máximo de conexões de usuário simultâneas permitido em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O número real de conexões de usuário permitidas depende também da versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você está usando e dos limites de seu aplicativo ou aplicativos e hardware. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite um máximo de 32.767 conexões de usuário. Como **conexões de usuário** é uma opção dinâmica (autoconfigurável), o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ajusta o número máximo de conexões de usuário automaticamente conforme o necessário, até o valor máximo permitido. Por exemplo, se somente 10 usuários estiverem conectados, 10 objetos de conexão de usuário serão alocados. Na maioria dos casos, não é necessário alterar o valor dessa opção. O padrão é 0, o que significa que as permitidas conexões máximas (32,767) de usuário são permitidas.  
  
 Para determinar o número máximo de conexões de usuário que seu sistema permite, você pode executar [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) ou pode consultar a exibição de catálogo [sys.configuration](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) .  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção user connections usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de configurar a opção user connections](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou por um profissional de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] certificado.  
  
-   O uso da opção **user connections** ajuda a evitar sobrecarregar o servidor com muitas conexões simultâneas. Você pode calcular o número de conexões com base no sistema e nos requisitos do usuário. Por exemplo, em um sistema com muitos usuários, cada usuário não requer geralmente uma conexão exclusiva. As conexões podem ser compartilhadas entre os usuários. Usuários que executam aplicativos OLE DB precisam de uma conexão para cada objeto de conexão aberto, usuários que executam aplicativos ODBC (Conectividade Aberta de Banco de Dados) precisam de uma conexão para cada atividade gerenciada no aplicativo e usuários que executam aplicativos DB-Library precisam de uma conexão para cada processo iniciado que chama a função **dbopen** do DB-Library.  
  
    > [!IMPORTANT]  
    >  Se for necessário usar essa opção, não defina o valor muito alto, porque cada conexão tem sobrecarga, independentemente da conexão que está sendo usada. Se o número máximo de conexões de usuário for excedido, você receberá uma mensagem de erro e não poderá se conectar até que outra conexão fique disponível.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-the-user-connections-option"></a>Para configurar a opção user connections  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e clique em **Propriedades**.  
  
2.  Clique no nó **Conexões** .  
  
3.  Em **Conexões**, na caixa **Número máximo de conexões simultâneas** , digite ou selecione um valor de 0 a 32767 para definir o número máximo de usuários que terão permissão para se conectar simultaneamente à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  Reinicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-configure-the-user-connections-option"></a>Para configurar a opção user connections  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para configurar o valor da opção `user connections` como `325` usuários.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'user connections', 325 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 Para obter mais informações, veja [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de configurar a opção user connections  
 O servidor deve ser reiniciado para que a configuração entre em vigor.  
  
## <a name="see-also"></a>Consulte Também  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
