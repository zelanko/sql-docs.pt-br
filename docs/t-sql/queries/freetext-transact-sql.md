---
title: FREETEXT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FREETEXT
- FREETEXT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], meaning matches
- meaning matches [full-text search]
- FREETEXT predicate (Transact-SQL)
- words in predicate [full-text search]
- column searches [full-text search]
ms.assetid: 2f199d3c-440e-4bcf-bdb5-82bb3994005d
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: d9df7c71608bef12b5da2a4be987031900ab8af5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62467007"
---
# <a name="freetext-transact-sql"></a>FREETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  É um predicado usado na [cláusula WHERE](../../t-sql/queries/where-transact-sql.md) de [!INCLUDE[tsql](../../includes/tsql-md.md)] de uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT para executar uma pesquisa de texto completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma coluna indexada para texto completo que contenha caracteres de tipos de dados baseados em caracteres. Esse predicado procura valores correspondentes ao significado e não apenas o teor exato das palavras nos critérios da pesquisa. Quando FREETEXT é usado, o mecanismo de consulta de texto completo executa internamente as ações a seguir na *freetext_string*, atribui um peso a cada termo e, em seguida, localiza as correspondências:  
  
-   Separa a cadeia de caracteres em palavras individuais com base em limites de palavra (quebra de palavras).  
  
-   Gera formas flexivas das palavras (ramificações).  
  
-   Identifica uma lista de expansões ou substituições dos termos baseados em correspondências no dicionário de sinônimos.  
  
