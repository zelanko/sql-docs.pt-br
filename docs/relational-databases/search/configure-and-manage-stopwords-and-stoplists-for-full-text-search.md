---
title: Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes para pesquisa de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.component: search
ms.reviewer: ''
ms.suite: sql
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- full-text search [SQL Server], noise words
- noise words [full-text search]
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 43b5ce7b-9f09-4443-8a5b-c3da6eb28bcc
caps.latest.revision: 81
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 64d4572f3b2612bb4b10210adbe8f8edb301572c
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39553276"
---
# <a name="configure-and-manage-stopwords-and-stoplists-for-full-text-search"></a>Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes (stoplists) para pesquisa de texto completo
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Para evitar que os índices de texto completo fiquem lotados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispõe de um mecanismo que descarta cadeias de caracteres que ocorrem com frequência e que não auxiliam nas pesquisas. Essas cadeias de caracteres descartadas são chamadas de *palavras irrelevantes*(stopwords). Durante a criação do índice, o Mecanismo de Texto Completo omite as palavras irrelevantes do índice de texto completo. Em outras palavras, as consultas de texto completo não pesquisarão palavras irrelevantes.  
   
**Palavras irrelevantes**. Uma palavra irrelevante pode ser uma palavra com significado em um idioma específico. Por exemplo, em inglês, palavras como "a", "and", "is" e "the" não são incluídas no índice de texto completo porque são consideradas inúteis em uma pesquisa. Uma palavra irrelevante também pode ser um *token* que não tem significado linguístico.  

**Listas de palavras irrelevantes**. As palavras irrelevantes são gerenciadas nos bancos de dados por meio de objetos denominados listas de palavras irrelevantes (stoplists). Uma *lista de palavras irrelevantes (stoplist)* é uma lista que, quando associada a um índice de texto completo, é aplicada às consultas de texto completo desse índice.
   
## <a name="use-an-existing-stoplist"></a>Usar uma lista de palavras irrelevantes existente  
 É possível usar uma lista de palavras irrelevantes existente das seguintes maneiras:  
  
-   Use a lista de palavras irrelevantes fornecida pelo sistema no banco de dados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é fornecido com uma lista de palavras irrelevantes do sistema que contém as palavras irrelevantes mais comumente usadas em cada idioma com suporte, ou seja, em cada idioma associado a determinados separadores de palavra por padrão. É possível copiar a lista de palavras irrelevantes do sistema e personalizar sua cópia adicionando e removendo palavras irrelevantes.  
  
     A lista de palavras irrelevantes do sistema é instalada no banco de dados [Resource](../../relational-databases/databases/resource-database.md) .  
  
-   Use uma lista de palavras irrelevantes personalizada existente de outro banco de dados na instância de servidor atual. Em seguida, adicione ou remova palavras irrelevantes conforme necessário.  
  
## <a name="create-a-new-stoplist"></a>Criar uma nova lista de palavras irrelevantes 
### <a name="create-a-new-stoplist-with-transact-sql"></a>Criar uma nova lista de palavras irrelevantes com Transact-SQL
Use [CREATE FULLTEXT STOPLIST](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md).

### <a name="create-a-new-stoplist-with-management-studio"></a>Criar uma nova lista de palavras irrelevantes com o Management Studio
  
1.  No Pesquisador de Objetos, expanda o servidor.  
  
2.  Expanda **Bancos de Dados**e o banco de dados no qual você deseja criar a lista de palavras irrelevantes (stoplist) de texto completo.  
  
3.  Expanda **Armazenamento**e clique com o botão direito do mouse em **Lista de Palavras Irrelevantes de Texto Completo**.  
  
4.  Selecione **Nova lista de palavras irrelevantes de texto completo**.  
  
5.  Insira o nome da sua nova lista de palavras irrelevantes.  
  
6.  Opcionalmente, especifique outra pessoa como o proprietário da lista de palavras irrelevantes.  
  
