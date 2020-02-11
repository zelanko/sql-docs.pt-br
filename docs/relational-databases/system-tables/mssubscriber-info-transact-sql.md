---
title: MSsubscriber_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscriber_info_TSQL
- MSsubscriber_info
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriber_info system table
ms.assetid: 5ca22f41-6020-4f72-8110-e69baf3447cb
author: stevestein
ms.author: sstein
ms.openlocfilehash: 45065f7cde525d65997df2c97c972d684cadd90f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68139817"
---
# <a name="mssubscriber_info-transact-sql"></a>MSsubscriber_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSsubscriber_info** contém uma linha para cada par Publicador/Assinante que está sendo enviado por push de assinaturas do distribuidor local. Esta tabela é armazenada no banco de dados de distribuição.  
  
 **Observação** Esta tabela do sistema foi preterida e está sendo mantida para dar suporte a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]versões anteriores do.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**Publicador**|**sysname**|O nome do Publicador.|  
|**Assinante**|**sysname**|O nome do Assinante.|  
|**tipo**|**tinyint**|O tipo de assinante:<br /><br /> **** =  0[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinante.<br /><br /> **1** = fonte de dados ODBC.|  
|**entrar**|**sysname**|O logon para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Armazenado em formato criptografado se o Assinante for adicionado com o modo de Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**password**|**nvarchar (524)**|A senha para a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Armazenado em formato criptografado se o Assinante for adicionado com o modo de Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ndescrição**|**nvarchar (255)**|A descrição do Assinante.|  
|**security_mode**|**int**|O modo de segurança implementado:<br /><br /> **** =  0[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.<br /><br /> **** =  1[!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticação do Windows.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
