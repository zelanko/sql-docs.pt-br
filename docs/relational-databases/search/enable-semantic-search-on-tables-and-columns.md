---
title: Habilitar a pesquisa semântica em tabelas e colunas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], enabling
ms.assetid: 895d220c-6749-4954-9dd3-2ea4c6a321ff
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c046bbc7ac0b1da4c4e3be7c1eef0d7d47ccf9ec
ms.sourcegitcommit: fc6a6eedcea2d98c93e33d39c1cecd99fbc9a155
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49169307"
---
# <a name="enable-semantic-search-on-tables-and-columns"></a>Habilitar a pesquisa semântica em tabelas e colunas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Descreve como habilitar ou desabilitar a indexação semântica estatística em colunas selecionadas que contêm documentos ou texto.  
  
 A pesquisa semântica estatística usa os índices que são criados pela Pesquisa de Texto Completo e cria índices adicionais. Como resultado dessa dependência na pesquisa de texto completo, você cria um novo índice semântico ao definir um novo índice de texto completo ou ao alterar um índice de texto completo existente. Você pode criar um novo índice semântico usando instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] , ou usando o Assistente para Indexação de Texto Completo e outras caixas de diálogo no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conforme descrito neste tópico.  
  
##  <a name="BasicEnabling"></a> Criar um índice semântico  
  
###  <a name="reqenable"></a> Requisitos e restrições para criar um índice semântico  
  
-   Você pode criar um índice em qualquer um dos objetos de banco de dados com suporte para indexação de texto completo, inclusive tabelas e exibições indexadas.  
  
-   Antes de habilitar a indexação semântica para colunas específicas, verifique se existem os seguintes pré-requisitos:  
  
    -   Um catálogo de texto completo deve existir para o banco de dados.  
  
    -   A tabela deve ter um índice de texto completo.  
  
    -   As colunas selecionadas devem participar do índice de texto completo.  
  
     É possível criar e habilitar todos esses requisitos ao mesmo tempo.  
  
-   Você pode criar um índice semântico em colunas que tenham qualquer um dos tipos de dados com suporte para indexação de texto completo. Para obter mais informações, veja [Criar e gerenciar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md).  
  
