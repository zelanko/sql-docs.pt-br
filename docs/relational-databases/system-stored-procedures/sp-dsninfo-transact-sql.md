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
ms.openlocfilehash: cb67524304807eba6765387590fd53a52b92f19a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68124713"
---
# <a name="sp_dsninfo-transact-sql"></a>sp_dsninfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna as informações de fonte de dados ODBC ou OLE DB do Distribuidor associado com o servidor atual. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dsninfo [ @dsn =] 'dsn'   
    [ , [ @infotype =] 'info_type']   
    [ , [ @login =] 'login']   
    [ , [ @password =] 'password']  
    [ , [ @dso_type=] dso_type]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @dsn = ] 'dsn'`É o nome do DSN ODBC ou OLE DB servidor vinculado. o *DSN* é **varchar (128)**, sem padrão.  
  
`[ @infotype = ] 'info_type'`É o tipo de informação a ser retornado. Se *info_type* não for especificado ou se NULL for especificado, todos os tipos de informações serão retornados. *info_type* é **varchar (128)**, com um padrão de NULL, e pode ser um desses valores.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**DBMS_NAME**|Especifica o nome de fornecedor da fonte de dados.|  
|**DBMS_VERSION**|Especifica a versão da fonte de dados.|  
|**DATABASE_NAME**|Especifica o nome do banco de dados.|  
|**SQL_SUBSCRIBER**|Especifica que a fonte de dados pode ser um Assinante.|  
  
`[ @login = ] 'login'`É o logon da fonte de dados. Se a fonte de dados incluir um logon, especifique NULL ou omita o parâmetro. o *logon*é **varchar (128)**, com um padrão de NULL.  
  
`[ @password = ] 'password'`É a senha para o logon. Se a fonte de dados incluir um logon, especifique NULL ou omita o parâmetro. a *senha*é **varchar (128)**, com um padrão de NULL.  
  
`[ @dso_type = ] dso_type`É o tipo de fonte de dados. *dso_type* é **int**e pode ser um desses valores.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**1** (padrão)|Fonte de dados ODBC|  
|**Beta**|Fonte de dados OLE DB|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**Information Type**|**nvarchar (64)**|Tipos de informações como DBMS_NAME, DBMS_VERSION, DATABASE_NAME, SQL_SUBSCRIBER.|  
|**Valor**|**nvarchar(512)**|Valor do tipo de informação associado.|  
  
## <a name="remarks"></a>Comentários  
 **sp_dsninfo** é usado em todos os tipos de replicação.  
  
 **sp_dsninfo** recupera informações de fonte de dados do ODBC ou do OLE DB que mostram se o Database pode ser usado para replicação ou consulta.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_dsninfo**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_enumdsn](../../relational-databases/system-stored-procedures/sp-enumdsn-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
