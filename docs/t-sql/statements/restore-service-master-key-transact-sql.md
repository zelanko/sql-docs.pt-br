---
title: RESTORE SERVICE MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RESTORE SERVICE MASTER KEY
- RESTORE_SERVICE_MASTER_KEY_TSQL
- LOAD SERVICE MASTER KEY
- LOAD_SERVICE_MASTER_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- importing Service Master Keys
- copying Service Master Keys
- service master key [SQL Server], importing
- RESTORE SERVICE MASTER KEY statement
- transferring Service Master Keys
ms.assetid: a68fd0ee-70ce-4104-aca0-fcae5f41fc38
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: ee122adb459586f370f2b115f161c56468f4ce7a
ms.sourcegitcommit: c6e71ed14198da67afd7ba722823b1af9b4f4e6f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54327657"
---
# <a name="restore-service-master-key-transact-sql"></a>RESTORE SERVICE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Importa uma chave mestra de serviço de um arquivo de backup.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RESTORE SERVICE MASTER KEY FROM FILE = 'path_to_file'   
    DECRYPTION BY PASSWORD = 'password' [FORCE]  
```  
  
## <a name="arguments"></a>Argumentos  
 FILE **='**_path\_to\_file_**'**  
 Especifica o caminho completo, inclusive o nome do arquivo, para a chave mestra do serviço. *path_to_file* pode ser um caminho local ou um caminho UNC para um local de rede.  
  
 PASSWORD **='**_password_**'**  
 Especifica a senha exigida para decifrar a chave mestra de serviço que está sendo importada de um arquivo.  
  
 FORCE  
 Força a substituição da chave mestra de serviço, mesmo com o risco de perda de dados.  
  
## <a name="remarks"></a>Remarks  
 Quando a chave mestra de serviço é restaurada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] descriptografa todas as chaves e segredos que foram criptografados com a chave mestra de serviço atual e, em seguida, criptografa a chave mestra de serviço carregada do arquivo de backup.  
  
 Se qualquer uma dessas descriptografias falhar, a restauração falhará. É possível usar a opção FORCE para ignorar erros, mas essa opção causará a perda dos dados que não puderem ser descriptografados.  
  
> [!CAUTION]  
>  A chave mestra de serviço é a raiz da hierarquia de criptografia do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A chave mestra de serviço protege todas as outras chaves diretamente ou indiretamente na árvore. Se uma chave dependente não puder ser descriptografada durante uma restauração forçada, os dados protegidos por ela serão perdidos.  
  
 A nova geração da hierarquia de criptografia é uma operação que utiliza muitos recursos. É recomendável agendá-la em um período de baixa demanda.  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão CONTROL SERVER no servidor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir restaura a chave mestra de serviço de um arquivo de backup.  
  
```  
RESTORE SERVICE MASTER KEY   
    FROM FILE = 'c:\temp_backups\keys\service_master_key'   
    DECRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Chave Mestra do Serviço](../../relational-databases/security/encryption/service-master-key.md)   
 [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-service-master-key-transact-sql.md)   
 [BACKUP SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/backup-service-master-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
