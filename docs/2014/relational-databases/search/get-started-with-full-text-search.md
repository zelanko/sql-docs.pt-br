---
title: Introdução à pesquisa de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text indexes [SQL Server], creating
- full-text search [SQL Server], about
- full-text search [SQL Server], setting up
ms.assetid: 1fa628ba-0ee4-4d8f-b086-c4e52962ca4a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 722921015886e8aed687a8bf689dd7f7d8c592ca
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48125036"
---
# <a name="get-started-with-full-text-search"></a>Iniciar a pesquisa de texto completo
  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], por padrão, os bancos de dados são habilitados para texto completo. No entanto, para usar um índice de texto completo em uma tabela, você deve configurar o recurso de indexação de texto completo nas colunas das tabelas que deseja acessar usando o Mecanismo de Texto Completo.  
  
##  <a name="configure"></a> Configurando um banco de dados para pesquisa de texto completo  
 Em qualquer cenário, um administrador de banco de dados executa as seguintes etapas básicas para configurar as colunas de tabela de um banco de dados para pesquisa de texto completo:  
  
1.  Criar um catálogo de texto completo.  
  
2.  Em cada tabela que você deseja pesquisar, crie um índice de texto completo da seguinte maneira:  
  
    1.  Identifique cada coluna de texto a ser incluída no índice de texto completo.  
  
    2.  Se uma determinada coluna contiver documentos armazenados como dados binários (`varbinary(max)`, ou `image` dados), você deve especificar uma coluna de tabela (a *coluna de tipo*) que identifica o tipo de cada documento na coluna que está sendo indexada.  
  
    3.  Especifique o idioma que a pesquisa de texto completo deverá usar nos documentos da coluna.  
  
    4.  Escolha o mecanismo de controle de alterações que você deseja usar no índice de texto completo para controlar alterações na tabela base e em suas colunas.  
  
 A pesquisa de texto completo dá suporte a vários idiomas através do uso dos seguintes *componentes linguísticos*: separadores de palavras e lematizadores, listas de palavras irrelevantes (stoplists) (também conhecidas como palavras de ruído) e arquivos de dicionário de sinônimos. Os arquivos de dicionário de sinônimos e, em alguns casos, as listas de palavras irrelevantes exigem configuração pelo administrador de banco de dados. Um dado arquivo de dicionário de sinônimos oferece suporte a todos os índices de texto completo que usam o idioma correspondente, e uma determinada lista de palavras irrelevantes (stoplist) pode ser associada aos índices de texto completo que você desejar.  
  
##  <a name="setup"></a> Configurando um catálogo de texto completo e o índice  
 Isso envolve as seguintes etapas básicas:  
  
1.  Criar um catálogo de texto completo para armazenar índices de texto completo.  
  
     Cada índice de texto completo deve pertencer a um catálogo de texto completo. Você pode criar um catálogo de texto completo separado para cada índice de texto completo ou associar vários índices de texto completo a um determinado catálogo. Um catálogo de texto completo é um objeto virtual; ele não pertence a nenhum grupo de arquivos. O catálogo é um conceito lógico que faz referência a um grupo de índices de texto completo.  
  
2.  Crie um índice de texto completo na tabela ou exibição indexada.  
  
     Um índice de texto completo consiste em um tipo especial de índice funcional com base em token que é criado e mantido pelo Mecanismo de Texto Completo. Para criar uma pesquisa de texto completo em uma tabela ou exibição, ele deve ter um índice não nulo exclusivo de uma só coluna. O Mecanismo de Texto Completo exige que esse índice exclusivo mapeie cada linha da tabela para uma chave exclusiva e compactável. Um índice de texto completo pode incluir `char`, `varchar`, `nchar`, `nvarchar`, `text`, `ntext`, `image`, `xml`, `varbinary`, e `varbinary(max)` colunas. Para obter mais informações, veja [Criar e gerenciar índices de texto completo](create-and-manage-full-text-indexes.md).  
  
 Antes de aprender a criar índices de texto completo, é importante considerar a diferença entre eles e os índices regulares do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A tabela a seguir lista as diferenças.  
  
