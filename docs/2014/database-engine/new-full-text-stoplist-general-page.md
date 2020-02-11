---
title: NovaList de palavras irrelevantes de texto completo (página Geral) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftstoplist.general.f1
ms.assetid: 97f8e82d-82ab-4525-91c9-1ee3ae217309
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: eca5e82b9d23709b45949cfe6af9022f1243ef08
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62774208"
---
# <a name="new-full-text-stoplist-general-page"></a>Nova Lista de Palavras Irrelevantes de Texto Completo (página Geral)
  Use esta caixa de diálogo para criar uma lista de palavras irrelevantes (stoplist) de texto completo. Uma *lista de palavras irrelevantes* é um conjunto de palavras usadas com frequência, chamadas *palavras irrelevantes*, que são omitidas da indexação de texto completo de tabelas que usam a lista de palavras irrelevantes. Para obter mais informações, veja [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes para pesquisa de texto completo](../relational-databases/search/full-text-search.md).  
  
 **Para usar o SQL Server Management Studio para criar uma lista de palavras irrelevantes**  
  
-   [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes para pesquisa de texto completo](../relational-databases/search/full-text-search.md)  
  
## <a name="options"></a>Opções  
 **Nome da lista de palavras irrelevantes de texto completo**  
 Digite o nome da lista de palavras irrelevantes de texto completo.  
  
 **Proprietário**  
 Especifique o proprietário da lista de palavras irrelevantes de texto completo. Para atribuir a propriedade a você, ou seja, para o usuário atual, deixe esse campo em branco.  
  
 Para especificar um usuário diferente, clique no botão Procurar.  
  
### <a name="create-stoplist-options"></a>Opções para criar listas de palavras irrelevantes  
 Clique em uma destas opções de criação:  
  
 **Criar uma lista de palavras irrelevantes vazia**  
 A nova lista de palavras irrelevantes não conterá nenhuma palavra irrelevante.  
  
 **Criar com base na lista de palavras irrelevantes do sistema**  
 A nova lista de palavras irrelevantes será criada a partir da lista de palavras irrelevantes existente por padrão no [Banco de dados de recursos](../relational-databases/databases/resource-database.md).  
  
 **Criar com base em uma lista de palavras irrelevantes existente**  
 A nova lista de palavras irrelevantes será criada a partir da cópia de uma lista de palavras irrelevantes existente.  
  
 **Banco de dados de origem**  
 Especifica o nome do banco de dados ao qual a lista de palavras irrelevantes existente pertence. Por padrão, o banco de dados atual é selecionado. Você tem a opção de selecionar um outro banco de dados na caixa de listagem.  
  
 **Lista de palavras irrelevantes de origem**  
 Especifica o nome de um lista de palavras irrelevantes existente. Na relação de listas de palavras irrelevantes disponíveis, selecione uma para usar como origem. As listas de palavras irrelevantes disponíveis são relacionadas na ordem em aparecem no Pesquisador de Objetos.  
  
 Se qualquer idioma especificado nas palavras irrelevantes da lista de palavras irrelevantes de origem não estiver registrado no banco de dados atual, CREATE FULLTEXT STOPLIST terá êxito, mas serão retornados avisos e as palavras irrelevantes correspondentes não serão adicionadas.  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)   
 [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)   
 [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-stoplist-transact-sql)   
 [Configurar e gerenciar palavras irrelevantes (stop words) e listas de palavras irrelevantes (stoplists) para a pesquisa de texto completo](../relational-databases/search/full-text-search.md)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql)  
  
  
