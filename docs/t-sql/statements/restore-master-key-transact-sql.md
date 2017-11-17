---
title: RESTORE MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RESTORE_MASTER_KEY_TSQL
- RESTORE MASTER KEY
- LOAD_MASTER_KEY_TSQL
- LOAD MASTER KEY
dev_langs:
- TSQL
helpviewer_keywords:
- database master key [SQL Server], importing
- encryption [SQL Server], Database Master Key
- copying Database Master Keys
- importing Database Master Keys
- cryptography [SQL Server], Database Master Key
- transferring Database Master Keys
- RESTORE MASTER KEY statement
ms.assetid: 70ceb951-31a2-4fc4-a0c1-e6c18eeb3ae7
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 941c6bd886615588ca74bf92de6665e25db224a0
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="restore-master-key-transact-sql"></a>RESTORE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Importa uma chave mestra de banco de dados de um arquivo de backup.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RESTORE MASTER KEY FROM FILE = 'path_to_file'   
    DECRYPTION BY PASSWORD = 'password'  
    ENCRYPTION BY PASSWORD = 'password'  
    [ FORCE ]  
```  
  
## <a name="arguments"></a>Argumentos  
 ARQUIVO ='*path_to_file*'  
 Especifica o caminho completo, inclusive o nome do arquivo, para a chave mestra do banco de dados armazenado. *path_to_file* pode ser um caminho local ou um caminho UNC para um local de rede.  
  
 DECRYPTION BY PASSWORD ='*senha*'  
 Especifica a senha exigida para decifrar a chave mestra de banco de dados que está sendo importada de um arquivo.  
  
 ENCRYPTION BY PASSWORD ='*senha*'  
 Especifica a senha usada para criptografar a chave mestra de banco de dados depois que ela é carregada no banco de dados.  
  
 FORCE  
 Especifica que o processo RESTORE deve continuar, mesmo que a chave mestra de banco de dados atual não seja aberta ou se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não puder descriptografar algumas chaves particulares criptografadas com ela.  
  
## <a name="remarks"></a>Comentários  
 Quando a chave mestra é restaurada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] descriptografa todas as chaves atualmente criptografadas com a chave mestra ativa e criptografa essas chaves com a chave mestra restaurada. Essa operação de uso intensivo de recursos deve ser agendada em um período de baixa demanda. Se a chave mestra de banco de dados atual não for aberta ou não puder ser aberta, ou se qualquer chave criptografada com ela não puder ser descriptografada, a operação de restauração falhará.  
  
 Use a opção de FORCE somente se a chave mestra for irrecuperável ou se descriptografia falhar. As informações que só são criptografadas por uma chave irrecuperável serão perdidas.  
  
 Se a chave mestra foi criptografada pela chave mestra de serviço, a chave mestra restaurada também será criptografada pela chave mestra de serviço.  
  
 Se não houver nenhuma chave mestra no banco de dados atual, RESTORE MASTER KEY criará uma chave mestra. A nova chave mestra não será criptografada automaticamente com a chave mestra de serviço.  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão CONTROL no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir restaura a chave mestra de banco de dados do banco de dados `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
RESTORE MASTER KEY   
    FROM FILE = 'c:\backups\keys\AdventureWorks2012_master_key'   
    DECRYPTION BY PASSWORD = '3dH85Hhk003#GHkf02597gheij04'   
    ENCRYPTION BY PASSWORD = '259087M#MyjkFkjhywiyedfgGDFD';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

