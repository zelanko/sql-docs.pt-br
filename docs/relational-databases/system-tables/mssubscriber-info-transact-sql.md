---
title: MSsubscriber_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSsubscriber_info_TSQL
- MSsubscriber_info
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriber_info system table
ms.assetid: 5ca22f41-6020-4f72-8110-e69baf3447cb
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 33b09b942cea3fc8e2da711ef956e86e85119a5d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mssubscriberinfo-transact-sql"></a>MSsubscriber_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSsubscriber_info** tabela contém uma linha para cada par de publicador/assinante que está sendo enviada assinaturas do distribuidor local. Esta tabela é armazenada no banco de dados de distribuição.  
  
 **Observação** esta tabela do sistema foi preterida e está sendo mantida para oferecer suporte a versões anteriores do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|O nome do publicador.|  
|**Assinante**|**sysname**|O nome do Assinante.|  
|**type**|**tinyint**|O tipo de assinante:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinante.<br /><br /> **1** = fonte de dados ODBC.|  
|**login**|**sysname**|O logon para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Armazenado em formato criptografado se o Assinante for adicionado com o modo de Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**password**|**nvarchar (524)**|A senha para a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Armazenado em formato criptografado se o Assinante for adicionado com o modo de Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Descrição**|**nvarchar(255)**|A descrição do Assinante.|  
|**security_mode**|**Int**|O modo de segurança implementado:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticação do Windows.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
