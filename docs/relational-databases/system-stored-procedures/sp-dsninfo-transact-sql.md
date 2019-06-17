---
title: sp_dsninfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dsninfo
- sp_dsninfo_TSQL
helpviewer_keywords:
- sp_dsninfo
ms.assetid: 34648615-814b-42bc-95a3-50e86b42ec4d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e6eacb453fc2f66f4b87790770fa50916916a27c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62724011"
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
`[ @dsn = ] 'dsn'` É o nome do servidor vinculado ODBC DSN ou OLE DB. *DSN* está **varchar (128)** , sem padrão.  
  
`[ @infotype = ] 'info_type'` É o tipo de informação a ser retornada. Se *tipo_info* não for especificado ou se NULL for especificado, todos os tipos de informações são retornados. *Tipo_info* está **varchar (128)** , com um padrão de NULL, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**DBMS_NAME**|Especifica o nome de fornecedor da fonte de dados.|  
|**DBMS_VERSION**|Especifica a versão da fonte de dados.|  
|**DATABASE_NAME**|Especifica o nome do banco de dados.|  
|**SQL_SUBSCRIBER**|Especifica que a fonte de dados pode ser um Assinante.|  
  
`[ @login = ] 'login'` É o logon da fonte de dados. Se a fonte de dados incluir um logon, especifique NULL ou omita o parâmetro. *login*está **varchar (128)** , com um padrão NULL.  
  
`[ @password = ] 'password'` É a senha para o logon. Se a fonte de dados incluir um logon, especifique NULL ou omita o parâmetro. *senha*está **varchar (128)** , com um padrão NULL.  
  
`[ @dso_type = ] dso_type` É o tipo de fonte de dados. *dso_type* está **int**, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1** (padrão)|Fonte de dados ODBC|  
|**3**|Fonte de dados OLE DB|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**Tipo de informação**|**nvarchar(64)**|Tipos de informações como DBMS_NAME, DBMS_VERSION, DATABASE_NAME, SQL_SUBSCRIBER.|  
|**Value**|**nvarchar(512)**|Valor do tipo de informação associado.|  
  
## <a name="remarks"></a>Comentários  
 **sp_dsninfo** é usado em todos os tipos de replicação.  
  
 **sp_dsninfo** recupera ODBC ou OLE DB informações fonte de dados que mostra se o banco de dados pode ser usado para replicação ou consulta.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** pode executar a função de servidor fixa **sp_dsninfo**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_enumdsn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumdsn-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
