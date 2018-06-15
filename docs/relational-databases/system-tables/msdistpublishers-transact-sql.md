---
title: MSdistpublishers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
- MSdistpublishers
- MSdistpublishers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistpublishers system table
ms.assetid: 31844099-4b33-4dc9-84b4-bac70aa82598
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2565f080af7fc798a4f53cdaa425387b75652d2b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33006763"
---
# <a name="msdistpublishers-transact-sql"></a>MSdistpublishers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  O **MSdistpublishers** tabela contém uma linha para cada publicador remoto com suporte pelo distribuidor local. Essa tabela é armazenada no **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|É o nome do Distribuidor do Publicador.|  
|**distribution_db**|**sysname**|O nome do banco de dados de distribuição.|  
|**working_directory**|**nvarchar(255)**|O nome do diretório de trabalho usado para armazenar dados e arquivos de esquema para a publicação.|  
|**security_mode**|**Int**|O modo de segurança implementado no Distribuidor.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.<br /><br /> **1** = autenticação do Windows.|  
|**login**|**sysname**|A ID de logon para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**password**|**nvarchar (524)**|A senha (criptografada) para a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Ativo**|**bit**|Indica se o Distribuidor local está em uso pelo Publicador remoto.|  
|**confiável**|**bit**|Indica se o Publicador remoto usa mesma senha que o Distribuidor local.<br /><br /> **0** = A senha é necessária no publicador remoto para conectar-se ao distribuidor.<br /><br /> **1** = nenhuma senha é necessária.|  
|**third_party**|**bit**|Se o Publicador é uma instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalação. **1** = fonte de dados heterogêneos.|  
|**publisher_type**|**sysname**|Tipo de Publicador:<br /><br /> **MSSQLSERVER**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.<br /><br /> **ORACLE** = editor Oracle padrão.<br /><br /> **ORACLE GATEWAY** = editor Oracle Gateway.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
