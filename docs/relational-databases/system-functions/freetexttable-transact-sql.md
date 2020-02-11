---
title: FREETEXTtable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- FREETEXTTABLE_TSQL
- FREETEXTTABLE
dev_langs:
- TSQL
helpviewer_keywords:
- search conditions [SQL Server], meaning matches
- meaning matches [full-text search]
- FREETEXTTABLE function (Transact-SQL)
- ranked results [full-text search]
- column searches [full-text search]
ms.assetid: 4523ae15-4260-40a7-a53c-8df15e1fee79
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4ab1797fabd8fb7d77eab85c97604b77e72f25c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68042765"
---
# <a name="freetexttable-transact-sql"></a>FREETEXTTABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  É uma função usada na [cláusula from](../../t-sql/queries/from-transact-sql.md) de uma [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução SELECT para executar uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pesquisa de texto completo em colunas indexadas de texto completo que contêm tipos de dados baseados em caracteres. Essa função retorna uma tabela de zero, uma ou mais linhas para as colunas que contêm valores que correspondem ao significado e não apenas às palavras exatas do texto no *freetext_string*especificado. FREETEXTTABLE é referenciada como se fosse um nome de tabela comum.  
  
 FREETEXTtable é útil para os mesmos tipos de correspondências que o [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md),  
  
 As consultas que usam FREETEXTTABLE retornam um valor de classificação de relevância (RANK) e uma chave de texto completo (KEY) para cada linha.  
  
> [!NOTE]  
>  Para obter informações sobre os formatos de pesquisas de texto completo compatíveis com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Consulta com a pesquisa de texto completo](../../relational-databases/search/query-with-full-text-search.md).  
  
