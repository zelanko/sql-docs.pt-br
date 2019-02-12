---
title: CREATE XML INDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- XML_TSQL
- CREATE_XML_INDEX_TSQL
- XML INDEX
- CREATE_XML_TSQL
- XML
- CREATE XML
- CREATE XML INDEX
- XML_INDEX_TSQL
- FOR_XML_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE XML INDEX statement
- CREATE INDEX statement
- index creation [SQL Server], XML indexes
- XML indexes [SQL Server], creating
ms.assetid: c510cfbc-68be-4736-b3cc-dc5b7aa51f14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b021451fc0334d931b0321272b23d7ac4100ee3a
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56024957"
---
# <a name="create-xml-index-transact-sql"></a>CREATE XML INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cria um índice XML em uma tabela especificada. Um índice pode ser criado antes que haja dados na tabela. Os índices XML podem ser criados em tabelas em outro banco de dados especificando um nome de banco de dados qualificado.  
  
> [!NOTE]  
>  Para criar um índice relacional, consulte [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md). Para obter informações sobre como criar um índice espacial, consulte [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Create XML Index   
CREATE [ PRIMARY ] XML INDEX index_name   
    ON <object> ( xml_column_name )  
    [ USING XML INDEX xml_index_name   
        [ FOR { VALUE | PATH | PROPERTY } ] ]  
    [ WITH ( <xml_index_option> [ ,...n ] ) ]  
[ ; ]  
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
    table_name  
}  
  
<xml_index_option> ::=  
{   
    PAD_INDEX  = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY = OFF  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
}  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [PRIMARY] XML  
 Cria um índice XML na coluna **xml** especificada. Quando PRIMARY é especificado, um índice clusterizado é criado com a chave clusterizada formada pela chave de cluster da tabela do usuário e um identificador de nó XML. Cada tabela pode ter até 249 índices XML. Observe o seguinte quando for criar um índice XML:  
  
-   Um índice clusterizado deve existir na chave primária da tabela do usuário.  
  
-   A chave de cluster da tabela do usuário é limitada a 15 colunas.  
  
-   Cada coluna **xml** em uma tabela pode ter um índice XML primário e vários índices XML secundários.  
  
-   Deve existir um índice XML primário em uma coluna **xml** antes que um índice XML secundário possa ser criado na coluna.  
  
-   Um índice XML apenas pode ser criado em uma única coluna **xml**. Não é possível criar um índice XML em uma coluna não **xml** nem criar um índice relacional em uma coluna **xml**.  
  
-   Não é possível criar um índice XML, seja primário ou secundário, em uma coluna **xml** em uma exibição, em uma variável com valor de tabela com colunas **xml** ou variáveis do tipo **xml**.  
  
-   Não é possível criar um índice XML primário em uma coluna **xml** computada.  
  
