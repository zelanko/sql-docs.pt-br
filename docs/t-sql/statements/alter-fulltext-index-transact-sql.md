---
description: ALTER FULLTEXT INDEX (Transact-SQL)
title: ALTER FULLTEXT INDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER FULLTEXT INDEX
- ALTER_FULLTEXT_INDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- modifying full-text indexes
- full-text indexes [SQL Server], modifying
- search property lists [SQL Server], associating with full-text indexes
- ALTER FULLTEXT INDEX statement
ms.assetid: b6fbe9e6-3033-4d1b-b6bf-1437baeefec3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 584fcb85f71d253fd2ecc471d64c58579cf2c233
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124263"
---
# <a name="alter-fulltext-index-transact-sql"></a>ALTER FULLTEXT INDEX (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Altera as propriedades de um índice de texto completo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
ALTER FULLTEXT INDEX ON table_name  
   { ENABLE   
   | DISABLE  
   | SET CHANGE_TRACKING [ = ] { MANUAL | AUTO | OFF }  
   | ADD ( column_name   
           [ TYPE COLUMN type_column_name ]   
           [ LANGUAGE language_term ]  
           [ STATISTICAL_SEMANTICS ]  
           [,...n]   
         )  
     [ WITH NO POPULATION ]  
   | ALTER COLUMN column_name  
     { ADD | DROP } STATISTICAL_SEMANTICS  
     [ WITH NO POPULATION ]  
   | DROP ( column_name [,...n] )  
     [ WITH NO POPULATION ]   
   | START { FULL | INCREMENTAL | UPDATE } POPULATION  
   | {STOP | PAUSE | RESUME } POPULATION   
   | SET STOPLIST [ = ] { OFF| SYSTEM | stoplist_name }  
     [ WITH NO POPULATION ]   
   | SET SEARCH PROPERTY LIST [ = ] { OFF | property_list_name }  
     [ WITH NO POPULATION ]   
   }  
[;]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *table_name*  
 É o nome da tabela ou exibição indexada que contém a coluna ou colunas incluídas no índice de texto completo. A especificação dos nomes dos proprietários da tabela e do banco de dados é opcional.  
  
 ENABLE | DISABLE  
 Instrui o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quanto à coleta de dados de índice de texto completo para *table_name*. ENABLE ativa o índice de texto completo. DISABLE desativa o índice de texto completo. A tabela não dará suporte a consultas de texto completo enquanto o índice estiver desabilitado.  
  
 Desabilitar um índice de texto completo permite desativar o controle de alterações, mantendo o índice de texto completo que você pode reativar usando ENABLE a qualquer momento. Quando o índice de texto completo é desabilitado, os metadados de índice de texto completo permanecem nas tabelas do sistema. Se CHANGE_TRACKING estiver no estado habilitado (atualização automática ou manual) quando o índice de texto completo for desabilitado, o estado do índice congelará, qualquer rastreamento em andamento será interrompido e as novas alterações nos dados de tabela não serão controladas nem propagadas no índice.  
  
 SET CHANGE_TRACKING {MANUAL | AUTO | OFF}  
 Especifica se as alterações (atualizações, exclusões ou inserções) feitas nas colunas da tabela cobertas pelo índice de texto completo serão propagadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o índice de texto completo. As alterações de dados por meio de WRITETEXT e UPDATETEXT não são refletidas no índice de texto completo e não são coletadas com o controle de alterações.  
  
> [!NOTE]  
>  Para obter mais informações, confira [Interações do Controle de Alterações com o parâmetro NO POPULATION](#change-tracking-no-population).
  
 MANUAL  
 Especifica que as alterações controladas serão propagadas manualmente chamando-se a instrução ALTER FULLTEXT INDEX ... Instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] START UPDATE POPULATION (*preenchimento manual*). É possível usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para chamar essa instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] periodicamente.  
  
 AUTO  
 Especifica que as alterações controladas serão propagadas automaticamente conforme os dados forem modificados na tabela base (*preenchimento automático*). Embora sejam propagadas automaticamente, talvez essas alterações não se reflitam imediatamente no índice de texto completo. AUTO é o padrão.  
  
 OFF  
 Especifica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não manterá uma lista de alterações nos dados indexados.  
  
 ADD | DROP *column_name*  
 Especifica as colunas a serem adicionadas ou excluídas de um índice de texto completo. A coluna ou colunas devem ser do tipo **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml**, **varbinary** ou **varbinary(max)**.  
  
 Use a cláusula DROP apenas em colunas que foram habilitadas anteriormente para indexação de texto completo.  
  
 Use TYPE COLUMN e LANGUAGE com a cláusula ADD para definir essas propriedades em *column_name*. Quando uma coluna é adicionada, o índice de texto completo na tabela deve ser repopulado para que as consultas de texto completo nessa coluna funcionem.  
  
