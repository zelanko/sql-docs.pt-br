---
title: "Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes (stoplists) para pesquisa de texto completo | Microsoft Docs"
ms.custom: ""
ms.date: "02/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "listas de palavras irrelevantes (stoplists) [pesquisa de texto completo]"
  - "pesquisa de texto completo [SQL Server], lista de palavras irrelevantes"
  - "pesquisa de texto completo [SQL Server], palavra de ruído"
  - "palavras de ruído [pesquisa de texto completo]"
  - "pesquisa de texto completo [SQL Server], palavras irrelevantes"
  - "palavras irrelevantes (stopwords) [pesquisa de texto completo]"
ms.assetid: 43b5ce7b-9f09-4443-8a5b-c3da6eb28bcc
caps.latest.revision: 81
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 79
---
# Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes (stoplists) para pesquisa de texto completo
  Para evitar que os índices de texto completo fiquem lotados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispõe de um mecanismo que descarta cadeias de caracteres que ocorrem com frequência e que não auxiliam nas pesquisas. Essas cadeias de caracteres descartadas são chamadas de *palavras irrelevantes*(stopwords). Durante a criação do índice, o Mecanismo de Texto Completo omite as palavras irrelevantes do índice de texto completo. Em outras palavras, as consultas de texto completo não pesquisarão palavras irrelevantes.  
  
