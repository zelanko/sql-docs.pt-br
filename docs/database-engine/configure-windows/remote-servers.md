---
title: Servidores remotos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- server management [SQL Server], remote servers
- remote servers [SQL Server], configuring
- remote servers [SQL Server]
- servers [SQL Server], remote
- remote access option
ms.assetid: abf0fa24-f199-4273-9a1a-e8787ac9bee1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2b3c4937d87d166d87711389be7acd0c4ae0f8ff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938179"
---
# <a name="remote-servers"></a>Servidores remotos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Os servidores remotos só têm suporte no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para compatibilidade com versões anteriores. Os novos aplicativos devem usar servidores vinculados. Para obter mais informações, veja [Servidores vinculados &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md).  
  
 Uma configuração de servidor remoto permite que um cliente conectado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] execute um procedimento armazenado em outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem estabelecer uma conexão separada. Em vez disso, o servidor ao qual o cliente está conectado aceita a solicitação do cliente e envia a solicitação para o servidor remoto em nome do cliente. O servidor remoto processa a solicitação e retorna todos os resultados ao servidor original. Esse servidor, por sua vez, passa esses resultados para o cliente. Quando você define uma configuração de servidor remoto, deve considerar também como estabelecer a segurança.  
  
 Se você quiser definir uma configuração de servidor para executar procedimentos armazenados em outro servidor e não possuir configurações de servidor remoto, use servidores vinculados em vez de servidores remotos. Procedimentos armazenados e consultas distribuídas são permitidos em servidores vinculados; no entanto, somente procedimentos armazenados são permitidos em servidores remotos.  
  
## <a name="remote-server-details"></a>Detalhes do servidor remoto  
 Os servidores remotos são definidos em pares. Para definir um par de servidores remotos, configure ambos os servidores para reconhecerem um ao outro como servidores remotos.  
  
 Na maioria das vezes, você não precisará definir opções de configuração para servidores remotos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define os padrões em ambos os computadores locais e remotos para permitir conexões de servidor remoto.  
  
 Para que o acesso ao servidor remoto funcione, a opção de configuração **acesso remoto** deve ser definida como 1 no computador local e no computador remoto. (Essa é a definição padrão.) O  **acesso remoto** controla os logons de servidores remotos. Você pode redefinir essa opção de configuração usando o procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)] **sp_configure** ou o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para definir a opção no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], na página **Propriedades do Servidor - Conexões** , use **Permitir conexões remotas com este servidor**. Para acessar a página **Propriedades do Servidor – Conexões** , no Pesquisador de Objetos, clique com o botão direito do mouse no nome do servidor e clique em **Propriedades**. Na página **Propriedades do Servidor** , clique na página **Conexões** .  
  
 No servidor local, é possível desabilitar uma configuração de servidor remoto para evitar o acesso ao servidor local por usuários do servidor remoto com o qual ele faz par.  
  
## <a name="security-for-remote-servers"></a>Segurança para servidores remotos  
 Para habilitar RPCs (chamadas de procedimento remoto) em um servidor remoto, é necessário configurar mapeamentos de logon no servidor remoto e, possivelmente, no servidor local que está executando uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A RPC é desabilitada por padrão no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa configuração aumenta a segurança do servidor reduzindo sua área da superfície passível de ataque. Antes de usar RPC, é necessário habilitar esse recurso. Para obter mais informações, veja [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
### <a name="setting-up-the-remote-server"></a>Configurando o servidor remoto  
 Os mapeamentos de logon remoto devem ser configurados no servidor remoto. Usando esses mapeamentos, o servidor remoto mapeia o logon de entrada de uma conexão RPC, de um servidor especificado para um logon local. Os mapeamentos de logon remoto podem ser configurados com o procedimento armazenado **sp_addremotelogin** no servidor remoto.  
  
> [!NOTE]  
>  A opção **confiável** de  **sp_remoteoption** não tem suporte no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="setting-up-the-local-server"></a>Configurando o servidor local  
 Para logons locais de autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você não precisa configurar um mapeamento de logon no servidor local. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa o logon e a senha locais para se conectar ao servidor remoto. Para logons autenticados do Windows, configure um mapeamento de logon local em um servidor local que defina que o logon e a senha sejam usados por uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando ele fizer uma conexão RPC para um servidor remoto.  
  
 Para logons criados pela Autenticação do Windows, é necessário criar um mapeamento para um nome de logon e senha usando o procedimento armazenado **sp_addlinkedservlogin** . Esse nome de logon e essa senha devem corresponder ao logon e senha de entrada esperados pelo servidor remoto, conforme criado por **sp_addremotelogin**.  
  
> [!NOTE]  
>  Quando possível, use a Autenticação do Windows.  
  
### <a name="remote-server-security-example"></a>Exemplo de segurança de servidor remoto  
 Considere estas instalações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] : **serverSend** e **serverReceive**. **serverReceive** está configurado para mapear um logon de entrada de **serverSend**, chamado **Sales_Mary**, para um logon autenticado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no **serverReceive**, chamado **Brenda**. Outro logon de entrada de **serverSend**, chamado **Joe**, está mapeado para um logon autenticado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em **serverReceive** _,_ chamado **Joe**.  
  
 O exemplo de código do Transact-SQL a seguir configura `serverSend` para executar RPCs em `serverReceive`.  
  
```  
--Create remote server entry for RPCs   
--from serverSend in serverReceive.  
EXEC sp_addserver 'serverSend';  
GO  
  
--Create remote login mapping for login 'Sales_Mary' from serverSend  
--to Alice.  
EXEC sp_addremotelogin 'serverSend', 'Alice', 'Sales_Mary';  
GO  
--Create remote login mapping for login Joe from serverReceive   
--to same login.  
--Assumes same password for Joe in both servers.  
EXEC sp_addremotelogin 'serverSend', 'Joe', 'Joe';  
GO  
```  
  
 Em `serverSend`, um mapeamento de logon local é criado para um logon autenticado do Windows `Sales\Mary` para um logon `Sales_Mary`. Nenhum mapeamento local é necessário para `Joe`, porque o padrão é usar o mesmo nome de logon e senha, e `serverReceive` tem um mapeamento para `Joe`.  
  
```  
--Create a remote server entry for RPCs from serverReceive.  
EXEC sp_addserver 'serverReceive';  
GO  
--Create a local login mapping for the Windows authenticated login.  
--Sales\Mary to Sales_Mary. The password should match the  
--password for the login Sales_Mary in serverReceive.  
EXEC sp_addlinkedsrvlogin 'serverReceive', false, 'Sales\Mary',  
   'Sales_Mary', '430[fj%dk';  
GO  
```  
  
## <a name="viewing-local-or-remote-server-properties"></a>Exibindo propriedades do servidor local ou remoto  
 Você pode usar o procedimento armazenado estendido **xp_msver** para examinar atributos de servidores locais ou remotos. Entre esses atributos estão o número da versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o tipo e o número de processadores no computador e a versão do sistema operacional. No servidor local, você pode exibir bancos de dados, arquivos, logons e ferramentas para um servidor remoto. Para obter mais informações, veja [xp_msver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-msver-transact-sql.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 [Servidores vinculados &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
 [Configurar a opção remote access de configuração de servidor](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)  
  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  