> [!NOTE]  
>  O fato de o índice de texto completo ser populado depois que uma coluna é adicionada ou removida de um índice de texto completo depende de o controle de alterações estar habilitado e de WITH NO POPULATION ter sido especificado. Para obter mais informações, confira [Interações do Controle de Alterações com o parâmetro NO POPULATION](#change-tracking-no-population).
  
 TYPE COLUMN *type_column_name*  
 Especifica o nome de uma coluna de tabela, *type_column_name*, usada para manter o tipo de um documento para um documento **varbinary**, **varbinary(max)** ou **image** . Essa coluna, conhecida como coluna de tipo, contém uma extensão de arquivo fornecida pelo usuário (.doc, .pdf, .xls e assim por diante). A coluna de tipo deve ser do tipo **char**, **nchar**, **varchar**, ou **nvarchar**.  
  
 Especifique TYPE COLUMN *type_column_name* somente se *column_name* especificar uma coluna **varbinary**, **varbinary(max)** ou **image** na qual os dados são armazenados como dados binários. Caso contrário, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará um erro.  
  
> [!NOTE]  
>  No momento da indexação, o Mecanismo de Texto Completo usa a abreviação na coluna de tipo de cada linha da tabela para identificar o filtro de pesquisa de texto completo que deve ser usado para o documento no *column_name*. O filtro carrega o documento como um fluxo binário, remove as informações de formatação e envia o texto do documento para o componente do separador de palavras. Para obter mais informações, veja [Configurar e gerenciar filtros para pesquisa](../../relational-databases/search/configure-and-manage-filters-for-search.md).  
  
 LANGUAGE *language_term*  
 É o idioma dos dados armazenados em **column_name**.  
  
 *language_term* é opcional e pode ser especificado como uma cadeia de caracteres, um inteiro ou um valor hexadecimal que corresponda ao LCID (identificador de localidade) de um idioma. Se *language_term* for especificado, o idioma que ele representa será aplicado a todos os elementos do critério de pesquisa. Se nenhum valor for especificado, o idioma de texto completo padrão da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será usado.  
  
 Use o procedimento armazenado **sp_configure** para acessar informações sobre o idioma de texto completo padrão da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Quando especificado como uma cadeia de caracteres, *language_term* corresponde ao valor da coluna **alias** na tabela do sistema **syslanguages**. A cadeia de caracteres precisa ser colocada entre aspas, como em '*language_term*'. Quando especificado como um inteiro, *language_term* é a LCID real que identifica o idioma. Quando especificado como um valor hexadecimal, *language_term* é 0x seguido pelo valor hexadecimal da LCID. O valor hexadecimal não deve exceder oito dígitos, incluindo zeros à esquerda.  
  
 Se o valor estiver no formato DBCS (conjunto de caracteres de dois bytes), o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o converterá em Unicode.  
  
 Os recursos, como separadores e lematizadores de palavras, devem estar habilitados para o idioma especificado como *language_term*. Se tais recursos não aceitarem o idioma especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará um erro.  
  
 Para colunas não BLOB e não XML que contêm dados de texto em vários idiomas ou nos casos em que o idioma do texto armazenado na coluna é desconhecido, use o recurso de idioma neutro (0x0). Para documentos armazenados em colunas do tipo XML ou BLOB, a codificação de idioma do documento será usada no momento da indexação. Por exemplo, em colunas XML, o atributo xml:lang em documentos XML identificará o idioma. No momento da consulta, o valor especificado anteriormente em *language_term* se torna o idioma padrão usado para consultas de texto completo, a menos que *language_term* seja especificado como parte de uma consulta de texto completo.  
  
 STATISTICAL_SEMANTICS  
 **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.  
  
 Cria a frase-chave adicional e índices de similaridade de documentos que fazem parte da indexação semântica estatística. Para obter mais informações, veja [Pesquisa semântica &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md).  
  
 [ **,**_...n_]  
 Indica que várias colunas podem ser especificadas para as cláusulas ADD, ALTER ou DROP. Ao especificar várias colunas, separe-as com vírgulas.  
  
 WITH NO POPULATION  
 Especifica que o índice de texto completo não será populado depois de uma operação de coluna ADD ou DROP, ou uma operação SET STOPLIST. O índice será populado somente se o usuário executar um comando START... POPULATION.  
  
 Quando a opção NO POPULATION for especificada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não populará um índice. O índice será populado somente depois que o usuário executar um comando ALTER FULLTEXT INDEX...START POPULATION. Quando a opção NO POPULATION não for especificada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] populará o índice.  
  
 Se CHANGE_TRACKING estiver habilitado e WITH NO POPULATION for especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará um erro. Se CHANGE_TRACKING estiver habilitado e WITH NO POPULATION não for especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executará um preenchimento completo do índice.  
  