-   Você pode especificar qualquer tipo de documento com suporte para indexação de texto completo para colunas **varbinary(max)** . Para obter mais informações, consulte [Como determinar os tipos de documento que podem ser indexados](#doctypes) neste tópico.  
  
-   A indexação semântica cria dois tipos de índices para as colunas que você seleciona – um índice de frases-chave e um índice de similaridade de documento. Você não pode selecionar somente um tipo de índice ou o outro quando habilita a indexação semântica. Entretanto, você pode consultar esses dois índices separadamente. Para obter mais informações, veja [Localizar frases-chave em documentos com a pesquisa semântica](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md) e [Localizar documentos semelhantes e relacionados com a pesquisa semântica](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md).  
  
-   Se você não especificar explicitamente um LCID para um índice semântico, somente o idioma principal e suas estatísticas de idioma associadas serão usados para a indexação semântica.  
  
-   Se você criar um idioma para uma coluna para a qual o modelo de idioma não está disponível, a criação do índice falhará e retornará uma mensagem de erro.  
  
##  <a name="HowToEnableCreate"></a> Criar um índice semântico quando não existe índice de texto completo  
 Quando você criar um novo índice de texto completo com a instrução **CREATE FULLTEXT INDEX** , poderá habilitar a indexação semântica no nível de coluna especificando a palavra-chave **STATISTICAL_SEMANTICS** como parte da definição de coluna. Você também poderá habilitar a indexação semântica ao usar o Assistente para Indexação de Texto Completo para criar um novo índice de texto completo.  
  
 ### <a name="create-a-new-semantic-index-by-using-transact-sql"></a>Criar um novo índice semântico usando Transact-SQL  
 
 Chame a instrução **CREATE FULLTEXT INDEX** e especifique **STATISTICAL_SEMANTICS** para cada coluna na qual você queira criar um índice semântico. Para obter mais informações sobre todas as opções para esta instrução, veja [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md).  
  
 **Exemplo 1: criar um índice exclusivo, um índice de texto completo e um índice semântico**  
  
 O exemplo a seguir cria um catálogo de texto completo padrão, **ft**. O exemplo cria um índice exclusivo na coluna **JobCandidateID** da tabela **HumanResources.JobCandidate** do banco de dados de exemplo AdventureWorks2012. Este índice exclusivo é necessário como a coluna de chave de um índice de texto completo. O exemplo cria um índice de texto completo um índice semântico na coluna **Retomar** .  
  
```sql  
CREATE FULLTEXT CATALOG ft AS DEFAULT  
GO  
  
CREATE UNIQUE INDEX ui_ukJobCand  
    ON HumanResources.JobCandidate(JobCandidateID)  
GO  
  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate  
    (Resume  
        Language 1033  
        Statistical_Semantics  
    )   
    KEY INDEX JobCandidateID   
    WITH STOPLIST = SYSTEM  
GO  
```  
  
 **Exemplo 2: criar um índice de texto completo e um índice semântico em várias colunas com população de índice atrasada**  
  
 O exemplo a seguir cria um catálogo de texto completo, **documents_catalog**, no banco de dados de exemplo AdventureWorks2012. Em seguida, o exemplo cria um índice de texto completo que usa esse novo catálogo. O índice de texto completo criado nas colunas **Title**, **DocumentSummary**e **Document** da tabela **Production.Document** , enquanto o índice semântico está apenas na coluna **Document** . Esse índice de texto completo usa o catálogo de texto completo padrão e um índice de chave exclusiva existente, **PK_Document_DocumentID**. Conforme recomendado, essa chave de índice é criada em uma coluna de inteiros, **DocumentID**. O exemplo especifica o LCID para inglês, 1033, que é o idioma dos dados nas colunas.  
  
 Este exemplo também especifica que o controle de alterações está desativado sem nenhuma população. Posteriormente, fora do horário de pico, o exemplo usa uma instrução **ALTER FULLTEXT INDEX** para iniciar uma população completa no novo índice e habilitar o controle de alterações automático.  
  
```sql  
CREATE FULLTEXT CATALOG documents_catalog  
GO  
  
CREATE FULLTEXT INDEX ON Production.Document  
    (   
    Title  
        Language 1033,   
    DocumentSummary  
        Language 1033,   
    Document   
        TYPE COLUMN FileExtension  
        Language 1033  
        Statistical_Semantics  
    )  
    KEY INDEX PK_Document_DocumentID  
        ON documents_catalog  
        WITH CHANGE_TRACKING OFF, NO POPULATION  
GO  
```  
  
 Posteriormente, fora do horário de pico, o índice é populado:  
  
```sql  
ALTER FULLTEXT INDEX ON Production.Document SET CHANGE_TRACKING AUTO  
GO  
```  
  
### <a name="create-a-new-semantic-index-by-using-sql-server-management-studio"></a>Criar um novo índice semântico usando o SQL Server Management Studio  
 Execute o Assistente para Indexação de Texto Completo e habilite **Semântica Estatística** na página **Selecionar Colunas da Tabela** para cada coluna na qual você queira criar um índice semântico. Para obter mais informações, inclusive sobre como iniciar o Assistente de Indexação de Texto Completo, veja [Usar o Assistente de Indexação de Texto Completo](../../relational-databases/search/use-the-full-text-indexing-wizard.md).  
  
##  <a name="HowToEnableAlter"></a> Criar um índice semântico quando existe um índice de texto completo  
 Você pode adicionar a indexação semântica ao alterar um índice de texto completo existente com a instrução **ALTER FULLTEXT INDEX** . Você também pode adicionar indexação semântica usando várias caixas de diálogo no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
### <a name="add-a-semantic-index-by-using-transact-sql"></a>Adicionar um novo índice semântico usando Transact-SQL  
 Chame a instrução **ALTER FULLTEXT INDEX** com as opções descritas abaixo para cada coluna na qual você queira adicionar um índice semântico. Para obter mais informações sobre todas as opções para esta instrução, veja [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md).  
  
 Os índices de texto completo e semântico são ambos repopulados após uma chamada a **ALTER**, a menos que você especifique de outra forma.  
  
-   Para adicionar somente a indexação de texto completo a uma coluna, use a sintaxe **ADD** .  
  
-   Para adicionar indexação de texto completo e semântica a uma coluna, use a sintaxe **ADD** com a opção **STATISTICAL_SEMANTICS** .  
  
-   Para adicionar indexação de texto completo a uma coluna já habilitada para indexação de texto completo, use a opção **ADD STATISTICAL_SEMANTICS** . Você só pode adicionar indexação semântica a uma coluna em uma única instrução **ALTER** .  
  
 **Exemplo: adicionar a indexação semântica a uma coluna que já tenha a indexação de texto completo**  
  
 O exemplo a seguir altera um índice de texto completo existente na tabela **Production.Document** no banco de dados de exemplo AdventureWorks2012. O exemplo adiciona um índice semântico na coluna **Document** da tabela **Production.Document** , que já tem um índice de texto completo. O exemplo especifica que o índice não será repopulado automaticamente.  
  
```sql  
ALTER FULLTEXT INDEX ON Production.Document  
    ALTER COLUMN Document  
        ADD Statistical_Semantics  
    WITH NO POPULATION  
GO  
```  
  
### <a name="add-a-semantic-index-by-using-sql-server-management-studio"></a>Adicionar um índice semântico usando o SQL Server Management Studio  
 Você pode alterar as colunas que são habilitadas para indexação semântica e de texto completo na página **Colunas de Índice de Texto Completo** da caixa de diálogo **Propriedades do Índice de Texto Completo** . Para obter mais informações, veja [Gerenciar índices de texto completo](http://msdn.microsoft.com/library/28ff17dc-172b-4ac4-853f-990b5dc02fd1).  

## <a name="alter-a-semantic-index"></a>Alterar um índice semântico
  
###  <a name="addreq"></a> Requisitos e restrições para alterar um índice existente  
  
-   Você não pode alterar um índice existente enquanto a população do índice está em andamento. Para obter mais informações sobre como monitorar o progresso da população de índice, veja [Gerenciar e monitorar a pesquisa semântica](../../relational-databases/search/manage-and-monitor-semantic-search.md).  
  
-   Você não pode adicionar indexação a uma coluna, nem alterar ou remover a indexação para a mesma coluna, em uma única chamada à instrução **ALTER FULLTEXT INDEX** .  
  
##  <a name="dropping"></a> Remover um índice semântico  
Você pode remover a indexação semântica ao alterar um índice de texto completo existente com a instrução **ALTER FULLTEXT INDEX** . Você também pode descartar a indexação semântica usando várias caixas de diálogo no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 ### <a name="drop-a-semantic-index-by-using-transact-sql"></a>Descartar um novo índice semântico usando Transact-SQL  
Para remover apenas a indexação semântica de uma ou mais colunas, chame a instrução **ALTER FULLTEXT INDEX** com a opção **ALTER COLUMN**_nome_da\_coluna_**DROP STATISTICAL_SEMANTICS**. Você pode remover a indexação de várias colunas em uma única instrução **ALTER** .  
  
```sql  
USE database_name  
GO  

ALTER FULLTEXT INDEX  
    ALTER COLUMN column_name  
    DROP STATISTICAL_SEMANTICS  
GO  
```  
  
Para remover a indexação semântica e de texto completo de uma coluna, chame a instrução **ALTER FULLTEXT INDEX** com a opção **ALTER COLUMN**_nome_da\_coluna_**DROP**.  
  
```sql  
USE database_name  
GO  
  
ALTER FULLTEXT INDEX  
    ALTER COLUMN column_name  
    DROP  
GO  
```  
  
 ### <a name="drop-a-semantic-index-by-using-sql-server-management-studio"></a>Descartar um índice semântico usando o SQL Server Management Studio  
 Você pode alterar as colunas que são habilitadas para indexação semântica e de texto completo na página **Colunas de Índice de Texto Completo** da caixa de diálogo **Propriedades do Índice de Texto Completo** . Para obter mais informações, veja [Gerenciar índices de texto completo](http://msdn.microsoft.com/library/28ff17dc-172b-4ac4-853f-990b5dc02fd1).  
  
###  <a name="dropreq"></a> Requirements and restrictions for dropping a semantic index  
  
-   Você não pode remover a indexação de texto completo de uma coluna enquanto retém a indexação semântica. A indexação semântica depende da indexação de texto completo para resultados de similaridade de documento.  
  
-   Você não pode especificar a opção **NO POPULATION** ao remover a indexação semântica da última coluna de uma tabela para a qual a indexação semântica foi habilitada. Um ciclo de população é necessário para remover os resultados que foram previamente indexados.  
  
## <a name="check-whether-semantic-search-is-enabled-on-database-objects"></a>Verificar se a pesquisa semântica está habilitada em objetos de banco de dados  
### <a name="is-semantic-search-enabled-for-a-database"></a>A pesquisa semântica está habilitada para um banco de dados?
  
 Consulte a propriedade **IsFullTextEnabled** da função de metadados [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md).  
  
 Um valor de retorno 1 indica a pesquisa de texto completo e a pesquisa semântica estão habilitada para o banco de dados; um valor de retorno 0 indica que não são habilitadas.  
  
```sql  
SELECT DATABASEPROPERTYEX('database_name', 'IsFullTextEnabled')  
GO  
```  
  
### <a name="is-semantic-search-enabled-for-a-table"></a>A pesquisa semântica está habilitada para uma tabela?  
 
 Consulte a propriedade **TableFullTextSemanticExtraction** na função de metadados [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md).  
  
 Um valor de retorno 1 indica a pesquisa semântica está habilitada para a tabela; um valor de retorno 0 indica que ela não está habilitada.  
  
```scr  
SELECT OBJECTPROPERTYEX(OBJECT_ID('table_name'), 'TableFullTextSemanticExtraction')  
GO  
```  
  
 ### <a name="is-semantic-search-enabled-for-a-column"></a>A pesquisa semântica está habilitada para uma coluna?
   
 Para determinar se a pesquisa de semântica está habilitada para uma coluna específica:  
  
-   Consulte a propriedade **StatisticalSemantics** da função de metadados [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md).  
  
     Um valor de retorno 1 indica a pesquisa semântica está habilitada para a coluna; um valor de retorno 0 indica que ela não está habilitada.  
  
    ```sql  
    SELECT COLUMNPROPERTY(OBJECT_ID('table_name'), 'column_name', 'StatisticalSemantics')  
    GO  
    ```  
  
-   Consulte a exibição de catálogo [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md) para obter o índice de texto completo.  
  
     Um valor 1 na coluna **statistical_semantics** indica que a coluna especificada está habilitada para a indexação semântica, além da indexação de texto completo.  
  
    ```sql  
    SELECT * FROM sys.fulltext_index_columns WHERE object_id = OBJECT_ID('table_name')  
    GO  
    ```  
  
-   No Pesquisador de Objetos no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], clique com o botão direito do mouse em uma coluna e selecione **Propriedades**. Na página **Geral** da caixa de diálogo **Propriedades da Coluna** , verifique o valor da propriedade **Semântica Estatística** .  
  
     Um valor True indica que a coluna especificada está habilitada para a indexação semântica, além da indexação de texto completo.  
  
## <a name="determine-what-can-be-indexed-for-semantic-search"></a>Determinar o que pode ser indexado para Pesquisa Semântica  
  
###  <a name="HowToCheckLanguages"></a> Verificar os idiomas com suporte para a pesquisa semântica  
  
> [!IMPORTANT]  
>  Há suporte para menos idiomas na indexação semântica do que na indexação de texto completo. Como resultado, pode haver colunas que permitam a indexação para pesquisa de texto completo, mas não para pesquisa semântica.  
  
 Consulte a exibição de catálogo [sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md).  
  
```sql  
SELECT * FROM sys.fulltext_semantic_languages  
GO  
```  
  
 Há suporte para os seguintes idiomas na indexação semântica. Esta lista representa a saída da exibição de catálogo [sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md), ordenada por LCID.  
  
|Linguagem|LCID|  
|--------------|----------|  
|German|1031|  
|Inglês (EUA)|1046|  
|Francês|1036|  
|Italiano|1040|  
|Português (Brasil)|1046|  
|Russo|1049|  
|Sueco|1053|  
|Inglês (Reino Unido)|2057|  
|Português (Portugal)|2070|  
|Espanhol|3082|  
  
###  <a name="doctypes"></a> Determinar os tipos de documento que podem ser indexados  
 Consulte a exibição de catálogo [sys.fulltext_document_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md).  
  
 Se o tipo de documento que você deseja indexar não estiver na lista de tipos com suporte, talvez seja preciso localizar, baixar e instalar filtros adicionais. Para obter mais informações, consulte [Exibir ou alterar filtros registrados e separadores de palavras](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md).  
  
##  <a name="BestPracticeFilegroup"></a> Prática recomendada: considerar a criação de um grupo de arquivos separado para os índices de texto completo e semânticos  
 Considere criar um grupo de arquivos separado para os índices de texto completo e semântico se a alocação de espaço em disco for um problema. Os índices semânticos são criados no mesmo grupo de arquivos que o índice de texto completo. Um índice semântico totalmente populado pode conter uma grande quantidade de dados.  
 
##  <a name="IssueNoResults"></a> Problema: a pesquisa em coluna específica não retorna resultados  
 **Um LCID não Unicode foi especificado para um idioma Unicode?**  
 É possível habilitar a indexação semântica em um tipo de coluna não Unicode com um LCID para um idioma que tenha apenas palavras Unicode, como o LCID 1049 para russo. Neste caso, nenhum resultado será retornado dos índices semânticos nesta coluna.  
  
  