7.  Selecione uma das seguintes opções de criação de lista de palavras irrelevantes:  
  
    -   **Criar uma lista de palavras irrelevantes vazia**  
  
    -   **Criar com base na lista de palavras irrelevantes do sistema**  
  
    -   **Criar com base em uma lista de palavras irrelevantes existente**  
  
     Para obter mais informações, veja [Nova lista de palavras irrelevantes de texto completo &#40;Página Geral&#41;](http://msdn.microsoft.com/library/97f8e82d-82ab-4525-91c9-1ee3ae217309).  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="use-a-stoplist-in-full-text-queries"></a>Usar uma lista de palavras irrelevantes em consultas de texto completo  
 Para usar uma lista de palavras irrelevantes em consultas, é necessário associá-la a um índice de texto completo. Você pode anexar uma lista de palavras irrelevantes a um índice de texto completo ao criá-lo ou pode alterá-lo posteriormente para adicionar uma lista de palavras irrelevantes.  
  
### <a name="create-a-full-text-index-and-associate-a-stoplist-with-it"></a>Criar um índice de texto completo e associar uma lista de palavras irrelevantes a ele
Use [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md).
  
### <a name="associate-or-disassociate-a-stoplist-with-an-existing-full-text-index"></a>Associar uma lista de palavras irrelevantes a um índice de texto completo ou desassociá-la dele
Use [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md). 
  
## <a name="change-the-stopwords-in-a-stoplist"></a>Alterar as palavras irrelevantes em uma lista de palavras irrelevantes  
### <a name="add-or-drop-stopwords-from-a-stoplist-with-transact-sql"></a>Adicionar palavras irrelevantes a uma lista de palavras irrelevantes com Transact-SQL ou removê-las dela
Use [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md).
  
### <a name="add-or-drop-stopwords-from-a-stoplist-with-management-studio"></a>Adicionar palavras irrelevantes a uma lista de palavras irrelevantes com o Management Studio ou removê-las dela  
  
1.  No Pesquisador de Objetos, expanda o servidor.  
  
2.  Expanda **Bancos de Dados**e, em seguida, expanda o banco de dados.  
  
3.  Expanda **Armazenamento**e, depois, selecione **Listas de Palavras Irrelevantes de Texto Completo**.  
  
4.  Clique com o botão direito do mouse na lista de palavras irrelevantes cujas propriedades você deseja alterar e selecione **Propriedades**.  
  
5.  Na caixa de diálogo [Propriedades da lista de palavras irrelevantes de texto completo](http://msdn.microsoft.com/library/2e907f5b-0cf9-484a-afcf-a4e7f1e2f87f) :  
  
    1.  Na caixa de listagem **Ação** , selecione uma das seguintes ações: **Adicionar palavra irrelevante**, **Excluir palavra irrelevante**, **Excluir todas as palavras irrelevantes**ou **Limpar lista de palavras irrelevantes**.  
  
    2.  Se a caixa de texto **Palavra irrelevante** estiver habilitada para a ação selecionada, insira uma única palavra irrelevante. Essa palavra irrelevante deve ser exclusiva; ou seja, ainda não deve estar na lista de palavras irrelevantes para o idioma selecionado.  
  
    3.  Se a caixa de listagem **Idioma de texto completo** estiver habilitada para a ação selecionada, selecione um idioma.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="manage-stoplists-and-their-usage"></a>Gerenciar listas de palavras irrelevantes e seu uso
  
### <a name="view-all-the-stopwords-in-a-stoplist"></a>Exibir todas as palavras irrelevantes em uma lista de palavras irrelevantes
Use [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md). 
  
### <a name="get-info-about-all-the-stoplists-in-the-current-database"></a>Obter informações sobre todas as listas de palavras irrelevantes no banco de dados atual
Use [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md) e [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md).
  
### <a name="view-the-tokenization-result-of-a-word-breaker-thesaurus-and-stoplist-combination"></a>Exibir o resultado da geração de tokens de um separador de palavras, dicionário de sinônimos e combinação de lista de palavras irrelevantes
Use [sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md).

### <a name="suppress-an-error-message-if-stopwords-cause-a-boolean-operation-on-a-full-text-query-to-fail"></a>Suprimir uma mensagem de erro se as palavras irrelevantes causarem falha em uma operação booliana em uma consulta de texto completo
Use a [Opção de configuração de servidor para transformar palavras de ruído](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md). 
   
## <a name="more-info-about-stopword-position"></a>Mais informações sobre a posição de palavras irrelevantes
 Embora as palavras irrelevantes sejam ignoradas, o índice de texto completo leva em conta sua posição. Por exemplo, considere a frase "Instructions are applicable to these Adventure Works Cycles models". A tabela a seguir descreve a posição das palavras na frase:  
  
|Word|Posição|  
|----------|--------------|  
|Instruções|1|  
|are|2|  
|applicable|3|  
|para|4|  
|these|5|  
|Adventure|6|  
|Works|7|  
|Cycles|8|  
|modelos|9|  
  
 As palavras irrelevantes "are", "to" e "these", que estão nas posições 2, 4 e 5, são excluídas do índice de texto completo. Contudo, sua informação posicional é mantida, sem afetar a posição das outras palavras da frase.   
  
## <a name="upgrade-noise-words-from-sql-server-2005"></a>Atualizar palavras de ruído no SQL Server 2005  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] foram substituídas por palavras irrelevantes. Quando um banco de dados é atualizado no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], os arquivos de palavras de ruído não são mais usados. No entanto, os arquivos de palavras de ruído são armazenados na pasta FTDATA\ FTNoiseThesaurusBak e você pode usá-los ao atualizar ou compilar as listas de palavras irrelevantes (stoplists) correspondentes. Para obter informações sobre como atualizar arquivos de palavras de ruído para listas de palavras irrelevantes, consulte [Atualizar pesquisa de texto completo](../../relational-databases/search/upgrade-full-text-search.md).  
  
  
  