-   As configurações da opção SET devem ser iguais às necessárias para exibições indexadas e índices de coluna computada. Especificamente, a opção ARITHABORT deve ser definida como ON quando um índice XML é criado e ao inserir, excluir ou atualizar valores na coluna **xml**.  
  
 Para obter mais informações, veja [Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md).  
  
 *index_name*  
 É o nome do índice. Os nomes de índice devem ser exclusivos em uma tabela, mas não precisam ser exclusivos em um banco de dados. Os nomes de índice precisam seguir as regras para [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 Nomes de índice XML primários não podem começar com os seguintes caracteres: **#**, **##**, **@** ou **@@**.  
  
 *xml_column_name*  
 É a coluna **xml** na qual o índice se baseia. Somente uma coluna **xml** pode ser especificada em uma única definição de índice XML; no entanto, vários índices XML secundários podem ser criados em uma coluna **xml**.  
  
 USING XML INDEX *xml_index_name*  
 Especifica o índice XML primário a ser usado na criação de um índice XML secundário.  
  
 FOR { VALUE | PATH | PROPERTY }  
 Especifica o tipo de índice XML secundário.  
  
 Value  
 Cria um índice XML secundário em colunas nas quais as colunas de chave são (valor do nó e caminho) do índice XML primário.  
  
 PATH  
 Cria um índice XML secundário em colunas criadas em valores de caminho e de nó no índice XML primário. No índice secundário PATH, os valores de caminho e nó são colunas de chave que permitem buscas eficientes ao pesquisar caminhos.  
  
 PROPERTY  
 Cria um índice XML secundário em colunas (PK, caminho e valor do nó) do índice XML primário em que PK é a chave primária da tabela base.  
  
 **\<object>::=**  
  
 É o objeto totalmente qualificado ou não totalmente qualificado a ser indexado.  
  
 *database_name*  
 É o nome do banco de dados.  
  
 *schema_name*  
 É o nome do esquema ao qual a tabela pertence.  
  
 *table_name*  
 É o nome da tabela a ser indexada.  
  
 **\<xml_index_option> ::=** 
  
 Especifica as opções a serem usadas ao criar o índice.  
  
 PAD_INDEX **=** { ON | **OFF** }  
 Especifica o preenchimento do índice. O padrão é OFF.  
  
 ON  
 O percentual de espaço livre especificado por *fillfactor* é aplicado às páginas de nível intermediário do índice.  
  
 OFF ou *fillfactor* não está especificado  
 As páginas de nível intermediário são preenchidas até próximo de sua capacidade, deixando espaço suficiente para pelo menos uma linha do tamanho máximo que o índice pode ter, considerando o conjunto de chaves em páginas intermediárias.  
  
 A opção PAD_INDEX só é útil quando FILLFACTOR é especificado, porque PAD_INDEX usa a porcentagem especificada por FILLFACTOR. Se a porcentagem especificada para FILLFACTOR não for grande o suficiente para permitir uma linha, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] substituirá a porcentagem internamente para permitir o valor mínimo. O número de linhas em uma página de índice intermediária nunca é menor do que dois, independentemente de quão baixo seja o valor de *fillfactor*.  
  
 FILLFACTOR **=**_fillfactor_  
 Especifica uma porcentagem que indica quanto o [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve preencher o nível folha de cada página de índice durante a criação ou recriação do índice. *fillfactor* deve ser um valor inteiro de 1 a 100. O padrão é 0. Se *fillfactor* for 100 ou 0, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] criará índices com páginas folha preenchidas até a capacidade máxima.  
  
> [!NOTE]  
>  Os valores de fator de preenchimento 0 e 100 são iguais em todos os aspectos.  
  
 A configuração FILLFACTOR se aplica somente quando o índice é criado ou recriado. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] não mantém dinamicamente a porcentagem especificada de espaço vazio nas páginas. Para exibir a configuração do fator de preenchimento, use a exibição do catálogo [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
> [!IMPORTANT]  
>  A criação de um índice clusterizado com FILLFACTOR inferior a 100 afeta a quantidade de espaço de armazenamento ocupado pelos dados, porque o [!INCLUDE[ssDE](../../includes/ssde-md.md)] redistribui os dados quando cria o índice clusterizado.  
  
 Para obter mais informações, veja [Especificar fator de preenchimento para um índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).  
  
 SORT_IN_TEMPDB **=** { ON | **OFF** }  
 Especifica se os resultados de classificação temporários devem ser armazenados no **tempdb**. O padrão é OFF.  
  
 ON  
 Os resultados de classificação intermediários usados para criar o índice são armazenados no **tempdb**. Isso poderá reduzir o tempo necessário para criar um índice se **tempdb** estiver em um conjunto de discos diferente do banco de dados de usuário. Entretanto, isso aumenta o espaço em disco usado durante a criação do índice.  
  
 OFF  
 Os resultados intermediários de classificação são armazenados no mesmo banco de dados que o índice.  
  
 Além do espaço necessário no banco de dados de usuário para criar o índice, **tempdb** deve ter aproximadamente a mesma quantidade de espaço adicional para conter os resultados de classificação intermediários. Para obter mais informações, consulte a [Opção SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md).  
  
 IGNORE_DUP_KEY **=OFF**  
 Não tem nenhum efeito para índices XML porque o tipo de índice nunca é exclusivo. Não defina essa opção como ON; caso contrário, um erro será gerado.  
  
 DROP_EXISTING **=** { ON | **OFF** }  
 Especifica que o índice XML nomeado preexistente deve ser removido e recriado. O padrão é OFF.  
  
 ON  
 O índice existente é removido e recriado. O nome de índice especificado deve ser igual ao índice existente atualmente; no entanto, a definição de índice pode ser modificada. Por exemplo, você pode especificar colunas, ordens de classificação, esquemas de partição ou opções de índice diferentes.  
  
 OFF  
 Um erro será exibido se o nome de índice especificado já existir.  
  
 O tipo de índice não pode ser alterado com DROP_EXISTING. Além disso, um índice XML primário não pode ser redefinido como um índice XML secundário ou vice-versa.  
  
 ONLINE **=OFF**  
 Especifica que as tabelas subjacentes e os índices associados não estão disponíveis para consultas e modificação de dados durante a operação de índice. Nesta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], não há suporte para criações de índice online para índices XML. Se essa opção for definida como ON para um índice XML, um erro será gerado. Omita a opção ONLINE ou defina ONLINE como OFF.  
  
 Uma operação de índice offline que cria, recria ou remove um índice XML adquire um bloqueio de Modificação de esquema (Sch-M) na tabela. Isso evita o acesso de todos os usuários à tabela subjacente enquanto durar a operação.  
  
