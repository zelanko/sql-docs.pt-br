---
title: "Op&#231;&#227;o de configura&#231;&#227;o de servidor contained database authentication | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "banco de dados independente, habilitando"
  - "opção contained database authentication"
ms.assetid: b80768d2-ac20-4035-a335-d9adb74b3f6e
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 10
---
# Op&#231;&#227;o de configura&#231;&#227;o de servidor contained database authentication
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Use a opção **contained database authentication** para habilitar bancos de dados independentes na instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
 Essa opção de servidor permite controlar **contained database authentication**.  
  
-   Quando **contained database authentication** estiver desativada (0) para a instância, os bancos de dados independentes não poderão ser criados, nem conectados ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Quando **contained database authentication** estiver ativada (1) para a instância, os bancos de dados independentes poderão ser criados ou conectados ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Um banco de dados independente inclui todas as configurações de banco de dados e metadados necessários para definir o banco de dados e não tem nenhuma dependência de configuração da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] onde o banco de dados está instalado. Os usuários podem se conectar ao banco de dados sem autenticar um logon no nível do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . O isolamento do banco de dados do Mecanismo de Banco de Dados facilita mover o banco de dados para outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A inclusão de todas as configurações no banco de dados permite que os proprietários do banco de dados gerenciem todas as configurações do banco de dados. Para obter mais informações sobre bancos de dados independentes, consulte [Contained Databases](../../relational-databases/databases/contained-databases.md).  

> [!NOTE] Bancos de dados independentes estão sempre habilitados para [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] e [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] e não podem ser desabilitados.
  
 Se uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiver bancos de dados independentes, a configuração **contained database authentication** poderá ser definida como 0 por meio da instrução **RECONFIGURE WITH OVERRIDE** . Definir **contained database authentication** como 0 desabilitará a autenticação dos bancos de dados independentes.  
  
> [!IMPORTANT]  
>  Quando os bancos de dados independentes estiverem habilitados, os usuários dos bancos de dados com a permissão ALTER ANY USER, como membros das funções de banco de dados db_owner e db_accessadmin, podem conceder acesso aos bancos de dados e, ao fazer isso, garantir acesso ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso significa que o controle sobre o acesso ao servidor não está mais limitado aos membros do sysadmin e securityadmin fixo de função de servidor e logons com a permissão de CONTROL SERVER e ALTER ANY LOGIN de nível do servidor. Antes de permitir bancos de dados independentes, você deve entender os riscos associados a eles. Para obter mais informações, consulte [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md).  
  
## Exemplos  
 O exemplo a seguir habilita bancos de dados independentes na instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
```tsql  
sp_configure 'contained database authentication', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## Consulte também  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  