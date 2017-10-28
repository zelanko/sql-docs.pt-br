---
title: "Introdução à pesquisa de texto completo | Microsoft Docs"
ms.date: 08/22/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text indexes [SQL Server], creating
- full-text search [SQL Server], about
- full-text search [SQL Server], setting up
ms.assetid: 1fa628ba-0ee4-4d8f-b086-c4e52962ca4a
caps.latest.revision: 76
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cb839fc8929f20c0ac7ca72dc90f364382bc33d0
ms.contentlocale: pt-br
ms.lasthandoff: 07/31/2017

---
# <a name="get-started-with-full-text-search"></a>Iniciar a pesquisa de texto completo
Por padrão, os bancos de dados do SQL Server são habilitados para texto completo. No entanto, antes de executar consultas de texto completo, é necessário criar um catálogo de texto completo e criar um índice de texto completo em tabelas ou exibições indexadas nas quais você deseja pesquisar.

## <a name="set-up-full-text-search-in-two-steps"></a>Configurar uma pesquisa de texto completo em duas etapas
Há duas etapas básicas para configurar a pesquisa de texto completo:  
1.  Criar um catálogo de texto completo.  
2.  Criar um índice de texto completo em tabelas ou em uma exibição indexada na qual você deseja pesquisar. 

Cada índice de texto completo deve pertencer a um catálogo de texto completo. Você pode criar um catálogo de texto completo separado para cada índice de texto completo ou associar vários índices de texto completo a um determinado catálogo. Um catálogo de texto completo é um objeto virtual; ele não pertence a nenhum grupo de arquivos. O catálogo é um conceito lógico que faz referência a um grupo de índices de texto completo.

> [!NOTE]
> Essas etapas presumem que você instalou os componentes opcionais de pesquisa de texto completo quando você instalou o SQL Server. Caso contrário, você precisará executar a instalação do SQL Server novamente para adicioná-los.  

## <a name="set-up-full-text-search-with-a-wizard"></a>Configurar uma pesquisa de texto completo com um assistente 
 
Para configurar a pesquisa de texto completo usando um assistente, consulte [Usar o assistente para indexação de texto completo](../../relational-databases/search/use-the-full-text-indexing-wizard.md).

## <a name="set-up-full-text-search-with-transact-sql"></a>Configurar a pesquisa de texto completo com Transact-SQL 
 O exemplo de duas partes descrito a seguir cria um catálogo de texto completo denominado `AdvWksDocFTCat` no banco de dados de exemplo AdventureWorks e, em seguida, cria um índice de texto completo na tabela `Document` no banco de dados de exemplo. Essa instrução cria o catálogo de texto completo no diretório padrão especificado durante a instalação do SQL Server. A pasta nomeada `AdvWksDocFTCat` está no diretório padrão.  
  
1.  Para criar um catálogo de texto completo denominado `AdvWksDocFTCat`, o exemplo usa uma instrução [CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md) :  
  
    ```tsql
    USE AdventureWorks;  
    GO  
    CREATE FULLTEXT CATALOG AdvWksDocFTCat;  
    ```  
    Para obter mais informações, consulte [Criar e gerenciar catálogos de texto completo](../../relational-databases/search/create-and-manage-full-text-catalogs.md).
 
2.  Para você poder criar um índice de texto completo na tabela Document, verifique se a tabela tem um índice exclusivo, de uma só coluna e não anulável. A seguinte instrução [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) cria um índice exclusivo, `ui_ukDoc`, na coluna DocumentID da tabela Documento:  
  
    ```tsql 
    CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
    ```  

3.  Depois que você tiver uma chave exclusiva, poderá criar um índice de texto completo na tabela `Document` por meio da instrução [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) a seguir.  
  
    ```tsql  
    CREATE FULLTEXT INDEX ON Production.Document  
    (  
        Document                         --Full-text index column name   
            TYPE COLUMN FileExtension    --Name of column that contains file type information  
            Language 2057                 --2057 is the LCID for British English  
    )  
    KEY INDEX ui_ukDoc ON AdvWksDocFTCat --Unique index  
    WITH CHANGE_TRACKING AUTO            --Population type;  
    GO  
  
    ```  
  
     TYPE COLUMN definido neste exemplo especifica a coluna de tipo da tabela que contém o tipo do documento em cada linha da coluna 'Document' (que é do tipo binário). A coluna de tipo armazena a extensão de arquivo fornecida pelo usuário — ".doc", ".xls" etc. — do documento em uma dada linha. O Mecanismo de Texto Completo usa a extensão de arquivo de uma dada linha para chamar o filtro correto a ser usado para analisar os dados contidos nessa linha. Após o filtro analisar os dados binários da linha, o separador de palavras especificado analisará o conteúdo. (Neste exemplo, o separador de palavras para o inglês britânico é usado.) Para obter mais informações, veja [Configurar e gerenciar filtros para pesquisa](../../relational-databases/search/configure-and-manage-filters-for-search.md).  

    Para mais informações, consulte [Criar e gerenciar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md).

##  <a name="options"></a> Escolher opções para um índice de texto completo 
  