|Índices de texto completo|Índices regulares do SQL Server|  
|------------------------|--------------------------------|  
|Só é permitido um índice de texto completo por tabela.|Vários índices regulares são permitidos por tabela.|  
|A adição de dados a índices de texto completo, chamada de *população*, pode ser solicitada através de uma agenda ou de uma solicitação específica e pode ocorrer automaticamente com a inclusão de novos dados.|Atualizados automaticamente quando os dados nos quais eles se baseiam são inseridos, atualizados ou excluídos.|  
|Agrupados no mesmo banco de dados em um ou mais catálogos de texto completo.|Não agrupado.|  
  
  
##  <a name="options"></a> Escolhendo opções de um índice de texto completo  
 Esta seção aborda os seguintes tópicos:  
  
-   Escolhendo o idioma da coluna  
  
-   Escolhendo um grupo de arquivos para um índice de texto completo  
  
-   Atribuindo o índice de texto completo a um catálogo de texto completo  
  
-   Associando uma lista de palavras irrelevantes (stoplist) ao índice de texto completo  
  
-   Atualizando um índice de texto completo  
  
### <a name="choosing-the-column-language"></a>Escolhendo o idioma das colunas  
 Para obter mais informações sobre aspectos a considerar na escolha do idioma das colunas, consulte [Escolher um idioma ao criar um índice de texto completo](choose-a-language-when-creating-a-full-text-index.md).  
  
### <a name="choosing-a-filegroup-for-a-full-text-index"></a>Escolhendo um grupo de arquivos para um índice de texto completo  
 O processo de compilar um índice de texto completo gera bastante E/S (em um nível alto, consiste em ler os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e propagar os dados filtrados para o índice de texto completo). Como prática recomendada, localize um índice de texto completo no grupo de arquivos do banco de dados que seja o mais apropriado para maximizar o desempenho de E/S ou localize os índices de texto completo em outro grupo de arquivos de outro volume.  
  
 Se a facilidade de gerenciamento é um aspecto importante para você, é recomendável armazenar dados de tabela e qualquer catálogo de texto completo afiliado no mesmo grupo de arquivos. Às vezes, por motivo de desempenho, os dados de tabela e o índice de texto completo possivelmente precisarão estar em diferentes grupos de arquivos, armazenados em diferentes volumes, para maximizar o paralelismo de E/S.  
  
  
### <a name="assigning-the-full-text-index-to-a-full-text-catalog"></a>Atribuindo o índice de texto completo a um catálogo de texto completo  
 É importante planejar o posicionamento de índices de texto completo de tabelas em catálogos de texto completo.  
  
 Recomendamos associar tabelas com as mesmas características de atualização (como um número pequeno de alterações versus muitas alterações ou tabelas que são alteradas com frequência durante um determinado período do dia) juntas no mesmo catálogo de texto completo. Através da definição de agendas de população de catálogo de texto completo, os índices de texto completo permanecem sincronizados com as tabelas, sem afetar de modo negativo o uso de recursos do servidor de banco de dados durante períodos de alta atividade do banco de dados.  
  
 Ao atribuir uma tabela a um catálogo de texto completo, considere as seguintes diretrizes:  
  
