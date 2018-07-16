---
title: Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes para pesquisa de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
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
caps.latest.revision: 79
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c3ea419224478d1c4c45117795fe5a67ebfcaf5e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37284832"
---
# <a name="configure-and-manage-stopwords-and-stoplists-for-full-text-search"></a>Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes (stoplists) para pesquisa de texto completo
  Para evitar que os índices de texto completo fiquem lotados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispõe de um mecanismo que descarta cadeias de caracteres que ocorrem com frequência e que não auxiliam nas pesquisas. Essas cadeias de caracteres descartadas são chamadas de *palavras irrelevantes*(stopwords). Durante a criação do índice, o Mecanismo de Texto Completo omite as palavras irrelevantes do índice de texto completo. Em outras palavras, as consultas de texto completo não pesquisarão palavras irrelevantes.  
  
##  <a name="understand"></a> Listas de palavras irrelevantes e palavras irrelevantes de Noções básicas sobre  
 Uma palavra irrelevante pode ser uma palavra com significado em um determinado idioma ou um *token* sem significado linguístico. Por exemplo, em inglês, palavras como "a", "and", "is" e "the" não são incluídas no índice de texto completo porque são consideradas inúteis em uma pesquisa.  
  
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
  
 As palavras irrelevantes são gerenciadas nos bancos de dados por meio de objetos denominados listas de palavras irrelevantes (stoplists). Uma *lista de palavras irrelevantes (stoplist)* é uma lista que, quando associada a um índice de texto completo, é aplicada às consultas de texto completo desse índice.  
  
  
##  <a name="creating"></a> Criando uma lista de palavras irrelevantes  
 Você pode criar uma lista de palavras irrelevantes (stoplist) de qualquer uma destas formas:  
  
-   Usando a lista de palavras irrelevantes (stoplist) fornecida pelo sistema no banco de dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é fornecido com uma lista de palavras irrelevantes do sistema que contém as palavras irrelevantes mais usadas em cada idioma com suporte, ou seja, em cada idioma associado a determinados separadores de palavra por padrão. A lista de palavras irrelevantes do sistema contém palavras irrelevantes comuns para todos os idiomas com suporte.  Você pode copiar essa lista e personalizar sua cópia adicionando e removendo palavras irrelevantes.  
  
     A lista de palavras irrelevantes do sistema é instalada no banco de dados [Resource](../databases/resource-database.md) .  
  
-   Criando sua própria lista de palavras irrelevantes e depois adicionando palavras irrelevantes a ela para qualquer idioma especificado. Você também pode descartar palavras irrelevantes da lista sempre que necessário.  
  
-   Usando uma lista de palavras irrelevantes personalizada existente de outro banco de dados na instância de servidor atual e, em seguida, adicionando ou descartando palavras irrelevantes conforme necessário.  
  
 **Para criar uma lista de palavras irrelevantes**  
  
-   [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)  
  
#### <a name="to-create-a-full-text-stoplist-in-management-studio"></a>Para criar uma lista de palavras irrelevantes (stoplist) de texto completo no Management Studio  
  
1.  No Pesquisador de Objetos, expanda o servidor.  
  
2.  Expanda **Bancos de Dados**e o banco de dados no qual você deseja criar a lista de palavras irrelevantes (stoplist) de texto completo.  
  
3.  Expanda **Armazenamento**e clique com o botão direito do mouse em **Lista de Palavras Irrelevantes de Texto Completo**.  
  
4.  Selecione **Nova lista de palavras irrelevantes de texto completo**.  
  
5.  Especifique o nome da lista de palavras irrelevantes.  
  
6.  Opcionalmente, especifique outra pessoa como o proprietário da lista de palavras irrelevantes.  
  
