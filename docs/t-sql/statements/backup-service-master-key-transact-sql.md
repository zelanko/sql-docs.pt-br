---
title: "CHAVE MESTRA de serviço de BACKUP (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BACKUP SERVICE MASTER KEY
- DUMP_SERVICE_MASTER_KEY_TSQL
- DUMP SERVICE MASTER KEY
- BACKUP_SERVICE_MASTER_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backing up service master keys [SQL Server]
- BACKUP SERVICE MASTER KEY statement
- cryptography [SQL Server], Service Master Key
- exporting Service Master Keys
- encryption [SQL Server], Service Master Key
- service master key [SQL Server], exporting
ms.assetid: f8356683-6680-4f1c-9eaf-5c29a9a9020d
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dd3f95e0f3606d23dd1418b2cc0b3b32b5c61ac8
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="backup-service-master-key-transact-sql"></a>BACKUP SERVICE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exporta a chave mestra do serviço.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BACKUP SERVICE MASTER KEY TO FILE = 'path_to_file'   
    ENCRYPTION BY PASSWORD = 'password'  
```  
  
## <a name="arguments"></a>Argumentos  
 ARQUIVO **='***path_to_file***'**  
 Especifica o caminho completo, inclusive o nome de arquivo, para o arquivo para o qual a chave mestra de serviço será exportada. Esse pode ser um caminho local ou um caminho de UNC a um local de rede.  
  
 SENHA **='***senha***'**  
 A senha usada para criptografar a chave mestra do serviço está no o arquivo de backup. Esta senha está sujeita à verificação de complexidade. Para obter mais informações, consulte [Password Policy](../../relational-databases/security/password-policy.md).  
  
## <a name="remarks"></a>Comentários  
 A chave mestra do serviço deveria ter seu backup feito e ser armazenada em um local seguro, fora do site. Criar este backup deveria ser uma das primeiras ações administrativas executadas no servidor.  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão CONTROL SERVER no servidor.  
  
## <a name="examples"></a>Exemplos  
 No exemplo seguinte, a chave mestra do serviço tem seu backup feito para um arquivo.  
  
```  
BACKUP SERVICE MASTER KEY TO FILE = 'c:\temp_backups\keys\service_master_key' ENCRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTERAR a chave MESTRA de serviço &#40; Transact-SQL &#41;](../../t-sql/statements/alter-service-master-key-transact-sql.md)   
 [RESTORE SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-service-master-key-transact-sql.md)  
  
  
