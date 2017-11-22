---
title: "Práticas recomendadas de segurança com bancos de dados independentes | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: contained database, threats
ms.assetid: 026ca5fc-95da-46b6-b882-fa20f765b51d
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fd6636cc4e2ee383fbd178b0f6b1e304f996570c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="security-best-practices-with-contained-databases"></a>Práticas recomendadas de segurança com bancos de dados independentes
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Bancos de dados independentes têm algumas ameaças exclusivas que devem ser entendidas e mitigadas pelos administradores do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . A maioria das ameaças está relacionada ao processo de autenticação **USER WITH PASSWORD** que move o limite de autenticação do nível do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para o nível do banco de dados.  
  
## <a name="threats-related-to-users"></a>Ameaças relacionadas a usuários  
 Usuários em um banco de dados independente que têm a permissão **ALTER ANY USER** , como membros das funções de banco de dados fixas **db_owner** e **db_securityadmin** , podem conceder acesso ao banco de dados sem conhecimento ou permissão ou o administrador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A concessão de acesso a um banco de dados independente a usuários aumenta a área da superfície de ataque potencial contra toda a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os administradores devem entender essa delegação de controle de acesso e ter muito cuidado ao conceder permissão **ALTER ANY USER** aos usuários no banco de dados independente. Todos os proprietários de banco de dados têm a permissão **ALTER ANY USER** . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auditar os usuários periodicamente em um banco de dados independente.  
  
### <a name="accessing-other-databases-using-the-guest-account"></a>Acessando outros bancos de dados que usam a conta Convidado  
 Os proprietários e os usuários de banco de dados com a permissão **ALTER ANY USER** podem criar usuários de banco de dados independente. Após conectar-se a um banco de dados independente em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um usuário de banco de dados independente poderá acessar outros bancos de dados no [!INCLUDE[ssDE](../../includes/ssde-md.md)], caso os outros bancos de dados tenham habilitado a conta de **convidado** .  
  
### <a name="creating-a-duplicate-user-in-another-database"></a>Criando um usuário duplicado em outro banco de dados  
 Alguns aplicativos podem exigir que um usuário tenha acesso a mais de um banco de dados. Isso pode ser feito por meio da criação de usuários de banco de dados independente idênticos em cada banco de dados. Use a opção de SID ao criar o segundo usuário com a senha. O exemplo a seguir cria dois usuários idênticos em dois bancos de dados.  
  
```  
USE DB1;  
GO  
CREATE USER Carlo WITH PASSWORD = '<strong password>';   
-- Return the SID of the user  
SELECT SID FROM sys.database_principals WHERE name = 'Carlo';  
  
-- Change to the second database  
USE DB2;  
GO  
CREATE USER Carlo WITH PASSWORD = '<same password>', SID = <SID from DB1>;  
GO  
```  
  
 Para executar uma consulta de bancos de dados cruzado, você deve definir a opção **TRUSTWORTHY** no banco de dados de chamada. Por exemplo se o usuário (Carlo) definido acima estiver em DB1, para executar `SELECT * FROM db2.dbo.Table1;` , a configuração **TRUSTWORTHY** deve estar ativada para o banco de dados DB1. Execute o código a seguir para ativar a configuração **TRUSTWORTHY** .  
  
```  
ALTER DATABASE DB1 SET TRUSTWORTHY ON;  
```  
  
### <a name="creating-a-user-that-duplicates-a-login"></a>Criando um usuário que duplica um logon  
 Se um usuário de banco de dados independente com senha for criado com o mesmo nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e se o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conectar especificando o banco de dados independente como catálogo inicial, o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não poderá se conectar. A conexão será avaliada como a entidade do usuário com senha no banco de dados independente em vez de como um usuário baseado no logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Isso pode provocar uma negação intencional ou acidental do serviço para o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Como uma prática recomendada, membros da função de servidor fixa **sysadmin** devem sempre considerar conectar-se com o uso da opção de catálogo inicial. Isso conecta o logon ao banco de dados mestre e evita qualquer tentativa de um proprietário de banco de dados usar indevidamente a tentativa de logon. Em seguida, o administrador pode mudar para o banco de dados independente usando a instrução **USE***\<bancodedados>*. Também é possível definir o banco de dados padrão do logon para o banco de dados independente, o que conclui o logon no **mestre**e, em seguida, transfere o logon para o banco de dados independente.  
  