> [!NOTE]
>  As operações de índice online não estão disponíveis em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Edições e recursos com suporte no SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ALLOW_ROW_LOCKS **=** { **ON** | OFF }  
 Especifica se bloqueios de linha são permitidos. O padrão é ON.  
  
 ON  
 Bloqueios de linha são permitidos ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de linha são usados.  
  
 OFF  
 Bloqueios de linha não são usados.  
  
 ALLOW_PAGE_LOCKS **=** { **ON** | OFF }  
 Especifica se bloqueios de página são permitidos. O padrão é ON.  
  
 ON  
 Bloqueios de página são permitidos ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de página são usados.  
  
 OFF  
 Bloqueios de página não são usados.  
  
 MAXDOP **=**_max_degree_of_parallelism_  
 Substitui a opção de configuração [Configurar a opção max degree of parallelism de configuração do servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) durante a operação de índice. Use MAXDOP para limitar o número de processadores usados em uma execução de plano paralelo. O máximo é de 64 processadores.  
  
> [!IMPORTANT]  
>  Embora a opção MAXDOP tenha suporte sintaticamente para todos os índices XML, para um índice XML primário, CREATE XML INDEX usa apenas um único processador.  
  
 *max_degree_of_parallelism* pode ser:  
  
 1  
 Suprime a geração de plano paralelo.  
  
 \>1  
 Restringe o número máximo de processadores usados em uma operação de índice paralela ao número especificado, ou menos, com base na carga de trabalho atual do sistema.  
  
 0 (padrão)  
 Usa o número real de processadores, ou menos, com base na carga de trabalho atual do sistema.  
  
 Para obter mais informações, consulte [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]
>  As operações de índice paralelas não estão disponíveis em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Edições e recursos com suporte no SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
## <a name="remarks"></a>Remarks  
 As colunas computadas derivadas de tipos de dados **xml** podem ser indexadas como uma coluna de chave ou como uma coluna não chave incluída, desde que o tipo de dados da coluna computada seja permitido como uma coluna de chave de índice ou coluna não chave. Não é possível criar um índice XML primário em uma coluna **xml** computada.  
  
 Para exibir informações sobre índices XML, use a exibição do catálogo [sys.xml_indexes](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md).  
  
 Para obter mais informações sobre índices XML, consulte [Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md).  
  
## <a name="additional-remarks-on-index-creation"></a>Comentários adicionais sobre criação de índices  
 Para obter mais informações sobre a criação de índices, consulte a seção “Comentários” em [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-primary-xml-index"></a>A. Criando um índice XML primário  
 O exemplo a seguir cria um índice XML primário na coluna `CatalogDescription` da tabela `Production.ProductModel`.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT * FROM sys.indexes  
            WHERE name = N'PXML_ProductModel_CatalogDescription')  
    DROP INDEX PXML_ProductModel_CatalogDescription   
        ON Production.ProductModel;  
GO  
CREATE PRIMARY XML INDEX PXML_ProductModel_CatalogDescription  
    ON Production.ProductModel (CatalogDescription);  
GO  
```  
  
### <a name="b-creating-a-secondary-xml-index"></a>b. Criando um índice XML secundário  
 O exemplo a seguir cria um índice XML secundário na coluna `CatalogDescription` da tabela `Production.ProductModel`.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.indexes  
            WHERE name = N'IXML_ProductModel_CatalogDescription_Path')  
    DROP INDEX IXML_ProductModel_CatalogDescription_Path  
        ON Production.ProductModel;  
GO  
CREATE XML INDEX IXML_ProductModel_CatalogDescription_Path   
    ON Production.ProductModel (CatalogDescription)  
    USING XML INDEX PXML_ProductModel_CatalogDescription FOR PATH ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.xml_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)  
  
  