> [!NOTE]  
>  Para obter mais informações, confira [Interações do Controle de Alterações com o parâmetro NO POPULATION](#change-tracking-no-population).
  
 {ADD | DROP } STATISTICAL_SEMANTICS  
 **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.  
  
 Habilita ou desabilita a indexação semântica estatística para as colunas especificadas. Para obter mais informações, veja [Pesquisa semântica &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md).  
  
 START {FULL|INCREMENTAL|UPDATE} POPULATION  
 Instrui o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a começar a preencher o índice de texto completo de *table_name*. Se um preenchimento de índice de texto completo já estiver em andamento, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará um aviso e não iniciará o novo preenchimento.  
  
 FULL  
 Especifica que cada linha da tabela deve ser recuperada para a indexação de texto completo, mesmo que as linhas já tenham sido indexadas.  
  
 INCREMENTAL  
 Especifica que somente as linhas modificadas desde que a última população devem ser recuperadas para indexação de texto completo. INCREMENTAL poderá ser aplicado somente se a tabela tiver uma coluna do tipo **timestamp**. Se uma tabela no catálogo de texto completo não tiver uma coluna do tipo **timestamp**, a tabela passará por um preenchimento FULL.  
  
 UPDATE  
 Especifica o processamento de todas as inserções, atualizações ou exclusões desde a última vez que o índice de controle de alterações foi atualizado. A população de controle de alterações deve estar habilitada em uma tabela, mas o índice de atualização em segundo plano ou o controle de alterações automático não devem estar ativados.  
  
 {STOP | PAUSE | RESUME } POPULATION  
 Interrompe ou pausa todas as populações em andamento; ou interrompe ou retoma todas as populações pausadas.  
  
 STOP POPULATION não interrompe o controle de alterações automático ou o índice de atualização em segundo plano. Para interromper o controle de alterações, use SET CHANGE_TRACKING OFF.  
  
 PAUSE POPULATION e RESUME POPULATION podem ser usados somente para populações completas. Eles não são relevantes para outros tipos de população porque as outras populações retomam os rastreamentos do ponto em que eles pararam.  
  
 SET STOPLIST { OFF| SYSTEM | *stoplist_name* }  
 Altera a lista de palavras irrelevantes de texto completo associada ao índice, se houver.  
  
 OFF  
 Especifica que nenhuma lista de palavras irrelevantes seja associada ao índice de texto completo.  
  
 SYSTEM  
 Especifica que a lista de palavras irrelevantes do sistema de texto completo padrão deve ser usada para esse índice de texto completo.  
  
 *stoplist_name*  
 Especifica o nome da lista de palavras irrelevantes que deve ser associada ao índice de texto completo.  
  
 Para obter mais informações, veja [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes para pesquisa de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
 SET SEARCH PROPERTY LIST { OFF | *property_list_name* } [ WITH NO POPULATION ]  
 **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.  
  
 Altera a lista de propriedades de pesquisa associada ao índice, se houver.  
  
 OFF  
 Especifica que nenhuma lista de propriedades será associada ao índice de texto completo. Quando você desliga a lista de propriedades de pesquisa de um índice de texto completo (ALTER FULLTEXT INDEX... SET SEARCH PROPERTY LIST OFF), a pesquisa de propriedades na tabela base não é mais possível.  
  
 Por padrão, quando você desativar uma lista de propriedades de pesquisa existente, o índice de texto completo será repopulado automaticamente. Se você especificar WITH NO POPULATION quando desativar a lista de propriedades de pesquisa, a repopulação automática não ocorrerá. Porém, quando for conveniente, é recomendável executar uma população completa nesse índice de texto completo. A repopulação do índice de texto completo remove os metadados específicos de cada propriedade de pesquisa removida, o que torna o índice de texto completo menor e mais eficiente.  
  
 *property_list_name*  
 Especifica o nome da lista de propriedades de pesquisa que deve ser associada ao índice de texto completo.  
  
 A adição de uma lista de propriedades de pesquisa a um índice de texto completo exige a repopulação do índice para indexar as propriedades de pesquisa que são registradas para a lista de propriedades de pesquisa associada. Se você especificar WITH NO POPULATION ao adicionar a lista de propriedades de pesquisa, será necessário executar uma população no índice em um momento apropriado.  
  
> [!IMPORTANT]  
>  Se o índice de texto completo foi previamente associado a uma outra pesquisa, ele deverá ser a lista de propriedades recriada para que o índice tenha um estado consistente. O índice é truncado imediatamente e fica vazio até que a população completa seja executada. Para obter mais informações, confira [A alteração da lista de propriedades de pesquisa causa a recriação do índice](#change-search-property-rebuild-index). 
  
> [!NOTE]  
>  Você pode associar uma determinada lista de propriedades de pesquisa a mais de um índice de texto completo no mesmo banco de dados.  
  
 **Para localizar as listas de propriedades de pesquisa no banco de dados atual**  
  
-   [sys.registered_search_property_lists](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
 Para obter mais informações sobre listas de propriedades de pesquisa, veja [Pesquisar propriedades de documento com listas de propriedades de pesquisa](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="interactions-of-change-tracking-and-no-population-parameter"></a><a name="change-tracking-no-population"></a> Interações do Controle de Alterações com o parâmetro NO POPULATION  
 O fato de o índice de texto completo ser populado depende de o controle de alterações estar habilitado e de WITH NO POPULATION ter sido especificado na instrução ALTER FULLTEXT INDEX. A tabela a seguir resume o resultado da interação.  
  
|Controle de Alterações|WITH NO POPULATION|Result|  
|---------------------|------------------------|------------|  
|Não habilitado|Não especificado|Uma população completa é executada no índice.|  
|Não habilitado|Especificado|Não ocorre nenhuma população do índice até que uma instrução ALTER FULLTEXT INDEX...START POPULATION seja emitida.|  
|habilitado|Especificado|É gerado um erro e o índice não é alterado.|  
|habilitado|Não especificado|Uma população completa é executada no índice.|  
  
 Para obter mais informações sobre o preenchimento de índices de texto completo, veja [Preencher índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).  
  
## <a name="changing-the-search-property-list-causes-rebuilding-the-index"></a><a name="change-search-property-rebuild-index"></a> A alteração da lista de propriedades de pesquisa causa a recriação do índice  
 Da primeira vez que um índice de texto completo é associado a uma lista de propriedades de pesquisa, o índice deve ser repopulado para indexar termos de pesquisa específicos da propriedade. Os dados de índice existentes não são truncados.  
  
 Porém, se você associar o índice de texto completo a uma outra lista de propriedades, o índice será recriado. A recriação trunca o índice de texto completo imediatamente, removendo todos os dados existentes, e o índice deve ser repopulado. Enquanto o preenchimento é realizado, consultas de texto completo na tabela base pesquisam apenas nas linhas da tabela que já foram indexadas pelo preenchimento. Os dados de índice repopulados incluirão metadados das propriedades registradas da lista de propriedades de pesquisa recém-adicionada.  
  
 Os cenários que causam a recriação incluem:  
  
-   Alternando diretamente para uma outra lista de propriedades de pesquisa (consulte "Cenário A" posteriormente nesta seção).  
  
-   Desativando a lista de propriedades de pesquisa e depois associando o índice a qualquer lista de propriedades de pesquisa (consulte "Cenário B" posteriormente nesta seção).  
  
> [!NOTE]  
>  Para obter mais informações sobre como a pesquisa de texto completo funciona com listas de propriedades de pesquisa, veja [Pesquisar propriedades de documento com listas de propriedades de pesquisa](../../relational-databases/search/search-document-properties-with-search-property-lists.md). Para obter informações sobre índices de texto completo, veja [Preencher índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).  
  
### <a name="scenario-a-switching-directly-to-a-different-search-property-list"></a>Cenário A: Alternando diretamente para uma outra lista de propriedades de pesquisa  
  
1.  Um índice de texto completo é criado em `table_1` com uma lista de propriedades de pesquisa `spl_1`:  
  
    ```sql  
    CREATE FULLTEXT INDEX ON table_1 (column_name) KEY INDEX unique_key_index   
       WITH SEARCH PROPERTY LIST=spl_1,   
       CHANGE_TRACKING OFF, NO POPULATION;   
    ```  
  
2.  Uma população completa é executada no índice de texto completo:  
  
    ```sql  
    ALTER FULLTEXT INDEX ON table_1 START FULL POPULATION;  
    ```  
  
3.  O índice de texto completo é associado posteriormente a uma outra lista de propriedades de pesquisa, `spl_2`, usando a seguinte instrução:  
  
    ```sql  
    ALTER FULLTEXT INDEX ON table_1 SET SEARCH PROPERTY LIST spl_2;  
    ```  
  
     Essa instrução gera uma população completa, o comportamento padrão.  Porém, antes de começar essa população, o Mecanismo de Texto Completo trunca o índice automaticamente.  
  
### <a name="scenario-b-turning-off-the-search-property-list-and-later-associating-the-index-with-any-search-property-list"></a>Cenário B: Desativando a lista de propriedades de pesquisa e depois associando o índice a qualquer lista de propriedades de pesquisa  
  
1.  Um índice de texto completo é criado em `table_1` com uma lista de propriedades de pesquisa `spl_1`, seguido pelo preenchimento completo automático (o comportamento padrão):  
  
    ```sql  
    CREATE FULLTEXT INDEX ON table_1 (column_name) KEY INDEX unique_key_index   
       WITH SEARCH PROPERTY LIST=spl_1;   
    ```  
  
2.  A lista de propriedades de pesquisa é desativada da seguinte maneira:  
  
    ```sql  
    ALTER FULLTEXT INDEX ON table_1   
       SET SEARCH PROPERTY LIST OFF WITH NO POPULATION;   
    ```  
  
3.  O índice de texto completo é associado mais uma vez à mesma lista de propriedades de pesquisa ou a uma lista de propriedades de pesquisa diferente.  
  
     Por exemplo, a seguinte instrução reassocia o índice de texto completo com a lista de propriedades de pesquisa original, `spl_1`:  
  
    ```sql  
    ALTER FULLTEXT INDEX ON table_1 SET SEARCH PROPERTY LIST spl_1;  
    ```  
  
     Essa instrução inicia uma população completa, o comportamento padrão.  
  
    > [!NOTE]  
    >  A recompilação também seria necessária para uma lista de propriedades de pesquisa diferente, como `spl_2`.  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ter a permissão ALTER na exibição de tabela ou indexada, ou ser membro da função de servidor fixa **sysadmin** ou das funções de banco de dados fixas **db_ddladmin** ou **db_owner**.  
  
 Se a opção SET STOPLIST estiver especificada, o usuário deverá ter a permissão REFERENCES na lista de palavras irrelevantes. Se a opção SEARCH PROPERTY LIST estiver especificada, o usuário deverá ter a permissão REFERENCES na lista de propriedades de pesquisa. O proprietário da lista de palavras irrelevantes ou da lista de propriedades de pesquisa especificada pode conceder a permissão REFERENCES, se o proprietário tiver permissões ALTER FULLTEXT CATALOG.  
  
> [!NOTE]  
>  O público recebe a permissão REFERENCES para a lista de palavras irrelevantes padrão fornecida com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-setting-manual-change-tracking"></a>a. Definindo rastreamento manual de alterações  
 O exemplo a seguir define o controle de alterações manual no índice de texto completo na tabela `JobCandidate`.  
  
```sql  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate  
   SET CHANGE_TRACKING MANUAL;  
GO  
```  
  
### <a name="b-associating-a-property-list-with-a-full-text-index"></a>B. Associando uma lista de propriedades a um índice de texto completo  
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.  
  
 O exemplo a seguir associa a lista de propriedades `DocumentPropertyList` ao índice de texto completo na tabela `Production.Document`. Essa instrução ALTER FULLTEXT INDEX inicia uma população completa, que é o comportamento padrão da cláusula SET SEARCH PROPERTY LIST.  
  
> [!NOTE]  
>  Para obter um exemplo que crie uma lista de propriedades `DocumentPropertyList`, veja [CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-search-property-list-transact-sql.md).  
  
```sql  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT INDEX ON Production.Document   
   SET SEARCH PROPERTY LIST DocumentPropertyList;   
GO  
```  
  
### <a name="c-removing-a-search-property-list"></a>C. Removendo uma lista de propriedades de pesquisa  
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.  
  
 O exemplo a seguir remove a lista de propriedades `DocumentPropertyList` do índice de texto completo na tabela `Production.Document`. Neste exemplo, não há pressa para remover as propriedades do índice, de forma que a opção WITH NO POPULATION é especificada. Porém, a pesquisa em nível de propriedade é permitida por mais tempo em relação a esse índice de texto completo.  
  
```sql  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT INDEX ON Production.Document   
   SET SEARCH PROPERTY LIST OFF WITH NO POPULATION;   
GO  
```  
  
### <a name="d-starting-a-full-population"></a>D. Iniciando uma população completa  
 O exemplo a seguir inicia um preenchimento total no índice de texto completo na tabela `JobCandidate`.  
  
```sql  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate   
   START FULL POPULATION;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [Pesquisa de Texto Completo](../../relational-databases/search/full-text-search.md)   
 [Popular índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md)  
  
  
