---
title: sp_server_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_server_info
- sp_server_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_server_info
ms.assetid: 2dc2c262-3cfa-4a84-8127-3632ba583543
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6aae34fb03322a40f1b970df6271bb89d18b3293
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104452"
---
# <a name="spserverinfo-transact-sql"></a>sp_server_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma lista de nomes de atributo e valores correspondentes para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o gateway do banco de dados ou a fonte de dados subjacente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_server_info [[@attribute_id = ] 'attribute_id']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @attribute_id = ] 'attribute_id'` É a ID de inteiro do atributo. *attribute_id* está **int**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**ATTRIBUTE_ID**|**int**|Número do ID do atributo.|  
|**ATTRIBUTE_NAME**|**varchar(** 60 **)**|Nome do atributo.|  
|**ATTRIBUTE_VALUE**|**varchar(** 255 **)**|Configuração atual do atributo.|  
  
 A tabela a seguir lista os atributos. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Bibliotecas de cliente do ODBC atualmente usam atributos **1**, **2**, **18**, **22**, e **500** na conexão tempo.  
  
|ATTRIBUTE_ID|ATTRIBUTE_NAME Descrição|ATTRIBUTE_VALUE|  
|-------------------|---------------------------------|----------------------|  
|**1**|DBMS_NAME|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**2**|DBMS_VER|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] - *x.xx.xxxx*|  
|**10**|OWNER_TERM|owner|  
|**11**|TABLE_TERM|table|  
|**12**|MAX_OWNER_NAME_LENGTH|128|  
|**13**|TABLE_LENGTH<br /><br /> Especifica o número máximo de caracteres para um nome de tabela.|128|  
|**14**|MAX_QUAL_LENGTH<br /><br /> Especifica o comprimento máximo do nome de um qualificador de tabela (a primeira parte de um nome de tabela com três partes).|128|  
|**15**|COLUMN_LENGTH<br /><br /> Especifica o número máximo de caracteres para um nome de coluna.|128|  
|**16**|IDENTIFIER_CASE<br /><br /> Especifica os nomes definidos pelo usuário (nomes de tabelas, nomes de colunas, nomes de procedimentos armazenados) no banco de dados (maiúsculas/minúsculas dos objetos nos catálogos do sistema).|SENSITIVE|  
|**17**|TX_ISOLATION<br /><br /> Especifica o nível de isolamento inicial da transação que o servidor assume, o qual corresponde a um nível de isolamento definido em SQL-92.|2|  
|**18**|COLLATION_SEQ<br /><br /> Especifica a ordenação do conjunto de caracteres para este servidor.|charset=iso_1 sort_order=dictionary_iso charset_num=1 sort_order_num=51|  
|**19**|SAVEPOINT_SUPPORT<br /><br /> Especifica se o DBMS subjacente oferece suporte a pontos de salvamento nomeados.|S|  
|**20**|MULTI_RESULT_SETS<br /><br /> Especifica se o banco de dados subjacente ou o próprio gateway oferece suporte a vários conjuntos de resultados (várias instruções podem ser enviadas pelo gateway com vários conjuntos de resultados retornados ao cliente).|S|  
|**22**|ACCESSIBLE_TABLES<br /><br /> Especifica se deve em **sp_tables**, o gateway retorna somente tabelas, exibições e assim por diante, acessíveis pelo usuário atual (ou seja, o usuário que tem pelo menos permissões SELECT para a tabela).|S|  
|**100**|USERID_LENGTH<br /><br /> Especifica o número máximo de caracteres para um nome de usuário.|128|  
|**101**|QUALIFIER_TERM<br /><br /> Especifica o termo do fornecedor do DBMS de um qualificador de tabela (a primeira parte de um nome de tabela com três partes).|database|  
|**102**|NAMED_TRANSACTIONS<br /><br /> Especifica se o DBMS subjacente oferece suporte a transações nomeadas.|S|  
|**103**|SPROC_AS_LANGUAGE<br /><br /> Especifica se os procedimentos armazenados podem ser executados como eventos de linguagem.|S|  
|**104**|ACCESSIBLE_SPROC<br /><br /> Especifica se deve em **sp_stored_procedures**, o gateway retorna somente os procedimentos armazenados que são executáveis pelo usuário atual.|S|  
|**105**|MAX_INDEX_COLS<br /><br /> Especifica o número máximo de colunas em um índice para o DBMS.|16|  
|**106**|RENAME_TABLE<br /><br /> Especifica se as tabelas podem ser renomeadas.|S|  
|**107**|RENAME_COLUMN<br /><br /> Especifica se as colunas podem ser renomeadas.|S|  
|**108**|DROP_COLUMN<br /><br /> Especifica se as colunas podem ser descartadas.|S|  
|**109**|INCREASE_COLUMN_LENGTH<br /><br /> Especifica se o tamanho da coluna pode ser aumentado.|S|  
|**110**|DDL_IN_TRANSACTION<br /><br /> Especifica se instruções DDL podem aparecer em transações.|S|  
|**111**|DESCENDING_INDEXES<br /><br /> Especifica se há suporte para índices decrescentes.|S|  
|**112**|SP_RENAME<br /><br /> Especifica se um procedimento armazenado pode ser renomeado.|S|  
|**113**|REMOTE_SPROC<br /><br /> Especifica se os procedimentos armazenados podem ser executados pelas funções remotas de procedimento armazenado em DB-Library.|S|  
|**500**|SYS_SPROC_VERSION<br /><br /> Especifica a versão dos procedimentos armazenados do catálogo atualmente implementados.|Número da versão atual|  
  
## <a name="remarks"></a>Comentários  
 **sp_server_info** retorna um subconjunto das informações fornecidas por **SQLGetInfo** no ODBC.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