-   Como uma prática recomendada, não crie usuários de banco de dados independente com senhas que tenham o mesmo nome que logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Se o logon duplicado existir, conecte-se ao banco de dados **mestre** sem especificar um catálogo inicial e execute o comando **USE** para mudar para o banco de dados independente.  
  
-   Quando os bancos de dados independentes estiverem presentes, os usuários de bancos de dados dependentes devem se conectar ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] sem usar um catálogo inicial ou especificando o nome de um banco de dados dependente como catálogo inicial. Isso evita a conexão ao banco de dados independente que está sob controle menos direto pelos administradores do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
### <a name="increasing-access-by-changing-the-containment-status-of-a-database"></a>Aumentando o acesso por meio da alteração do status de contenção de um banco de dados  
 Logons que têm a permissão **ALTER ANY DATABASE** , como membros da função de servidor fixa **dbcreator** , e usuários em um banco de dados dependente que têm a permissão **CONTROL DATABASE** , como membros da função de banco de dados fixa **db_owner** , podem alterar a configuração de contenção de um banco de dados. Se a configuração de contenção de um banco de dados for alterada de **NONE** para **PARTIAL** ou **FULL**, o acesso de usuários poderá ser concedido por meio da criação de usuários de banco de dados independente com senhas. Isso pode fornecer acesso sem o conhecimento ou consentimento dos administradores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para impedir a contenção de qualquer banco de dados, defina a opção **contained database authentication** de [!INCLUDE[ssDE](../../includes/ssde-md.md)] do como 0. Para impedir conexões por usuários de banco de dados independente com senhas em bancos de dados independentes selecionados, use gatilhos de logon para cancelar tentativas de logon por usuários de banco de dados independente com senhas.  
  
### <a name="attaching-a-contained-database"></a>Anexando um banco de dados independente  
 Por meio da anexação de um banco de dados independente, um administrador pode dar acesso não desejado de usuários à instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Um administrador preocupado com esse risco pode colocar o banco de dados online em modo **RESTRICTED_USER** , o que impede a autenticação para usuários de bancos de dados independentes com senha. Apenas entidades autorizadas por meio de logon poderão acessar o [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Os usuários são criados com o uso dos requisitos de senha em vigor no momento em que são criados, e as senhas não são verificadas novamente quando um banco de dados é anexado. Com a anexação de um banco de dados independente que permite senhas fracas a um sistema com uma política de senha mais rígida, um administrador pode permitir senhas que não atendam à política de senha atual no [!INCLUDE[ssDE](../../includes/ssde-md.md)]de anexação. Os administradores podem evitar a contenção de senhas fracas com a exigência de que todas as senhas sejam redefinidas para o banco de dados anexado.  
  
### <a name="password-policies"></a>Políticas de senha  
 É possível exigir senhas fortes em um banco de dados, mas não é possível protegê-las com políticas de senha robusta. Use a Autenticação do Windows sempre que possível para tirar proveito das políticas de senha mais extensivas disponíveis no Windows.  
  
### <a name="kerberos-authentication"></a>Autenticação Kerberos  
 Usuários de bancos de dados independentes com senhas não podem usar a Autenticação Kerberos. Quando possível, use a Autenticação do Windows para tirar proveito dos recursos do Windows, como o Kerberos.  
  
### <a name="offline-dictionary-attack"></a>Ataque de dicionário offline  
 Os hashes de senha de usuários de banco de dados independente com senhas são armazenados no banco de dados independente. Qualquer usuário com acesso aos arquivos de banco de dados pode executar um ataque de dicionário contra os usuários de banco de dados independente com senhas em um sistema não auditado. Para mitigar essa ameaça, restrinja o acesso aos arquivos de banco de dados, ou apenas permita conexões ao bancos de dados contido por meio da Autenticação do Windows.  
  
## <a name="escaping-a-contained-database"></a>Escape de um banco de dados independente  
 Se um banco de dados for parcialmente contido, os administradores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverão auditar os recursos dos usuários e módulos periodicamente em bancos de dados independentes.  
  
## <a name="denial-of-service-through-autoclose"></a>Negação de serviço por meio de AUTO_CLOSE  
 Não configure bancos de dados independentes como fechamento automático. Se fechado, a abertura do banco de dados para autenticar um usuário consumirá recursos adicionais e poderá contribuir para um ataque de negação de serviço.  
  
## <a name="see-also"></a>Consulte também  
 [Bancos de dados independentes](../../relational-databases/databases/contained-databases.md)   
 [Migrar para um banco de dados independente parcialmente](../../relational-databases/databases/migrate-to-a-partially-contained-database.md)  
  
  