7.  Selecione uma das seguintes opções de criação de lista de palavras irrelevantes:  
  
    -   **Criar uma lista de palavras irrelevantes vazia**  
  
    -   **Criar com base na lista de palavras irrelevantes do sistema**  
  
    -   **Criar com base em uma lista de palavras irrelevantes existente**  
  
     Para obter mais informações, veja [Nova lista de palavras irrelevantes de texto completo &#40;Página Geral&#41;](../../integration-services/general-page-of-integration-services-designers-options.md).  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 **Para remover uma lista de palavras irrelevantes**  
  
-   [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-stoplist-transact-sql)  
  
  
##  <a name="queries"></a> Usando uma lista de palavras irrelevantes em consultas de texto completo  
 Para usar uma lista de palavras irrelevantes (stoplist) em consultas, é preciso associá-la a um índice de texto completo. Você pode anexar uma lista de palavras irrelevantes a um índice de texto completo ao criá-lo ou pode alterá-lo posteriormente para adicionar uma lista de palavras irrelevantes.  
  
 **Para criar um índice de texto completo e associar uma lista de palavras irrelevantes ele**  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
 **Para associar ou desassociar uma lista de palavras irrelevantes com um índice de texto completo existente**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)  
  
 **Para suprimir uma mensagem de erro se palavras irrelevantes causarem uma operação booliana em uma consulta de texto completo falha**  
  
-   [Opção de configuração do servidor transform noise words](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)  
  
  
##  <a name="viewing"></a> Exibindo metadados de lista de palavras irrelevantes e listas de palavras irrelevantes  
 **Para exibir todas as palavras irrelevantes de uma lista de palavras irrelevantes**  
  
-   [sys.fulltext_stopwords &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql)  
  
 **Para obter informações sobre todas as listas de palavras irrelevantes no banco de dados atual**  
  
-   [sys.fulltext_stoplists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql)  
  
-   [sys.fulltext_stopwords &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql)  
  
 **Para exibir o resultado da geração de tokens de uma combinação de separador, dicionário de sinônimos e lista de palavras irrelevantes do word**  
  
-   [sys.dm_fts_parser &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql)  
  
  
##  <a name="change"></a> Alterando as palavras irrelevantes em uma lista de palavras irrelevantes  
 **Para adicionar ou remover palavras irrelevantes em uma lista de palavras irrelevantes**  
  
-   [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)  
  
#### <a name="to-change-the-stopwords-in-a-stoplist-in-management-studio"></a>Para alterar as palavras irrelevantes em uma lista de palavras irrelevantes (stoplist) no Management Studio  
  
1.  No Pesquisador de Objetos, expanda o servidor.  
  
2.  Expanda **Bancos de Dados**e, em seguida, expanda o banco de dados.  
  
3.  Expanda **Armazenamento**e, depois, selecione **Listas de Palavras Irrelevantes de Texto Completo**.  
  
4.  Clique com o botão direito do mouse na lista de palavras irrelevantes cujas propriedades você deseja alterar e selecione **Propriedades**.  
  
5.  Na caixa de diálogo [Propriedades da lista de palavras irrelevantes de texto completo](../../database-engine/full-text-stoplist-properties.md) :  
  
    1.  Na caixa de listagem **Ação** , selecione uma das seguintes ações: **Adicionar palavra irrelevante**, **Excluir palavra irrelevante**, **Excluir todas as palavras irrelevantes**ou **Limpar lista de palavras irrelevantes**.  
  
    2.  Se a caixa de texto **Palavra irrelevante** estiver habilitada para a ação selecionada, insira uma única palavra irrelevante. Essa palavra irrelevante deve ser exclusiva; ou seja, ainda não deve estar na lista de palavras irrelevantes para o idioma selecionado.  
  
    3.  Se a caixa de listagem **Idioma de texto completo** estiver habilitada para a ação selecionada, selecione um idioma.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
##  <a name="upgrade"></a> Atualizando palavras de ruído do SQL Server 2005  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] foram substituídas por palavras irrelevantes. Quando um banco de dados é atualizado no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], os arquivos de palavras de ruído não são mais usados. No entanto, os arquivos de palavras de ruído são armazenados na pasta FTDATA\ FTNoiseThesaurusBak e você pode usá-los ao atualizar ou compilar as listas de palavras irrelevantes (stoplists) correspondentes. Para obter informações sobre como atualizar arquivos de palavras de ruído para listas de palavras irrelevantes, consulte [Atualizar pesquisa de texto completo](upgrade-full-text-search.md).  
  
  
  