> [!NOTE]  
>  Para obter informações sobre os formatos de pesquisas de texto completo compatíveis com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Consulta com a pesquisa de texto completo](../../relational-databases/search/query-with-full-text-search.md).  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FREETEXT ( { column_name | (column_list) | * }   
          , 'freetext_string' [ , LANGUAGE language_term ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *column_name*  
 É o nome de uma ou mais colunas indexadas de texto completo da tabela especificada na cláusula FROM. As colunas podem ser do tipo **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml**, **varbinary** ou **varbinary(max)** .  
  
 *column_list*  
 Indica que várias colunas, separadas por uma vírgula, podem ser especificadas. *column_list* precisa ser colocada entre parênteses. A menos que *language_term* seja especificado, o idioma de todas as colunas da *column_list* precisará ser o mesmo.  
  
 \*  
 Especifica que todas as colunas que forem registradas para pesquisa de texto completo deverão ser usadas para pesquisar a *freetext_string* determinada. Se houver mais de uma tabela na cláusula FROM, \* precisará ser qualificado pelo nome da tabela. A menos que *language_term* seja especificado, o idioma de todas as colunas da tabela precisará ser o mesmo.  
  
 *freetext_string*  
 É o texto a ser pesquisado no *column_name*. Qualquer texto, incluindo palavras, frases ou orações, pode ser inserido. Serão geradas correspondências se forem achados termos ou formas de termos no índice de texto completo.  
  
 Ao contrário do critério de pesquisa CONTAINS e CONTAINSTABLE, em que AND é uma palavra-chave, quando usada em *freetext_string* a palavra 'and' será considerada uma palavra de ruído ou [palavra irrelevante (stop word)](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md) e será descartada.  
  
 Não é permitido o uso de WEIGHT, FORMSOF, curingas, NEAR e outra sintaxe. *freetext_string* é uma palavra quebrada, não flexionada e passada pelo dicionário de sinônimos.  
  
 *freetext_string* é **nvarchar**. Uma conversão implícita acontece quando outro tipo de dados de caractere é usado como entrada. Os tipos de dados de cadeia de caracteres grande nvarchar(max) e varchar(max) não podem ser usados. No exemplo a seguir, a variável `@SearchWord`, que está definida como `varchar(30)`, causa uma conversão implícita no predicado `FREETEXT`.  
  
```sql  
  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord varchar(30)  
SET @SearchWord ='performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE FREETEXT(Description, @SearchWord);  
  
```  
  
 Como a "detecção de parâmetro" não funciona na conversão, use **nvarchar** para melhorar o desempenho. No exemplo, declare `@SearchWord` como `nvarchar(30)`.  
  
```sql  
  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord nvarchar(30)  
SET @SearchWord = N'performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE FREETEXT(Description, @SearchWord);  
  
```  
  
 Você também pode usar a dica de consulta OPTIMIZE FOR para casos em que um plano não ideal é gerado.  
  
 LANGUAGE *language_term*  
 É o idioma cujos recursos serão usados para quebra de palavras, lematização e dicionário de sinônimos e remoção de palavras irrelevantes (stop words) como parte da consulta. Esse parâmetro é opcional e pode ser especificado como uma cadeia de caracteres, um inteiro ou um valor hexadecimal que corresponda ao LCID (identificador de localidade) de um idioma. Se *language_term* for especificado, o idioma que ele representa será aplicado a todos os elementos do critério de pesquisa. Se nenhum valor for especificado, o idioma de texto completo da coluna será usado.  
  
 Se documentos de idiomas diferentes forem armazenados em conjunto como BLOBs (objetos binários grandes) em uma única coluna, o LCID de um determinado documento determinará qual idioma será usado para indexar seu conteúdo. Ao consultar uma coluna desse tipo, especificar LANGUAGE *language_term* pode aumentar a probabilidade de uma boa correspondência.  
  
 Quando especificado como uma cadeia de caracteres, *language_term* corresponde ao valor da coluna **alias** na exibição de compatibilidade [sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md).  A cadeia de caracteres precisa ser colocada entre aspas, como em '*language_term*'. Quando especificado como um inteiro, *language_term* é a LCID real que identifica o idioma. Quando especificado como um valor hexadecimal, *language_term* é 0x seguido pelo valor hexadecimal da LCID. O valor hexadecimal não deve exceder oito dígitos, inclusive zeros à esquerda.  
  
 Se o valor estiver no formato DBCS (conjunto de caracteres de byte duplo), [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o converterá em Unicode.  
  
 Se o idioma especificado não for válido ou se não houver nenhum recurso instalado que corresponda a esse idioma, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará um erro. Para usar os recursos de idioma neutro, especifique 0x0 como *language_term*.  
  
## <a name="general-remarks"></a>Comentários gerais  
 As funções e os predicados de texto completo trabalham em uma única tabela, que está implícita no predicado FROM. Para pesquisar em várias tabelas, use uma tabela unida na cláusula FROM para pesquisar em um conjunto de resultados que é o produto de duas ou mais tabelas.  
  
Consultas de texto completo que usam FREETEXT são menos precisas que consultas de texto completo que usam CONTAINS. O mecanismo de pesquisa de texto completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identifica palavras e frases importantes. Nenhum significado especial é dado a nenhuma das palavra-chave reservadas ou dos caracteres curingas que geralmente têm um significado quando são especificados no parâmetro \<contains_search_condition> do predicado CONTAINS.
  
 Predicados de texto completo não são permitidos na [cláusula OUTPUT](../../t-sql/queries/output-clause-transact-sql.md) quando o nível de compatibilidade do banco de dados é definido como 100.  
  
> [!NOTE]  
>  A função FREETEXTTABLE é útil para os mesmos tipos de correspondência que o predicado FREETEXT. É possível referenciar essa função como um nome de tabela normal na [cláusula FROM](../../t-sql/queries/from-transact-sql.md) de uma instrução SELECT. Para obter mais informações, confira [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md).  
  
## <a name="querying-remote-servers"></a>Consultando servidores remotos  
 É possível usar um nome de quatro partes no predicado [CONTAINS](../../t-sql/queries/contains-transact-sql.md) ou FREETEXT para consultar colunas indexadas de texto completo das tabelas de destino em um servidor vinculado. Para preparar um servidor remoto para receber consultas de texto completo, crie um índice de texto completo nas tabelas e colunas de destino no servidor remoto e, em seguida, adicione o servidor remoto como um servidor vinculado.  
  
## <a name="comparison-of-like-to-full-text-search"></a>Comparação entre LIKE e a pesquisa de texto completo  
 Ao contrário da pesquisa de texto completo, o predicado [LIKE](../../t-sql/language-elements/like-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] funciona apenas em padrões de caracteres. Além disso, não é possível usar o predicado LIKE para consultar dados binários formatados. Além disso, uma consulta LIKE feita em uma grande quantidade de dados de texto não estruturados é bem mais lenta do que uma consulta de texto completo equivalente feita nos mesmos dados. Uma consulta LIKE executada em milhões de linhas de dados de texto pode demorar muitos minutos, enquanto uma consulta de texto completo pode demorar alguns segundos ou menos para ser executada nos mesmos dados, dependendo do número de linhas retornadas.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-freetext-to-search-for-words-containing-specified-character-values"></a>A. Usando FREETEXT para pesquisar palavras que contêm valores de caracteres especificados  
 As pesquisas de exemplo a seguir para todos os documentos que contêm as palavras relacionadas a componentes vitais, de segurança.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Title  
FROM Production.Document  
WHERE FREETEXT (Document, 'vital safety components' );  
GO  
```  
  
### <a name="b-using-freetext-with-variables"></a>B. Usando FREETEXT com variáveis  
 O exemplo a seguir usa uma variável em vez de um termo de pesquisa específico.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord nvarchar(30);  
SET @SearchWord = N'high-performance';  
SELECT Description   
FROM Production.ProductDescription   
WHERE FREETEXT(Description, @SearchWord);  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar a pesquisa de texto completo](../../relational-databases/search/get-started-with-full-text-search.md)   
 [Criar e gerenciar catálogos de texto completo](../../relational-databases/search/create-and-manage-full-text-catalogs.md)   
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [Criar e gerenciar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [Consulta com pesquisa de texto completo](../../relational-databases/search/query-with-full-text-search.md)   
 [Criar consultas de pesquisa de texto completo &#40;Visual Database Tools&#41;](https://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
