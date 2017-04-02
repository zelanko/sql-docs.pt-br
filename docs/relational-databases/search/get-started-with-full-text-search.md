---
title: "Iniciar a pesquisa de texto completo | Microsoft Docs"
ms.date: "08/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "catálogos de texto completo [SQL Server], criando"
  - "índices de texto completo [SQL Server], criando"
  - "pesquisa de texto completo [SQL Server], sobre"
  - "pesquisa de texto completo [SQL Server], configurando"
ms.assetid: 1fa628ba-0ee4-4d8f-b086-c4e52962ca4a
caps.latest.revision: 76
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 72
---
# Iniciar a pesquisa de texto completo
A pesquisa de texto completo dá suporte a vários idiomas através do uso dos seguintes *componentes linguísticos*: separadores de palavras e lematizadores, listas de palavras irrelevantes (stoplists) (também conhecidas como palavras de ruído) e arquivos de dicionário de sinônimos. Os arquivos de dicionário de sinônimos e, em alguns casos, as listas de palavras irrelevantes exigem configuração pelo administrador de banco de dados. Um dado arquivo de dicionário de sinônimos oferece suporte a todos os índices de texto completo que usam o idioma correspondente, e uma determinada lista de palavras irrelevantes (stoplist) pode ser associada aos índices de texto completo que você desejar.  
 