### <a name="choose-a-language"></a>Escolher um idioma  
 Para obter mais informações sobre como escolher o idioma das colunas, consulte [Escolher um idioma ao criar um índice de texto completo](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).  
  
### <a name="choose-a-filegroup"></a>Escolher um grupo de arquivos  
 O processo de criação de um índice de texto completo é bastante intenso em relação a E/S. Resumidamente, ele consiste em ler dados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e propagar os dados filtrados para o índice de texto completo. Como prática recomendada, localize um índice de texto completo no grupo de arquivos do banco de dados que seja o mais apropriado para maximizar o desempenho de E/S ou localize os índices de texto completo em outro grupo de arquivos de outro volume.
  
### <a name="choose-a-full-text-catalog"></a>Escolher um catálogo de texto completo   
 
 Recomendamos associar tabelas com as mesmas características de atualização (como um número pequeno de alterações versus muitas alterações ou tabelas que são alteradas com frequência durante um determinado período do dia) juntas no mesmo catálogo de texto completo. Através da definição de agendas de população de catálogo de texto completo, os índices de texto completo permanecem sincronizados com as tabelas, sem afetar de modo negativo o uso de recursos do servidor de banco de dados durante períodos de alta atividade do banco de dados.  
  
 Considere as seguintes diretrizes:  
  
-   Se você estiver indexando uma tabela com milhões de linhas, atribua a tabela a seu próprio catálogo de texto completo.  
  
-   Considere o volume de alterações ocorridas nas tabelas que estão sendo indexadas com texto completo, bem como o total de linhas. Se o total de linhas que estiverem sendo alteradas, junto com o número de linhas da tabela presentes durante a última população de texto completo, representar milhões de linhas, atribua a tabela a seu próprio catálogo de texto completo.  

### <a name="associate-a-unique-index"></a>Associar um índice exclusivo
Sempre selecione o menor índice exclusivo disponível para sua chave exclusiva de texto completo. (O ideal é um índice baseado em inteiro de 4 bytes.) Isso reduz consideravelmente os recursos exigidos pelo serviço [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search no sistema de arquivos. Se a chave primária for grande (mais de 100 bytes), considere escolher outro índice exclusivo na tabela (ou criar outro índice exclusivo) como a chave exclusiva de texto completo. Caso contrário, se o tamanho da chave exclusiva de texto completo exceder o tamanho máximo permitido (900 bytes), a população de texto completo não poderá prosseguir.  
 
### <a name="associate-a-stoplist"></a>Associar uma lista de palavras irrelevantes   
  Uma *lista de palavras irrelevantes* também é conhecida como lista de palavras de ruído. Uma lista de palavras irrelevantes é associada a cada índice de texto completo, e as palavras dessa lista são aplicadas a consultas de texto completo nesse índice. Por padrão, a lista de palavras irrelevantes do sistema é associada a um novo índice de texto completo. Você também pode criar e usar sua própria lista de palavras irrelevantes.   
  
 Por exemplo, a seguinte instrução [CREATE FULLTEXT STOPLIST](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] cria uma nova lista de palavras irrelevantes de texto completo chamada myStoplist copiando da lista de palavras irrelevantes do sistema:  
  
```tsql  
CREATE FULLTEXT STOPLIST myStoplist FROM SYSTEM STOPLIST;  
GO  
```  
  
 A seguinte instrução [ALTER FULLTEXT STOPLIST](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] altera uma lista de palavras irrelevantes chamada myStoplist, adicionando a palavra 'en', primeiro para espanhol e depois para francês:  
  
```tsql  
ALTER FULLTEXT STOPLIST myStoplist ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST myStoplist ADD 'en' LANGUAGE 'French';  
GO  
```  
Para obter mais informações, veja [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes para pesquisa de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).

## <a name="update-a-full-text-index"></a>Atualizar um índice de texto completo  
 Como os índices normais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , os índices de texto completo podem ser atualizados automaticamente à medida que dados são modificados nas tabelas associadas. Esse é o comportamento padrão. Como alternativa, você pode manter seus índices de texto completo atualizados manualmente ou em intervalos agendados especificados. Popular um índice de texto completo pode ser demorado e usar muitos recursos. No entanto, a atualização de índices geralmente é feita como um processo assíncrono em segundo plano e mantém o índice de texto completo atualizado após modificações na tabela base. 
 
Atualizar um índice de texto completo imediatamente após cada alteração na tabela base também usa muitos recursos. Por isso, se você tiver uma taxa de atualização/inserção/exclusão muito alta, poderá observar alguma degradação no desempenho de consulta. Se isso ocorrer, considere agendar atualizações manuais do controle de alterações para acompanhar o ritmo das inúmeras alterações periódicas, em vez de competir por recursos com as consultas.  
  
Para obter mais informações, consulte [Popular índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md). 

## <a name="next-steps"></a>Próximas etapas
Depois de configurar a pesquisa de texto completo do SQL Server, você estará pronto para executar consultas de texto completo. Para mais informações, veja [Consulta com pesquisa de texto completo](../../relational-databases/search/query-with-full-text-search.md).

