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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b0cf48f494c04bd57e1bf20930917e4f9a3d015b
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39102674"
---
# <a name="msdistpublishers-transact-sql"></a>MSdistpublishers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  O **MSdistpublishers** tabela contém uma linha para cada publicador remoto com suporte pelo distribuidor local. Essa tabela é armazenada na **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|É o nome do Distribuidor do Publicador.|  
|**distribution_db**|**sysname**|O nome do banco de dados de distribuição.|  
|**working_directory**|**nvarchar(255)**|O nome do diretório de trabalho usado para armazenar dados e arquivos de esquema para a publicação.|  
|**security_mode**|**int**|O modo de segurança implementado no Distribuidor.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.<br /><br /> **1** = autenticação do Windows.|  
|**login**|**sysname**|A ID de logon para Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**password**|**nvarchar(524)**|A senha (criptografada) para a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Active Directory**|**bit**|Indica se o Distribuidor local está em uso pelo Publicador remoto.|  
|**confiável**|**bit**|Indica se o Publicador remoto usa mesma senha que o Distribuidor local.<br /><br /> **0** = uma senha é necessária no publicador remoto para se conectar ao distribuidor.<br /><br /> **1** = nenhuma senha é necessária.|  
|**third_party**|**bit**|Se o Publicador é uma instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalação. **1** = fonte de dados heterogêneos.|  
|**publisher_type**|**sysname**|Tipo de Publicador:<br /><br /> **MSSQLSERVER**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.<br /><br /> **ORACLE** = editor Oracle padrão.<br /><br /> **ORACLE GATEWAY** = editor Oracle Gateway.|  
|**storage_connection_string**|**nvarchar(779)**|Valor da cadeia de conexão de armazenamento do banco de dados SQL.|  

  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
