---
title: sp_help_log_shipping_primary_secondary (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_primary_secondary
- sp_help_log_shipping_primary_secondary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_primary_secondary
ms.assetid: bc0044b4-7831-4ff9-8856-825c76aa9893
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3d1c93bb6fecea955e139688b1a8f4f2c1dccc75
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68066818"
---
# <a name="sp_help_log_shipping_primary_secondary-transact-sql"></a>sp_help_log_shipping_primary_secondary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esse procedimento armazenado retorna informações relativas a todos os bancos de dados secundários de um determinado banco de dados primário.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_log_shipping_primary_secondary  
[ @primary_database = ] 'primary_database'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @primary_database = ] 'primary_database'`É o nome do banco de dados no servidor primário. *primary_database* é **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|DESCRIÇÃO|  
|-----------------|-----------------|  
|**secondary_server**|O nome da instância secundária do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] na configuração de envio de logs.|  
|**secondary_database**|Nome do banco de dados secundário na configuração de envio de logs.|  
  
## <a name="remarks"></a>Comentários  
 **sp_help_log_shipping_primary_secondary** deve ser executado do banco de dados **mestre** no servidor primário.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo ilustra o uso de **sp_help_log_shipping_primary_secondary** para recuperar uma lista de bancos de dados secundários associados ao [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]banco de dados primário.  
  
```  
EXECUTE master.dbo.sp_help_log_shipping_primary_secondary @primary_database=N'AdventureWorks';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
