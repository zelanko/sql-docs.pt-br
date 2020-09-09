---
description: sp_fulltext_semantic_register_language_statistics_db (Transact-SQL)
title: sp_fulltext_semantic_register_language_statistics_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_semantic_register_language_statistics_db
- sp_fulltext_semantic_register_language_statistics_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_semantic_register_language_statistics_db
ms.assetid: bef1b104-5a44-4327-9ae4-45eae3000f7e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: deb1973dcff95f79d70ca3f458c38208db3b1f47
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548019"
---
# <a name="sp_fulltext_semantic_register_language_statistics_db-transact-sql"></a>sp_fulltext_semantic_register_language_statistics_db (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Registra um banco de dados de Estatísticas Semânticas de Idioma previamente preenchido na instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 É possível iniciar a extração semântica apenas depois de anexar este banco de dados de estatísticas de idioma e de registrá-lo com este procedimento armazenado. É necessário executar essa tarefa apenas uma vez para cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
EXEC sp_fulltext_semantic_register_language_statistics_db  
    [ @dbname = ] 'database_name';  
GO  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> Argumentos  
 [ @dbname =] '*database_name*'  
 É o nome do banco de dados de Estatísticas de Idioma Semântico a ser registrado para a instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O banco de dados já deve estar anexado. *database_name* é **sysname**e não pode ser nulo.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-set"></a>Conjunto de resultados  
 Nenhum.  
  
## <a name="general-remarks"></a>Comentários gerais  
 O banco de dados de Estatísticas de Idioma Semântico contém estatísticas relacionadas a idioma que são necessárias para processamento semântico de conteúdo textual.  
  
 **sp_fulltext_semantic_register_language_statistics_db** executa as seguintes etapas:  
  
1.  Verifica se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é uma versão que dá suporte ao processamento semântico.  
  
2.  Verifica se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] já não tem um banco de dados de Estatísticas de Idioma Semântico definido.  
  
3.  Verifica se o banco de dados é um banco de dados de Estatísticas de Idioma Semântico válido.  
  
4.  Define as permissões no banco de dados de Estatísticas de Idioma Semântico para restringir o acesso ao banco de dados pelos usuários.  
  
5.  Insere os metadados que definem o nome do banco de dados de Estatísticas de Idioma Semântico para a instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
6.  Insere os metadados que definem os mapeamentos entre o banco de dados de Estatísticas de Idioma Semântico instalado e as tabelas do Modelo do Idioma.  
  
7.  Verifica se o banco de dados está pronto para uso.  
  
 Para obter mais informações, veja [Instalar e configurar a pesquisa semântica](../../relational-databases/search/install-and-configure-semantic-search.md).  
  
## <a name="metadata"></a>Metadados  
 Para obter informações sobre o Estatísticas Semânticas de Idioma banco de dados instalado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte a exibição de catálogo [sys. fulltext_semantic_language_statistics_database &#40;&#41;do TRANSACT-SQL ](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md).  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer as permissões CONTROL SERVER.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como registrar o Estatísticas Semânticas de Idioma banco de dados chamando **sp_fulltext_semantic_register_language_statistics_db**.  
  
```sql  
EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = 'semanticsDb';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar e configurar a pesquisa semântica](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
