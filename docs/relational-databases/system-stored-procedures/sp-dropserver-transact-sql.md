---
title: sp_dropserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropserver_TSQL
- sp_dropserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropserver
ms.assetid: 0fc83e35-0caa-49a3-a4b6-a1890d4f46ef
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 0155b154a1d63343c157bc2eca6e5cbd7c1b8968
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68124834"
---
# <a name="sp_dropserver-transact-sql"></a>sp_dropserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Remove um servidor da lista de servidores remotos e vinculados conhecidos na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link](../../database-engine/configure-windows/media/topic-link.gif "ícone de link") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
sp_dropserver [ @server = ] 'server'   
     [ , [ @droplogins = ] { 'droplogins' | NULL} ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *servidor*  
 É o servidor a ser removido. o *servidor* é **sysname**, sem padrão. o *servidor* deve existir.  
  
 *droplogins*  
 Indica que os logons de servidor remoto e vinculado relacionados ao *servidor* também devem ser removidos se **droplogins** for especificado. **`@droplogins`** é **Char (10)**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Se você executar **sp_dropserver** em um servidor que tenha entradas de logon de servidor remotas e vinculadas associadas, ou estiver configurado como um Publicador de replicação, uma mensagem de erro será retornada. Para remover todos os logons de servidor remoto e vinculado de um servidor quando você remove o servidor, use o argumento **droplogins** .  
  
 **sp_dropserver** não pode ser executado dentro de uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer permissão ALTER ANY LINKED SERVER no servidor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte remove o servidor remoto `ACCOUNTS` e todos os logons remotos associados da instância local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
sp_dropserver 'ACCOUNTS', 'droplogins';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addserver](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropremotelogin](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpremotelogin](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpserver](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
