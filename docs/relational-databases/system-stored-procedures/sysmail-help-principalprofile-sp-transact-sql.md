---
title: sysmail_help_principalprofile_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_principalprofile_sp_TSQL
- sysmail_help_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_principalprofile_sp
ms.assetid: 0cfd6464-09c7-4f03-9d25-58001c096a9e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 024eec5c9e74eb48ac57dcf16a40a7783d79f5b3
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890889"
---
# <a name="sysmail_help_principalprofile_sp-transact-sql"></a>sysmail_help_principalprofile_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Lista informações sobre associações entre perfis de Database Mail e entidades do banco de dados.  
  
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_help_principalprofile_sp [ {   [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ]  
    [ [ , ] {   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @principal_id = ] principal_id`É a ID do usuário do banco de dados ou da função no banco de dados **msdb** para a associação a ser listada. *principal_id* é **int**, com um padrão de NULL. *Principal_id* ou *principal_name* pode ser especificado.  
  
`[ @principal_name = ] 'principal_name'`É o nome do usuário do banco de dados ou da função no banco de dados **msdb** para a associação a ser listada. *principal_name* é **sysname**, com um padrão de NULL. *Principal_id* ou *principal_name* pode ser especificado.  
  
`[ @profile_id = ] profile_id`É a ID do perfil para a associação a ser listada. *profile_id* é **int**, com um padrão de NULL. *Profile_id* ou *profile_name* pode ser especificado.  
  
`[ @profile_name = ] 'profile_name'`É o nome do perfil para a associação a ser listada. *profile_name* é **sysname**, com um padrão de NULL. *Profile_id* ou *profile_name* pode ser especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Retorna um conjunto de resultados que contém as colunas listadas na tabela a seguir.  
  
||||  
|-|-|-|  
|Nome da coluna|Tipo de dados|Descrição|  
|**principal_id**|**int**|O ID do usuário do banco de dados.|  
|**principal_name**|**sysname**|O nome do usuário do banco de dados.|  
|**profile_id**|**int**|O número do ID do perfil de Database Mail.|  
|**profile_name**|**sysname**|O nome do perfil de Database Mail.|  
|**is_default**|**bit**|O sinalizador que indica se este é o perfil padrão do usuário.|  
  
## <a name="remarks"></a>Comentários  
 Se **sysmail_help_principalprofile_sp** for invocado sem parâmetros, o conjunto de resultados retornado listará todas as associações na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Caso contrário, o conjunto de resultados conterá informações sobre as associações correspondentes aos parâmetros fornecidos. Por exemplo, o procedimento lista todas as associações de um perfil quando o nome de perfil for fornecido.  
  
 **sysmail_help_principalprofile_sp** está no banco de dados **msdb** e pertence ao esquema **dbo** . O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-information-for-a-specific-association"></a>a. Listando informações de uma associação específica  
 O exemplo a seguir mostra a lista de informações de todas as associações entre o perfil `AdventureWorks Administrator` e a entidade `ApplicationLogin` no banco de dados `msdb`.  
  
```  
EXECUTE msdb.dbo.sysmail_help_principalprofile_sp  
    @principal_name = 'danw',  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
 Conjunto de resultados de exemplo, reformatado para comprimento de linha.  
  
```  
principal_id principal_name     profile_id  profile_name                   is_default  
------------ ------------------ ----------- ------------------------------ ----------  
5            danw               9           AdventureWorks Administrator   1  
```  
  
### <a name="b-listing-information-for-all-associations"></a>B. Listando informações de todas as associações  
 O exemplo a seguir mostra a lista de informações de todas as associações na instância.  
  
```  
EXECUTE msdb.dbo.sysmail_help_principalprofile_sp ;  
```  
  
 Conjunto de resultados de exemplo, reformatado para comprimento de linha.  
  
```  
principal_id principal_name     profile_id  profile_name                   is_default  
------------ ------------------ ----------- ------------------------------ ----------  
6            terrid             3           Product Update Profile         1  
5            danw               9           AdventureWorks Administrator   1  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
