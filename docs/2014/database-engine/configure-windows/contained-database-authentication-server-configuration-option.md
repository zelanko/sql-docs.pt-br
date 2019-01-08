---
title: Opção de configuração de servidor contained database authentication | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- contained_database_authentication_TSQL
- contained database authentication
helpviewer_keywords:
- contained database, enabling
- contained database authentication option
ms.assetid: b80768d2-ac20-4035-a335-d9adb74b3f6e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 60b0cca44cae7e71e538fe87d5912a044209d06d
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52641377"
---
# <a name="contained-database-authentication-server-configuration-option"></a>Opção de configuração de servidor contained database authentication
  Use a opção **contained database authentication** para habilitar bancos de dados independentes na instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
 Essa opção de servidor permite controlar **contained database authentication**.  
  
-   Quando **contained database authentication** estiver desativada (0) para a instância, os bancos de dados independentes não poderão ser criados, nem conectados ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Quando **contained database authentication** estiver ativada (1) para a instância, os bancos de dados independentes poderão ser criados ou conectados ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Um banco de dados independente inclui todas as configurações de banco de dados e metadados necessários para definir o banco de dados e não tem nenhuma dependência de configuração da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] onde o banco de dados está instalado. Os usuários podem se conectar ao banco de dados sem autenticar um logon no nível do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . O isolamento do banco de dados do Mecanismo de Banco de Dados facilita mover o banco de dados para outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A inclusão de todas as configurações no banco de dados permite que os proprietários do banco de dados gerenciem todas as configurações do banco de dados. Para obter mais informações sobre bancos de dados independentes, consulte [Contained Databases](../../relational-databases/databases/contained-databases.md).  
  
 Se uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiver bancos de dados independentes, a configuração **contained database authentication** poderá ser definida como 0 por meio da instrução **RECONFIGURE WITH OVERRIDE** . Definir **contained database authentication** como 0 desabilitará a autenticação dos bancos de dados independentes.  
  
> [!IMPORTANT]  
>  Quando os bancos de dados independentes estiverem habilitados, os usuários dos bancos de dados com a permissão ALTER ANY USER, como membros das funções de banco de dados db_owner e db_accessadmin, podem conceder acesso aos bancos de dados e, ao fazer isso, garantir acesso ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso significa que o controle sobre o acesso ao servidor não está mais limitado aos membros do sysadmin e securityadmin fixo de função de servidor e logons com a permissão de CONTROL SERVER e ALTER ANY LOGIN de nível do servidor. Antes de permitir bancos de dados independentes, você deve entender os riscos associados a eles. Para obter mais informações, consulte [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir habilita bancos de dados independentes na instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
```tsql  
sp_configure 'contained database authentication', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