##  <a name="understand"></a> Noções básicas sobre palavras irrelevantes e listas de palavras irrelevantes (stoplists)  
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
  
 [Neste tópico](#TOP)  
  
##  <a name="creating"></a> Criando uma lista de palavras irrelevantes (stoplist)  
 Você pode criar uma lista de palavras irrelevantes (stoplist) de qualquer uma destas formas:  
  
-   Usando a lista de palavras irrelevantes (stoplist) fornecida pelo sistema no banco de dados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é fornecido com uma lista de palavras irrelevantes do sistema que contém as palavras irrelevantes mais usadas em cada idioma com suporte, ou seja, em cada idioma associado a determinados separadores de palavra por padrão. A lista de palavras irrelevantes do sistema contém palavras irrelevantes comuns para todos os idiomas com suporte.  Você pode copiar essa lista e personalizar sua cópia adicionando e removendo palavras irrelevantes.  
  
     A lista de palavras irrelevantes do sistema é instalada no banco de dados [Resource](../../relational-databases/databases/resource-database.md) .  
  
-   Criando sua própria lista de palavras irrelevantes e depois adicionando palavras irrelevantes a ela para qualquer idioma especificado. Você também pode descartar palavras irrelevantes da lista sempre que necessário.  
  
-   Usando uma lista de palavras irrelevantes personalizada existente de outro banco de dados na instância de servidor atual e, em seguida, adicionando ou descartando palavras irrelevantes conforme necessário.  
  
 **Par criar uma lista de palavras irrelevantes (stoplist)**  
  
-   [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)  
  
#### Para criar uma lista de palavras irrelevantes (stoplist) de texto completo no Management Studio  
  
1.  No Pesquisador de Objetos, expanda o servidor.  
  
2.  Expanda **Bancos de Dados** e o banco de dados no qual você deseja criar a lista de palavras irrelevantes (stoplist) de texto completo.  
  
3.  Expanda **Armazenamento** e clique com o botão direito do mouse em **Lista de Palavras Irrelevantes de Texto Completo**.  
  
4.  Selecione **Nova lista de palavras irrelevantes de texto completo**.  
  
5.  Especifique o nome da lista de palavras irrelevantes.  
  
6.  Opcionalmente, especifique outra pessoa como o proprietário da lista de palavras irrelevantes.  
  
7.  Selecione uma das seguintes opções de criação de lista de palavras irrelevantes:  
  
    -   **Criar uma lista de palavras irrelevantes vazia**  
  
    -   **Criar com base na lista de palavras irrelevantes do sistema**  
  
    -   **Criar com base em uma lista de palavras irrelevantes existente**  
  
     Para obter mais informações, veja [Nova lista de palavras irrelevantes de texto completo &#40;Página Geral&#41;](../Topic/New%20Full-Text%20Stoplist%20\(General%20Page\).md).  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 **Para remover uma lista de palavras irrelevantes (stoplist)**  
  
-   [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)  
  
 [Neste tópico](#TOP)  
  
##  <a name="queries"></a> Usando uma lista de palavras irrelevantes (stoplist) em consultas de texto completo  
 Para usar uma lista de palavras irrelevantes (stoplist) em consultas, é preciso associá-la a um índice de texto completo. Você pode anexar uma lista de palavras irrelevantes a um índice de texto completo ao criá-lo ou pode alterá-lo posteriormente para adicionar uma lista de palavras irrelevantes.  
  
 **Para criar um índice de texto completo e associar uma lista de palavras irrelevantes a ele**  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)  
  
 **Para associar uma lista de palavras irrelevantes a um índice de texto completo ou desassociá-la dele**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
 **Para suprimir uma mensagem de erro se palavras irrelevantes causarem falha em uma operação booliana em uma consulta de texto completo**  
  
-   [Opção de configuração de servidor para transformar palavras de ruído](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)  
  
 [Neste tópico](#TOP)  
  
##  <a name="viewing"></a> Exibindo listas de palavras irrelevantes (stoplists) e metadados de lista de palavras irrelevantes  
 **Para exibir todas as palavras irrelevantes de uma lista de palavras irrelevantes (stoplist)**  
  
-   [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)  
  
 **Para obter informações sobre todas as listas de palavras irrelevantes do banco de dados atual**  
  
-   [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)  
  
-   [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)  
  
 **Para exibir o resultado da geração de tokens de um separador de palavras, dicionário de sinônimos e combinação de lista de palavras irrelevantes (stoplist)**  
  
-   [sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md)  
  
 [Neste tópico](#TOP)  
  
##  <a name="change"></a> Alterando palavras irrelevantes em uma lista de palavras irrelevantes (stoplist)  
 **Para adicionar ou remover palavras irrelevantes em uma lista de palavras irrelevantes (stoplist)**  
  
-   [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)  
  
#### Para alterar as palavras irrelevantes em uma lista de palavras irrelevantes (stoplist) no Management Studio  
  
1.  No Pesquisador de Objetos, expanda o servidor.  
  
2.  Expanda **Bancos de Dados**e, em seguida, expanda o banco de dados.  
  
3.  Expanda **Armazenamento**e, depois, selecione **Listas de Palavras Irrelevantes de Texto Completo**.  
  
4.  Clique com o botão direito do mouse na lista de palavras irrelevantes cujas propriedades você deseja alterar e selecione **Propriedades**.  
  
5.  Na caixa de diálogo [Propriedades da lista de palavras irrelevantes de texto completo](../Topic/Full-Text%20Stoplist%20Properties.md):  
  
    1.  Na caixa de listagem **Ação** , selecione uma das seguintes ações: **Adicionar palavra irrelevante**, **Excluir palavra irrelevante**, **Excluir todas as palavras irrelevantes**ou **Limpar lista de palavras irrelevantes**.  
  
    2.  Se a caixa de texto **Palavra irrelevante** estiver habilitada para a ação selecionada, insira uma única palavra irrelevante. Essa palavra irrelevante deve ser exclusiva; ou seja, ainda não deve estar na lista de palavras irrelevantes para o idioma selecionado.  
  
    3.  Se a caixa de listagem **Idioma de texto completo** estiver habilitada para a ação selecionada, selecione um idioma.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 [Neste tópico](#TOP)  
  
##  <a name="upgrade"></a> Atualizando palavras de ruído no SQL Server 2005  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] foram substituídas por palavras irrelevantes. Quando um banco de dados é atualizado no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], os arquivos de palavras de ruído não são mais usados. No entanto, os arquivos de palavras de ruído são armazenados na pasta FTDATA\ FTNoiseThesaurusBak e você pode usá-los ao atualizar ou compilar as listas de palavras irrelevantes (stoplists) correspondentes. Para obter informações sobre como atualizar arquivos de palavras de ruído para listas de palavras irrelevantes, consulte [Atualizar pesquisa de texto completo](../../relational-databases/search/upgrade-full-text-search.md).  
  
 [Neste tópico](#TOP)  
  
  