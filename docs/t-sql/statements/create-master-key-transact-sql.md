---
title: CREATE MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_MASTER_KEY_TSQL
- MASTER_KEY_TSQL
- MASTER KEY
- CREATE MASTER KEY
dev_langs: TSQL
helpviewer_keywords:
- encryption [SQL Server], Database Master Key
- database master key [SQL Server]
- CREATE MASTER KEY statement
- cryptography [SQL Server], Database Master Key
- database master key [SQL Server], creating
ms.assetid: 1710a305-1a4f-48ec-836c-11ffd0356d76
caps.latest.revision: "50"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aaec4d28dc95d792faa6406ef68df50167d0f091
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="create-master-key-transact-sql"></a>CREATE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Cria uma chave mestra de banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Parallel Data Warehouse  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password'  
[ ; ]  
```  
  
```  
-- Syntax for Azure SQL Database and Azure SQL Data Warehouse  
  
CREATE MASTER KEY [ ENCRYPTION BY PASSWORD ='password' ]
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 SENHA ='*senha*'  
 É a senha usada para criptografar a chave mestra no banco de dados. *senha* devem atender aos requisitos da política de senha do Windows do computador que está executando a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *senha* é opcional em [!INCLUDE[ssSDS](../../includes/sssds-md.md)] e [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)].  
  
## <a name="remarks"></a>Comentários  
 A chave mestra do banco de dados é uma chave simétrica usada para proteger as chaves privadas dos certificados e as chaves assimétricas presentes no banco de dados. Quando é criada, a chave mestra é criptografada com o algoritmo AES_256 e uma senha fornecida pelo usuário. No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e no [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], o algoritmo DES triplo é usado. Para permitir a descriptografia automática da chave mestra, uma cópia da chave é criptografada usando a chave mestra de serviço e armazenada no banco de dados atual e no mestre. Normalmente, a cópia armazenada em mestre é silenciosamente atualizada sempre que a chave mestra é alterada. Esse padrão pode ser alterado usando a opção DROP ENCRYPTION BY SERVICE MASTER KEY de [ALTER MASTER KEY](../../t-sql/statements/alter-master-key-transact-sql.md). Uma chave mestra não criptografada pela chave mestra de serviço deve ser aberta usando o [OPEN MASTER KEY](../../t-sql/statements/open-master-key-transact-sql.md) instrução e uma senha.  
  
 A coluna is_master_key_encrypted_by_server da exibição do catálogo sys.databases em mestre indica se a chave mestra do banco de dados é criptografada pela chave mestra de serviço.  
  
 Informações sobre a chave mestra de banco de dados são visíveis na exibição do catálogo sys.symmetric_keys.  

Para o SQL Server e o Parallel Data Warehouse, a chave mestra normalmente é protegida pela chave mestra de serviço e a senha de pelo menos um. No caso do banco de dados que está sendo movido fisicamente em um servidor diferente (envio de logs, a restauração do backup, etc.), o banco de dados conterá uma cópia da chave mestra criptografada pela chave mestra de serviço de servidor original (a menos que essa criptografia foi explicitamente removida usando ALTER MASTER KEY DDL) e uma cópia criptografada por cada senha especificada durante CREATE MASTER KEY ou as operações ALTER MASTER KEY DDL subsequentes. Para recuperar a chave mestra e todos os dados criptografados usando a chave mestra como a raiz da hierarquia de chave depois que o banco de dados foi movido, o usuário terá qualquer uso instrução OPEN MASTER KEY usando um a senha usada para proteger a chave mestra , restaure um backup da chave mestra ou restaurar um backup de original chave mestra de serviço no novo servidor. 

Para [!INCLUDE[ssSDS](../../includes/sssds-md.md)] e [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)], a proteção de senha não é considerada para ser um mecanismo de segurança para impedir que um cenário de perda de dados em situações em que o banco de dados pode ser movido de um servidor para outro, como a proteção de chave mestra de serviço na chave mestra gerenciado pela plataforma do Microsoft Azure. Portanto, a senha da chave mestre é opcional em [!INCLUDE[ssSDS](../../includes/sssds-md.md)] e [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)].
  
> [!IMPORTANT]  
>  Você deve fazer backup da chave mestra usando [BACKUP MASTER KEY](../../t-sql/statements/backup-master-key-transact-sql.md) e armazene o backup em um local externo seguro.  
  
 A chave mestra de serviço e as chaves mestras de banco de dados são protegidas pelo algoritmo AES-256.  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão CONTROL no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma chave mestra de banco de dados para o banco de dados atual. A chave é criptografada usando a senha `23987hxJ#KL95234nl0zBe`.  
  
```  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  
GO  
```  

  
## <a name="see-also"></a>Consulte também  
 [symmetric_keys &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Abra a chave MESTRA &#40; Transact-SQL &#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [DROP MASTER KEY &#40; Transact-SQL &#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [CLOSE MASTER KEY &#40; Transact-SQL &#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  


