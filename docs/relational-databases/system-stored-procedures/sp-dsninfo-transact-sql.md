---
title: sp_dsninfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_dsninfo
- sp_dsninfo_TSQL
helpviewer_keywords:
- sp_dsninfo
ms.assetid: 34648615-814b-42bc-95a3-50e86b42ec4d
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 85e70b19b4884eb5bfc7a973177e9fcd52b2f30b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spdsninfo-transact-sql"></a>sp_dsninfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna as informações de fonte de dados ODBC ou OLE DB do Distribuidor associado com o servidor atual. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dsninfo [ @dsn =] 'dsn'   
    [ , [ @infotype =] 'info_type']   
    [ , [ @login =] 'login']   
    [ , [ @password =] 'password']  
    [ , [ @dso_type=] dso_type]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@dsn =**] **'***dsn***'**  
 É o nome do servidor vinculado ODBC DSN ou OLE DB. *DSN* é **varchar (128)**, sem padrão.  
  
 [  **@infotype =**] **'***tipo_info***'**  
 É o tipo de informação a ser retornada. Se *tipo_info* não for especificado ou se NULL for especificado, todos os tipos de informações são retornados. *Tipo_info* é **varchar (128)**, com um padrão NULL, e pode ser um destes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**DBMS_NAME**|Especifica o nome de fornecedor da fonte de dados.|  
|**DBMS_VERSION**|Especifica a versão da fonte de dados.|  
|**DATABASE_NAME**|Especifica o nome do banco de dados.|  
|**SQL_SUBSCRIBER**|Especifica que a fonte de dados pode ser um Assinante.|  
  
 [  **@login =**] **'***login***'**  
 É o logon para a fonte de dados. Se a fonte de dados incluir um logon, especifique NULL ou omita o parâmetro. *logon*é **varchar (128)**, com um padrão NULL.  
  
 [  **@password =**] **'***senha***'**  
 É a senha para o logon. Se a fonte de dados incluir um logon, especifique NULL ou omita o parâmetro. *senha*é **varchar (128)**, com um padrão NULL.  
  
 [  **@dso_type=**] *dso_type*  
 É o tipo da fonte de dados. *dso_type* é **int**, e pode ser um destes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**1** (padrão)|Fonte de dados ODBC|  
|**3**|Fonte de dados OLE DB|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**Tipo de informação**|**nvarchar(64)**|Tipos de informações como DBMS_NAME, DBMS_VERSION, DATABASE_NAME, SQL_SUBSCRIBER.|  
|**Value**|**nvarchar(512)**|Valor do tipo de informação associado.|  
  
## <a name="remarks"></a>Remarks  
 **sp_dsninfo** é usado em todos os tipos de replicação.  
  
 **sp_dsninfo** recupera ODBC ou OLE DB informações fonte de dados que mostra se o banco de dados pode ser usado para replicação ou consulta.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa **sp_dsninfo**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_enumdsn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumdsn-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