-   Sempre selecione o menor índice exclusivo disponível para sua chave exclusiva de texto completo. (O ideal é um índice baseado em inteiro de 4 bytes.) Isso reduz consideravelmente os recursos exigidos pelo serviço [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search no sistema de arquivos. Se a chave primária for grande (mais de 100 bytes), considere escolher outro índice exclusivo na tabela (ou criar outro índice exclusivo) como a chave exclusiva de texto completo. Caso contrário, se o tamanho da chave exclusiva de texto completo exceder o tamanho máximo permitido (900 bytes), a população de texto completo não poderá prosseguir.  
  
-   Se você estiver indexando uma tabela que tem milhões de linhas, atribua a tabela a seu próprio catálogo de texto completo.  
  
-   Considere o volume de alterações ocorridas nas tabelas que estão sendo indexadas com texto completo, bem como o total de linhas. Se o total de linhas que estiverem sendo alteradas, junto com o número de linhas da tabela presentes durante a última população de texto completo, representar milhões de linhas, atribua a tabela a seu próprio catálogo de texto completo.  
  
  
### <a name="associating-a-stoplist-with-the-full-text-index"></a>Associando uma lista de palavras irrelevantes (stoplist) ao índice de texto completo  
 O [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] introduz as listas de palavras irrelevantes (stoplists). Uma *lista de palavras irrelevantes* também é conhecida como lista de palavras de ruído. Uma lista de palavras irrelevantes é associada a cada índice de texto completo, e as palavras dessa lista são aplicadas a consultas de texto completo nesse índice. Por padrão, a lista de palavras irrelevantes do sistema é associada a um novo índice de texto completo. Porém, você pode criar e usar sua própria lista de palavras irrelevantes. Para obter mais informações, veja [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes para pesquisa de texto completo](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
 Por exemplo, a seguinte [CREATE FULLTEXT STOPLIST](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrução cria um novo stoplist de texto completo chamado myStoplist3 copiando-se a lista de palavras irrelevantes do sistema:  
  
```  
CREATE FULLTEXT STOPLIST myStoplist FROM SYSTEM STOPLIST;  
GO  
```  
  
 O seguinte [ALTER FULLTEXT STOPLIST](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrução altera uma lista de palavras irrelevantes chamada myStoplist, adicionando a palavra 'en', primeiro para espanhol e depois para francês:  
  
```  
ALTER FULLTEXT STOPLIST MyStoplist ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST MyStoplist ADD 'en' LANGUAGE 'French';  
GO  
```  
  
  
### <a name="updating-a-full-text-index"></a>Atualizando um índice de texto completo  
 Como os índices normais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , os índices de texto completo podem ser atualizados automaticamente à medida que dados são modificados nas tabelas associadas. Esse é o comportamento padrão. Se preferir, você pode manter seus índices de texto completo atualizados manualmente ou em intervalos agendados específicos. Preencher um índice de texto completo pode ser um procedimento demorado e usar muitos recursos, por isso a atualização de índices geralmente é feita como um processo assíncrono em segundo plano e mantém o índice de texto completo atualizado após modificações na tabela base. Atualizar um índice de texto completo imediatamente depois de cada alteração na tabela base pode demandar muitos recursos. Por isso, se você tiver uma taxa de atualização/inserção/exclusão muito alta, poderá observar alguma diminuição no desempenho de consulta. Se isso ocorrer, considere agendar atualizações manuais do controle de alterações para acompanhar o ritmo das inúmeras alterações periódicas, em vez de competir por recursos com as consultas.  
  
 Para monitorar o status de população, use as funções FULLTEXTCATALOGPROPERTY ou OBJECTPROPERTYEX. Para obter o status de população de catálogo, execute a seguinte instrução:  
  
```  
SELECT FULLTEXTCATALOGPROPERTY('AdvWksDocFTCat', 'Populatestatus');  
```  
  
 Geralmente, se uma população completa estiver em andamento, o resultado retornado será 1.  
  
  
##  <a name="example"></a> Exemplo: Configurando a pesquisa de texto completo  
 O exemplo de duas partes descrito a seguir cria um catálogo de texto completo denominado `AdvWksDocFTCat` no banco de dados AdventureWorks e, em seguida, cria um índice de texto completo na tabela `Document` do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Essa instrução cria o catálogo de texto completo no diretório padrão especificado durante a instalação. A pasta nomeada `AdvWksDocFTCat` está no diretório padrão.  
  
1.  Para criar um catálogo de texto completo denominado `AdvWksDocFTCat`, o exemplo usa uma instrução [CREATE FULLTEXT CATALOG](/sql/t-sql/statements/create-fulltext-catalog-transact-sql):  
  
    ```  
    USE AdventureWorks;  
    GO  
    CREATE FULLTEXT CATALOG AdvWksDocFTCat;  
    ```  
  
2.  Para você poder criar um índice de texto completo na tabela Document, verifique se a tabela tem um índice exclusivo, de uma só coluna e não anulável. A seguinte instrução [CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql) cria um índice exclusivo, `ui_ukDoc`, na coluna DocumentID da tabela Documento:  
  
    ```  
    CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
    ```  
  
3.  Depois que você tiver uma chave exclusiva, poderá criar um índice de texto completo na tabela `Document` por meio da instrução [CREATE FULLTEXT INDEX](/sql/t-sql/statements/create-fulltext-index-transact-sql) a seguir.  
  
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
  
     TYPE COLUMN definido neste exemplo especifica a coluna de tipo da tabela que contém o tipo do documento em cada linha da coluna 'Document' (que é do tipo binário). A coluna de tipo armazena a extensão de arquivo fornecida pelo usuário — ".doc", ".xls" etc. — do documento em uma dada linha. O Mecanismo de Texto Completo usa a extensão de arquivo de uma dada linha para chamar o filtro correto a ser usado para analisar os dados contidos nessa linha. Depois que o filtro analisar os dados binários da linha, o separador de palavras especificado analisará o conteúdo (neste exemplo, é usado o separador de palavras do inglês britânico). Observe que o processo de filtragem ocorre apenas durante a indexação ou se um usuário inserir ou atualizar uma coluna na tabela base enquanto o controle automático de alterações está habilitado para o índice de texto completo. Para obter mais informações, veja [Configurar e gerenciar filtros para pesquisa](configure-and-manage-filters-for-search.md).  
  
  
##  <a name="tasks"></a> Tarefas comuns  
  
### <a name="to-create-a-full-text-catalog"></a>Para criar um catálogo de texto completo  
  
-   [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)  
  
-   [Criar e gerenciar catálogos de texto completo](create-and-manage-full-text-catalogs.md)  
  
### <a name="to-view-the-indexes-of-a-table-or-view"></a>Para visualizar os índices de uma tabela (ou exibição)  
  
-   [sys.indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)  
  
### <a name="to-create-a-unique-index"></a>Para criar um índice exclusivo  
  
-   [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)  
  
-   [Abrir o Designer de Tabela &#40;Ferramentas de Banco de Dados Visual&#41;](../../ssms/visual-db-tools/visual-database-tools.md)  
  
### <a name="to-create-a-full-text-index"></a>Para criar um índice de texto completo  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
-   [Criar e gerenciar índices de texto completo](create-and-manage-full-text-indexes.md)  
  
### <a name="to-view-information-about-a-full-text-index"></a>Para exibir informações sobre um índice de texto completo  
  
|Exibição de catálogo ou de gerenciamento dinâmico|Description|  
|----------------------------------------|-----------------|  
|[sys.fulltext_index_catalog_usages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql)|Retorna uma linha para cada catálogo de texto completo para referência de índice de texto completo.|  
|[sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)|Contém uma linha para cada coluna que faz parte de um índice de texto completo.|  
|[sys.fulltext_index_fragments &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql)|Um índice de texto completo usa tabelas internas, chamadas de fragmentos de índice de texto completo, para armazenar os dados de índices invertidos. Esta exibição pode ser usada para consultar os metadados sobre estes fragmentos. Esta exibição contém uma linha para cada fragmento de índice de texto completo em toda tabela que contém um índice de texto completo.|  
|[sys.fulltext_indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql)|Contém uma linha por índice de texto completo de um objeto tabular.|  
|[sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql)|Retorna informações sobre o conteúdo de um índice de texto completo da tabela especificada.|  
|[sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql)|Retorna informações sobre o conteúdo no nível de documento de um índice de texto completo da tabela especificada. Uma determinada palavra-chave pode aparecer em vários documentos.|  
|[sys.dm_fts_index_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)|Retorna informações sobre as populações de índice de texto completo que estão em andamento.|  
  
  
## <a name="see-also"></a>Consulte também  
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)   
 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)   
 [Popular índices de texto completo](populate-full-text-indexes.md)   
 [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql)   
 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql)  
  
  
