---
title: sp_copysubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_copysubscription
- sp_copysubscription_TSQL
helpviewer_keywords:
- sp_copysubscription
ms.assetid: 3c56cd62-2966-4e87-a986-44cb3fd0b760
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8b96c458f38dc43a7d35f00d88b4572a9ae95d5d
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43030317"
---
# <a name="spcopysubscription-transact-sql"></a>sp_copysubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  O recurso de assinaturas anexáveis está preterido e será removido em uma versão futura. Esse recurso não deveria ser usado em novo trabalho de desenvolvimento. Para publicações de mesclagem, que são particionadas usando filtros com parâmetros, recomendamos o uso de novos recursos de instantâneos particionados, que simplificam a inicialização de um grande número de assinaturas. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md). Para publicações que não são particionadas, é possível inicializar uma inscrição com um backup. Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 Copia um banco de dados de assinatura que tem assinatura pull, mas nenhuma assinatura push. Somente bancos de dados de arquivo único podem ser copiados. Esse procedimento armazenado é executado no assinante, no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_copysubscription [ @filename = ] 'file_name'  
    [ , [ @temp_dir = ] 'temp_dir' ]  
    [ , [ @overwrite_existing_file = ] overwrite_existing_file]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@filename =**] **'***file_name***'**  
 É a cadeia de caracteres que especifica o caminho completo, incluindo o nome do arquivo, no qual uma cópia do arquivo de dados (.mdf) é salva. *nome do arquivo* está **nvarchar (260)**, sem padrão.  
  
 [  **@temp_dir=**] **'***temp_dir***'**  
 É o nome do diretório que contém os arquivos temporários. *temp_dir* está **nvarchar (260)**, com um padrão NULL. Se for NULL, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diretório de dados padrão será usado. O diretório deve ter bastante espaço suficiente para conter um arquivo do tamanho de todos os arquivos de banco de dados de assinante combinados.  
  
 [  **@overwrite_existing_file=**] **'***overwrite_existing_file***'**  
 É um sinalizador booliano opcional que especifica se deve ou não substituir um arquivo existente de mesmo nome especificado na **@filename**. *overwrite_existing_file*está **bit**, com um padrão de **0**. Se **1**, ele substituirá o arquivo especificado por **@filename**, se ele existir. Se **0**, o procedimento armazenado falhará se o arquivo existe e o arquivo não será substituído.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_copysubscription** é usado em todos os tipos de replicação para copiar um banco de dados de assinatura para um arquivo como uma alternativa ao aplicar um instantâneo no assinante. O banco de dados deve ser configurado para oferecer suporte somente a assinaturas pull. Usuários com permissões apropriadas podem fazer cópias do banco de dados de assinatura e enviar por email, copiar ou transportar o arquivo de assinatura (.msf) para outro Assinante, onde poderá ser anexado a uma assinatura.  
  
 O tamanho do banco de dados de assinatura copiado deve ser menor de 2 gigabytes (GB).  
  
 **sp_copysubscription** tem suporte apenas para bancos de dados com assinaturas de cliente e não pode ser executado quando o banco de dados tem assinaturas de servidor.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** pode executar a função de servidor fixa **sp_copysubscription**.  
  
## <a name="see-also"></a>Consulte também  
 [Locais da pasta de instantâneos alternativos](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
