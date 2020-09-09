---
description: sp_dropdevice (Transact-SQL)
title: sp_dropdevice (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropdevice_TSQL
- sp_dropdevice
dev_langs:
- TSQL
helpviewer_keywords:
- backup devices [SQL Server], deleting
- sp_dropdevice
ms.assetid: c8b07189-7c35-414b-acc1-45bd6e7e17c3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: de658ea419fe2fe6fcdfbbdd2b335cf5abb12e2e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543480"
---
# <a name="sp_dropdevice-transact-sql"></a>sp_dropdevice (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Remove um dispositivo de banco de dados ou um dispositivo de backup de uma instância do [!INCLUDE[ssDEversion2005](../../includes/ssdeversion2005-md.md)] , excluindo a entrada de ** dispositivosmaster.dbo.sys**.  
   
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropdevice [ @logicalname = ] 'device'   
    [ , [ @delfile = ] 'delfile' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @logicalname = ] 'device'` É o nome lógico do dispositivo de banco de dados ou dispositivo de backup, conforme listado em **master.dbo.sysDevices.Name**. o *dispositivo* é **sysname**, sem padrão.  
  
`[ @delfile = ] 'delfile'` Especifica se o arquivo do dispositivo de backup físico deve ser excluído. *parâmetro delfile* é **varchar (7)**. Se especificado como **parâmetro delfile**, o arquivo de disco do dispositivo de backup físico será excluído.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 **sp_dropdevice** não pode ser usada dentro de uma transação.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de servidor fixa **diskadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir descarta o dispositivo de despejo de fita `tapedump1` do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
```  
EXEC sp_dropdevice 'tapedump1';  
```  
  
## <a name="see-also"></a>Confira também  
 [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Excluir um dispositivo de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpdb ](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpdevice ](../../relational-databases/system-stored-procedures/sp-helpdevice-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