(https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).|  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FREETEXTTABLE (table , { column_name | (column_list) | * }   
          , 'freetext_string'   
     [ , LANGUAGE language_term ]   
     [ , top_n_by_rank ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *tabela*  
 É o nome da tabela que foi marcada para consulta de texto completo. a *tabela* ou *exibição*pode ser um nome de objeto de banco de dados de um, dois ou três partes. Durante a consulta a uma exibição, apenas uma tabela base indexada por texto completo pode ser envolvida.  
  
 a *tabela* não pode especificar um nome de servidor e não pode ser usada em consultas em servidores vinculados.  
  
 *column_name*  
 É o nome de uma ou mais colunas indexadas de texto completo da tabela especificada na cláusula FROM. As colunas podem ser do tipo **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml**, **varbinary** ou **varbinary(max)**.  
  
 *column_list*  
 Indica que várias colunas, separadas por uma vírgula, podem ser especificadas. *column_list* deve ser colocado entre parênteses. A menos que *language_term* seja especificado, o idioma de todas as colunas da *column_list* precisará ser o mesmo.  
  
 \*  
 Especifica que todas as colunas que forem registradas para pesquisa de texto completo deverão ser usadas para pesquisar a *freetext_string* determinada. A menos que *language_term* seja especificado, o idioma de todas as colunas indexadas de texto completo na tabela deve ser o mesmo.  
  
 *freetext_string*  
 É o texto a ser pesquisado no *column_name*. Qualquer texto, incluindo palavras, frases ou orações, pode ser inserido. Serão geradas correspondências se forem achados termos ou formas de termos no índice de texto completo.  
  
 Diferentemente da condição de pesquisa CONTAINS, onde e é uma palavra-chave, quando usada em *freetext_string* a palavra ' and ' é considerada uma palavra de ruído, ou [palavra irrelevante](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md), e será descartada.  
  
 Não é permitido o uso de WEIGHT, FORMSOF, curingas, NEAR e outra sintaxe. *freetext_string* é wordbroken, originado e passado pelo dicionário de sinônimos.  
  
 LANGUAGE *language_term*  
 É o idioma cujos recursos serão usados para quebra de palavras, lematização e dicionário de sinônimos e remoção de palavras irrelevantes (stop words) como parte da consulta. Esse parâmetro é opcional e pode ser especificado como uma cadeia de caracteres, um inteiro ou um valor hexadecimal que corresponda ao LCID (identificador de localidade) de um idioma. Se *language_term* for especificado, o idioma que ele representa será aplicado a todos os elementos do critério de pesquisa. Se nenhum valor for especificado, o idioma de texto completo da coluna será usado.  
  
 Se documentos de idiomas diferentes forem armazenados em conjunto como BLOBs (objetos binários grandes) em uma única coluna, o LCID de um determinado documento determinará qual idioma será usado para indexar seu conteúdo. Ao consultar uma coluna desse tipo, especificar LANGUAGE *language_term* pode aumentar a probabilidade de uma boa correspondência.  
  
 Quando especificado como uma cadeia de caracteres, *language_term* corresponde ao valor da coluna **alias** no modo de exibição de compatibilidade [sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md).  A cadeia de caracteres precisa ser colocada entre aspas, como em '*language_term*'. Quando especificado como um inteiro, *language_term* é a LCID real que identifica o idioma. Quando especificado como um valor hexadecimal, *language_term* é 0x seguido pelo valor hexadecimal da LCID. O valor hexadecimal não deve exceder oito dígitos, inclusive zeros à esquerda.  
  
 Se o valor estiver no formato DBCS (conjunto de caracteres de dois bytes), o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o converterá em Unicode.  
  
 Se o idioma especificado não for válido ou se não houver nenhum recurso instalado que corresponda ao idioma, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará um erro. Para usar os recursos de idioma neutro, especifique 0x0 como *language_term*.  
  
 *top_n_by_rank*  
 Especifica que somente as *n*maiores correspondências classificadas, em ordem decrescente, são retornadas. Aplica-se somente quando um valor inteiro, *n*, é especificado. Se *top_n_by_rank* for combinado com outros parâmetros, a consulta retornará menos linhas do que o número de linhas que corresponde de fato a todos os predicados. *top_n_by_rank* permite aumentar o desempenho da consulta, rechamando apenas as ocorrências mais relevantes.  
  
## <a name="remarks"></a>Comentários  
 As funções e os predicados de texto completo trabalham em uma única tabela, que está implícita no predicado FROM. Para pesquisar em várias tabelas, use uma tabela unida na cláusula FROM para pesquisar em um conjunto de resultados que é o produto de duas ou mais tabelas.  
  
 FREETEXTTABLE usa as mesmas condições de pesquisa que o predicado FREETEXT.  
  
 Assim como CONTAINSTABLE, a tabela retornada tem colunas nomeadas **Key** e **Rank**, que são referenciadas dentro da consulta para obter as linhas apropriadas e usar os valores de classificação de linha.  
  
## <a name="permissions"></a>Permissões  
 FREETEXTTABLE pode ser invocada apenas por usuários com privilégios SELECT apropriados para a tabela especificada ou as colunas referenciadas da tabela.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-example"></a>a. Exemplo simples  
 O exemplo a seguir cria e popula uma tabela simples de duas colunas, listando 3 contagens e as cores em seus sinalizadores. Ele cria e popula um catálogo de texto completo e um índice na tabela. Em seguida, a sintaxe **FREETEXTTABLE** é demonstrada.  
  
```  
CREATE TABLE Flags (Country nvarchar(30) NOT NULL, FlagColors varchar(200));  
CREATE UNIQUE CLUSTERED INDEX FlagKey ON Flags(Country);  
INSERT Flags VALUES ('France', 'Blue and White and Red');  
INSERT Flags VALUES ('Italy', 'Green and White and Red');  
INSERT Flags VALUES ('Tanzania', 'Green and Yellow and Black and Yellow and Blue');  
SELECT * FROM Flags;  
GO  
  
CREATE FULLTEXT CATALOG TestFTCat;  
CREATE FULLTEXT INDEX ON Flags(FlagColors) KEY INDEX FlagKey ON TestFTCat;  
GO   
  
SELECT * FROM Flags;  
SELECT * FROM FREETEXTTABLE (Flags, FlagColors, 'Blue');  
SELECT * FROM FREETEXTTABLE (Flags, FlagColors, 'Yellow');  
```  
  
### <a name="b-using-freetext-in-an-inner-join"></a>B. Usando FREETEXT em uma INNER JOIN  
 O exemplo a seguir retorna a descrição e a classificação de qualquer produto com uma descrição que corresponda ao `high level of performance`significado de.  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.Description  
    ,KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL   
    INNER JOIN FREETEXTTABLE(Production.ProductDescription,  
    Description,   
    'high level of performance') AS KEY_TBL  
ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY RANK DESC;  
GO  
```  
  
### <a name="c-specifying-language-and-highest-ranked-matches"></a>C. Especificando o idioma e as correspondências de classificação mais alta  
 O exemplo a seguir é idêntico e mostra o uso dos `LANGUAGE`parâmetros *language_term* e *top_n_by_rank* .  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.Description  
    ,KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL   
    INNER JOIN FREETEXTTABLE(Production.ProductDescription,  
    Description,   
    'high level of performance',  
    LANGUAGE N'English', 2) AS KEY_TBL  
ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY RANK DESC;  
GO  
```  
  
> [!NOTE]
>  O parâmetro de *language_term* de idioma não é necessário para usar o parâmetro *top_n_by_rank* .  
  
## <a name="see-also"></a>Consulte Também  
 [Introdução à pesquisa de texto completo](../../relational-databases/search/get-started-with-full-text-search.md)   
 [Criar e gerenciar catálogos de texto completo](../../relational-databases/search/create-and-manage-full-text-catalogs.md)   
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [Criar e gerenciar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [Consulta com pesquisa de texto completo](../../relational-databases/search/query-with-full-text-search.md)   
 [Criar consultas de pesquisa de texto completo &#40;Visual Database Tools&#41;](https://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [Funções de conjunto de linhas &#40;&#41;Transact-SQL](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [Opção de configuração de servidor precompute rank](../../database-engine/configure-windows/precompute-rank-server-configuration-option.md)  
  
  
