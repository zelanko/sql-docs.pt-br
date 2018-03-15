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
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_MASTER_KEY_TSQL
- MASTER_KEY_TSQL
- MASTER KEY
- CREATE MASTER KEY
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], Database Master Key
- database master key [SQL Server]
- CREATE MASTER KEY statement
- cryptography [SQL Server], Database Master Key
- database master key [SQL Server], creating
ms.assetid: 1710a305-1a4f-48ec-836c-11ffd0356d76
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aaec4d28dc95d792faa6406ef68df50167d0f091
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
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
 PASSWORD ='*password*'  
 É a senha usada para criptografar a chave mestra no banco de dados. A *password* deve atender aos requisitos da política de senha do Windows do computador que executa a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *password* é opcional no [!INCLUDE[ssSDS](../../includes/sssds-md.md)] e [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)].  
  
## <a name="remarks"></a>Remarks  
 A chave mestra do banco de dados é uma chave simétrica usada para proteger as chaves privadas dos certificados e as chaves assimétricas presentes no banco de dados. Quando é criada, a chave mestra é criptografada com o algoritmo AES_256 e uma senha fornecida pelo usuário. No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e no [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], o algoritmo DES triplo é usado. Para permitir a descriptografia automática da chave mestra, uma cópia da chave é criptografada usando a chave mestra de serviço e armazenada no banco de dados atual e no mestre. Normalmente, a cópia armazenada em mestre é silenciosamente atualizada sempre que a chave mestra é alterada. Esse padrão pode ser alterado com a opção DROP ENCRYPTION BY SERVICE MASTER KEY de [ALTER MASTER KEY](../../t-sql/statements/alter-master-key-transact-sql.md). Uma chave mestra não criptografada pela chave mestra de serviço deve ser aberta com a instrução [OPEN MASTER KEY](../../t-sql/statements/open-master-key-transact-sql.md) e uma senha.  
  
 A coluna is_master_key_encrypted_by_server da exibição do catálogo sys.databases em mestre indica se a chave mestra do banco de dados é criptografada pela chave mestra de serviço.  
  
 Informações sobre a chave mestra de banco de dados são visíveis na exibição do catálogo sys.symmetric_keys.  

Para o SQL Server e o Parallel Data Warehouse, a Chave Mestra normalmente é protegida pela Chave Mestra de Serviço e por, pelo menos, uma senha. No caso do banco de dados que está sendo movido fisicamente para outro servidor (envio de logs, a restauração do backup, etc.), o banco de dados conterá uma cópia da Chave mestra criptografada pela Chave Mestra de Serviço do servidor original (a menos que essa criptografia tenha sido explicitamente removida com ALTER MASTER KEY DDL) e uma cópia criptografada por cada senha especificada durante as operações CREATE MASTER KEY ou ALTER MASTER KEY DDL seguintes. Para recuperar a Chave Mestra e todos os dados criptografados usando a Chave Mestra como a raiz na hierarquia de chaves depois que o banco de dados foi movido, o usuário precisará usar a instrução OPEN MASTER KEY com uma das senhas usadas para proteger a Chave Mestra, restaurar um backup da Chave Mestra ou restaurar um backup da Chave Mestra de Serviço original no novo servidor. 

Para o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] e o [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)], a proteção por senha não é considerada um mecanismo de segurança para prevenir um cenário de perda de dados em situações em que o banco de dados pode ser movido de um servidor para outro, pois a proteção da Chave Mestra de Serviço na Chave Mestra é gerenciada pela plataforma Microsoft Azure. Portanto, a senha da Chave Mestra é opcional no [!INCLUDE[ssSDS](../../includes/sssds-md.md)] e no [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)].
  
> [!IMPORTANT]  
>  Faça o backup da chave mestra usando [BACKUP MASTER KEY](../../t-sql/statements/backup-master-key-transact-sql.md) e armazene-o em um local seguro e externo.  
  
 A chave mestra de serviço e as chaves mestras de banco de dados são protegidas pelo algoritmo AES-256.  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão CONTROL no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma chave mestra de banco de dados para o banco de dados atual. A chave é criptografada usando a senha `23987hxJ#KL95234nl0zBe`.  
  
```  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  
GO  
```  

  
## <a name="see-also"></a>Consulte Também  
 [sys.symmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [OPEN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [DROP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [CLOSE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  


