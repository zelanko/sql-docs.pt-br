---
title: "ALTERAR o catálogo de texto completo (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_FULLEXT_CATALOG_TSQL
- ALTER FULLEXT CATALOG
dev_langs:
- TSQL
helpviewer_keywords:
- modifying full-text catalogs
- full-text catalogs [SQL Server], rebuilding
- accent sensitivity
- ALTER FULLTEXT CATALOG statement
- full-text catalogs [SQL Server], modifying
- full-text catalogs [SQL Server], reorganizing
ms.assetid: 31a47aaf-6c7f-48a4-a86a-d57aec66c9cb
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bd07ffa9da60ccbf38265d46a6415fe461d492f8
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-fulltext-catalog-transact-sql"></a>ALTER FULLTEXT CATALOG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Altera as propriedades de um catálogo de texto completo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER FULLTEXT CATALOG catalog_name   
{ REBUILD [ WITH ACCENT_SENSITIVITY = { ON | OFF } ]  
| REORGANIZE  
| AS DEFAULT   
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *catalog_name*  
 Especifica o nome do catálogo a ser modificado. Se um catálogo com o nome especificado não existir, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará um erro e não executa a operação de alteração.  
  
 REBUILD  
 Instrui o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a reconstruir o catálogo inteiro. Quando um catálogo é recriado, o catálogo existente é excluído e um novo catálogo é criado em seu lugar. Todas as tabelas que têm referências de indexação de texto completo são associadas ao novo catálogo. A recriação redefine os metadados de texto completo nas tabelas do sistema de banco de dados.  
  
 WITH ACCENT_SENSITIVITY = {ON|OFF}  
 Especifica se o catálogo a ser alterado diferencia acentuação ou não para indexação e consulta de texto completo.  
  
 Para determinar a configuração atual da propriedade sensibilidade de acentuação de um catálogo de texto completo, use a função FULLTEXTCATALOGPROPERTY com o **accentsensitivity** valor da propriedade contra *catalog_name*. Se a função retornar '1', o catálogo de texto completo diferencia acentuação; se a função retornar '0', o catálogo não diferencia acentuação.  
  
 O padrão de diferenciação de acentuação do catálogo e do banco de dados é o mesmo.  
  
 REORGANIZE  
 Informa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar um *a mesclagem mestra*, que envolve a mesclagem dos índices menores criados no processo de indexação em um índice grande. Mesclar os fragmentos de índice de texto completo pode melhorar o desempenho e liberar recursos de disco e memória. Se houver alterações frequentes no catálogo de texto completo, use este comando periodicamente para reorganizar o catálogo de texto completo.  
  
 REORGANIZE também otimiza o índice interno e as estruturas do catálogo.  
  
 Lembre-se de que, dependendo da quantidade de dados indexados, uma mesclagem mestra pode demorar algum tempo para ser concluída. A mesclagem mestra de grande quantidade de dados pode criar uma transação demorada, atrasando o truncamento do log de transações durante o ponto de verificação. Nesse caso, o log de transações pode crescer significativamente sob o modelo de recuperação completa. Como prática recomendada, verifique se o log de transações contém espaço suficiente para uma transação demorada antes de reorganizar um índice de texto completo grande em um banco de dados que usa o modelo de recuperação completa. Para obter mais informações, veja [Gerenciar o tamanho do arquivo de log de transações](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md).  
  
 AS DEFAULT  
 Especifica que este catálogo é o padrão. Quando forem criados índices de texto completo sem nenhum catálogo especificado, o catálogo padrão será usado. Se houver um catálogo de texto completo padrão, a configuração de AS DEFAULT para este catálogo substituirá o padrão existente.  
  
## <a name="permissions"></a>Permissões  
 Usuário deve ter a permissão ALTER no catálogo de texto completo ou ser um membro do **db_owner**, **db_ddladmin** fixa funções de banco de dados ou função de servidor fixa sysadmin.  
  
> [!NOTE]  
>  Para usar ALTER FULLTEXT CATALOG AS DEFAULT, o usuário deve ter permissão ALTER no catálogo de texto completo e permissão CREATE FULLTEXT CATALOG no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera a propriedade `accentsensitivity` do catálogo de texto completo padrão `ftCatalog` que diferencia acentos.  
  
```  
--Change to accent insensitive  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT CATALOG ftCatalog   
REBUILD WITH ACCENT_SENSITIVITY=OFF;  
GO  
-- Check Accentsensitivity  
SELECT FULLTEXTCATALOGPROPERTY('ftCatalog', 'accentsensitivity');  
GO  
--Returned 0, which means the catalog is not accent sensitive.  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys. fulltext_catalogs &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [CRIAR o catálogo de texto completo &#40; Transact-SQL &#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [REMOVER o catálogo de texto completo &#40; Transact-SQL &#41;](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)   
 [Pesquisa de Texto Completo](../../relational-databases/search/full-text-search.md)  
  
  