Por padrão, bancos de dados SQL Server são habilitados para texto completo, mas primeiro necessário [criar um catálogo de texto completo](https://msdn.microsoft.com/library/bb326035.aspx) e criar um índice de texto completo em tabelas ou exibições indexadas nas quais você deseja pesquisar.
 
 ## Instruções passo a passo 
 
 Vá para o tópico [Usar o Assistente para Indexação de Texto Completo](https://msdn.microsoft.com/library/ms180091.aspx) para obter as instruções passo a passo.

Este tópico aborda considerações, exemplos e links para outros tópicos.
##  <a name="configure"></a> Planejar a instalação

Há duas etapas básicas para configurar colunas de tabela em um banco de dados para a pesquisa de texto completo:  
  
- Criar um catálogo de texto completo.  
  
- Criar um índice de texto completo em tabelas ou em uma exibição indexada na qual você deseja pesquisar. 

     Um índice de texto completo é um tipo especial de índice funcional baseado em token criado e mantido pelo Mecanismo de Texto Completo. Para criar uma pesquisa de texto completo em uma tabela ou exibição, ele deve ter um índice não nulo exclusivo de uma só coluna. O Mecanismo de Texto Completo exige que esse índice exclusivo mapeie cada linha da tabela para uma chave exclusiva e compactável. Um índice de texto completo inclui as colunas **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml**, **varbinary**, e **varbinary(max)**. Para obter mais informações, veja [Criar e gerenciar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md).   
  
     Cada índice de texto completo deve pertencer a um catálogo de texto completo. Você pode criar um catálogo de texto completo separado para cada índice de texto completo ou associar vários índices de texto completo a um determinado catálogo. Um catálogo de texto completo é um objeto virtual; ele não pertence a nenhum grupo de arquivos. O catálogo é um conceito lógico que faz referência a um grupo de índices de texto completo.  
  

 Diferenças entre índices de texto completo e índices regulares do SQL Server:  
  
|Índices de texto completo|Índices regulares do SQL Server|  
|------------------------|--------------------------------|  
|Só é permitido um índice de texto completo por tabela.|Vários índices regulares são permitidos por tabela.|  
|A adição de dados a índices de texto completo, chamada de *população*, pode ser solicitada através de uma agenda ou de uma solicitação específica e pode ocorrer automaticamente com a inclusão de novos dados.|Atualizados automaticamente quando os dados nos quais eles se baseiam são inseridos, atualizados ou excluídos.|  
|Agrupados no mesmo banco de dados em um ou mais catálogos de texto completo.|Não agrupado.|  
    
##  <a name="options"></a> Opções  
  
### Idioma da coluna  
 Para obter mais informações sobre como escolher o idioma das colunas, consulte [Escolher um idioma ao criar um índice de texto completo](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).  
  
### Escolher um grupo de arquivos para um índice de texto completo  
 O processo de compilar um índice de texto completo gera bastante E/S (em um nível alto, consiste em ler os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e propagar os dados filtrados para o índice de texto completo). Como prática recomendada, localize um índice de texto completo no grupo de arquivos do banco de dados que seja o mais apropriado para maximizar o desempenho de E/S ou localize os índices de texto completo em outro grupo de arquivos de outro volume.  
  
 Recomendamos armazenar os dados da tabela e todos os catálogos de texto completo afiliados no mesmo grupo de arquivos. Às vezes, por motivos de desempenho, talvez você queira que os dados de tabela e o índice de texto completo estejam em diferentes grupos de arquivos, armazenados em diferentes volumes, para maximizar o paralelismo de E/S.  

  
### Atribuir o índice de texto completo   
 
 Recomendamos associar tabelas com as mesmas características de atualização (como um número pequeno de alterações versus muitas alterações ou tabelas que são alteradas com frequência durante um determinado período do dia) juntas no mesmo catálogo de texto completo. Através da definição de agendas de população de catálogo de texto completo, os índices de texto completo permanecem sincronizados com as tabelas, sem afetar de modo negativo o uso de recursos do servidor de banco de dados durante períodos de alta atividade do banco de dados.  
  
 Considere as seguintes diretrizes:  
  
-   Sempre selecione o menor índice exclusivo disponível para sua chave exclusiva de texto completo. (O ideal é um índice baseado em inteiro de 4 bytes.) Isso reduz consideravelmente os recursos exigidos pelo serviço [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search no sistema de arquivos. Se a chave primária for grande (mais de 100 bytes), considere escolher outro índice exclusivo na tabela (ou criar outro índice exclusivo) como a chave exclusiva de texto completo. Caso contrário, se o tamanho da chave exclusiva de texto completo exceder o tamanho máximo permitido (900 bytes), a população de texto completo não poderá prosseguir.  
  
-   Se você estiver indexando uma tabela com milhões de linhas, atribua a tabela a seu próprio catálogo de texto completo.  
  
-   Considere o volume de alterações ocorridas nas tabelas que estão sendo indexadas com texto completo, bem como o total de linhas. Se o total de linhas que estiverem sendo alteradas, junto com o número de linhas da tabela presentes durante a última população de texto completo, representar milhões de linhas, atribua a tabela a seu próprio catálogo de texto completo.  

  
### Associar uma lista de palavras irrelevantes   
  Uma *lista de palavras irrelevantes* também é conhecida como lista de palavras de ruído. Uma lista de palavras irrelevantes é associada a cada índice de texto completo, e as palavras dessa lista são aplicadas a consultas de texto completo nesse índice. Por padrão, a lista de palavras irrelevantes do sistema é associada a um novo índice de texto completo. Você também pode criar e usar sua própria lista de palavras irrelevantes. Para obter mais informações, veja [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes para pesquisa de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
 Por exemplo, a seguinte instrução [CREATE FULLTEXT STOPLIST](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] cria uma nova lista de palavras irrelevantes de texto completo chamada myStoplist3 copiando da lista de palavras irrelevantes do sistema:  
  
```  
CREATE FULLTEXT STOPLIST myStoplist FROM SYSTEM STOPLIST;  
GO  
```  
  
 A seguinte instrução [ALTER FULLTEXT STOPLIST](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] altera uma lista de palavras irrelevantes chamada myStoplist, adicionando a palavra 'en', primeiro para espanhol e depois para francês:  
  
```  
ALTER FULLTEXT STOPLIST MyStoplist ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST MyStoplist ADD 'en' LANGUAGE 'French';  
GO  
```  
    
## Atualizar um índice  
 Como os índices normais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os índices de texto completo podem ser atualizados automaticamente à medida que dados são modificados nas tabelas associadas. Esse é o comportamento padrão. Como alternativa, você pode manter seus índices de texto completo atualizados manualmente ou em intervalos agendados especificados. Preencher um índice de texto completo pode ser um procedimento demorado e usar muitos recursos, por isso a atualização de índices geralmente é feita como um processo assíncrono em segundo plano e mantém o índice de texto completo atualizado após modificações na tabela base. 
 
 Atualizar um índice de texto completo imediatamente depois de cada alteração na tabela base pode demandar muitos recursos. Por isso, se você tiver uma taxa de atualização/inserção/exclusão muito alta, poderá observar alguma diminuição no desempenho de consulta. Se isso ocorrer, considere agendar atualizações manuais do controle de alterações para acompanhar o ritmo das inúmeras alterações periódicas, em vez de competir por recursos com as consultas.  
  
 Monitore o status da população usando as funções FULLTEXTCATALOGPROPERTY ou OBJECTPROPERTYEX. Para obter o status de população de catálogo, execute a seguinte instrução:  
  
```  
SELECT FULLTEXTCATALOGPROPERTY('AdvWksDocFTCat', 'Populatestatus');  
```  
  
 Geralmente, se uma população completa estiver em andamento, o resultado retornado será 1.  
 

##  <a name="example"></a> Exemplo: Configurar uma pesquisa de texto completo  
 O exemplo de duas partes descrito a seguir cria um catálogo de texto completo denominado `AdvWksDocFTCat` no banco de dados AdventureWorks e, em seguida, cria um índice de texto completo na tabela `Document` do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Essa instrução cria o catálogo de texto completo no diretório padrão especificado durante a instalação. A pasta nomeada `AdvWksDocFTCat` está no diretório padrão.  
  
1.  Para criar um catálogo de texto completo denominado `AdvWksDocFTCat`, o exemplo usa uma instrução [CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md):  
  
    ```  
    USE AdventureWorks;  
    GO  
    CREATE FULLTEXT CATALOG AdvWksDocFTCat;  
    ```  
  
2.  Para você poder criar um índice de texto completo na tabela Document, verifique se a tabela tem um índice exclusivo, de uma só coluna e não anulável. A seguinte instrução [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) cria um índice exclusivo, `ui_ukDoc`, na coluna DocumentID da tabela Documento:  
  
    ```  
    CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
    ```  
  
3.  Depois que você tiver uma chave exclusiva, poderá criar um índice de texto completo na tabela `Document` por meio da instrução [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) a seguir.  
  
    ```  
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
  
     TYPE COLUMN definido neste exemplo especifica a coluna de tipo da tabela que contém o tipo do documento em cada linha da coluna 'Document' (que é do tipo binário). A coluna de tipo armazena a extensão de arquivo fornecida pelo usuário — ".doc", ".xls" etc. — do documento em uma dada linha. O Mecanismo de Texto Completo usa a extensão de arquivo de uma dada linha para chamar o filtro correto a ser usado para analisar os dados contidos nessa linha. Depois que o filtro analisar os dados binários da linha, o separador de palavras especificado analisará o conteúdo (neste exemplo, é usado o separador de palavras do inglês britânico). Observe que o processo de filtragem ocorre apenas durante a indexação ou se um usuário inserir ou atualizar uma coluna na tabela base enquanto o controle automático de alterações está habilitado para o índice de texto completo. Para obter mais informações, veja [Configurar e gerenciar filtros para pesquisa](../../relational-databases/search/configure-and-manage-filters-for-search.md).  
  
   
## Criar um catálogo de texto completo  
  
-   [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)  
  
-   [Criar e gerenciar catálogos de texto completo](../../relational-databases/search/create-and-manage-full-text-catalogs.md)  
  
## Exibir os índices  
  
-   [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
## Criar um índice exclusivo  
  
-   [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
-   [Abrir o Designer de Tabela &#40;Ferramentas de Banco de Dados Visual&#41;](../../ssms/visual-db-tools/open-table-designer-visual-database-tools.md)  
  
## Criar um índice de texto completo  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)  
  
-   [Criar e gerenciar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md)  
  
## Exibir informações sobre um índice de texto completo  
  
|Exibição de catálogo ou de gerenciamento dinâmico|Descrição|  
|----------------------------------------|-----------------|  
|[sys.fulltext_index_catalog_usages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)|Retorna uma linha para cada catálogo de texto completo para referência de índice de texto completo.|  
|[sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)|Contém uma linha para cada coluna que faz parte de um índice de texto completo.|  
|[sys.fulltext_index_fragments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)|Um índice de texto completo usa tabelas internas, chamadas de fragmentos de índice de texto completo, para armazenar os dados de índices invertidos. Esta exibição pode ser usada para consultar os metadados sobre estes fragmentos. Esta exibição contém uma linha para cada fragmento de índice de texto completo em toda tabela que contém um índice de texto completo.|  
|[sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)|Contém uma linha por índice de texto completo de um objeto tabular.|  
|[sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)|Retorna informações sobre o conteúdo de um índice de texto completo da tabela especificada.|  
|[sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)|Retorna informações sobre o conteúdo no nível de documento de um índice de texto completo da tabela especificada. Uma determinada palavra-chave pode aparecer em vários documentos.|  
|[sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)|Retorna informações sobre as populações de índice de texto completo que estão em andamento.|  
  

  
## E mais informações 
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Popular índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md)   
 [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)  
  
  