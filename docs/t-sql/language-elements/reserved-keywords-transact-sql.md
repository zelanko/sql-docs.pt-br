---
title: Palavras-chave (Transact-SQL) reservadas | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- ODBC function calls
- keywords [SQL Server], reserved
- reserved words [SQL Server]
- keywords [SQL Server]
ms.assetid: ed8b3e27-6796-40f0-aef3-0cac5e0e2418
caps.latest.revision: "53"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: f2a3e554a7a3b46242c44c38137609322e6d89f4
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="reserved-keywords-transact-sql"></a>Palavras-chave reservadas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa palavras-chave reservadas para definir, manipular e acessar bancos de dados. As palavras-chave reservadas fazem parte da gramática da linguagem [!INCLUDE[tsql](../../includes/tsql-md.md)] usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para analisar e compreender as instruções e os lotes [!INCLUDE[tsql](../../includes/tsql-md.md)]. Embora seja sintaticamente possível usar as palavras-chave reservadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como identificadores e nomes de objeto em scripts [!INCLUDE[tsql](../../includes/tsql-md.md)], você só pode fazer isso usando identificadores delimitados.  
  
 A tabela seguinte lista palavras-chave reservadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
||||  
|-|-|-|  
|ADD|EXTERNAL|PROCEDURE|  
|ALL|FETCH|PUBLIC|  
|ALTER|FILE|RAISERROR|  
|AND|FILLFACTOR|READ|  
|ANY|FOR|READTEXT|  
|AS|FOREIGN|RECONFIGURE|  
|ASC|FREETEXT|REFERENCES|  
|AUTHORIZATION|FREETEXTTABLE|Replicação|  
|BACKUP|FROM|RESTORE|  
|BEGIN|FULL|RESTRICT|  
|BETWEEN|FUNCTION|RETURN|  
|BREAK|GOTO|REVERT|  
|BROWSE|GRANT|REVOKE|  
|BULK|GROUP|RIGHT|  
|BY|HAVING|ROLLBACK|  
|CASCADE|HOLDLOCK|ROWCOUNT|  
|CASE|IDENTITY|ROWGUIDCOL|  
|CHECK|IDENTITY_INSERT|RULE|  
|CHECKPOINT|IDENTITYCOL|SAVE|  
|CLOSE|IF|SCHEMA|  
|CLUSTERED|IN|SECURITYAUDIT|  
|COALESCE|INDEX|SELECT|  
|COLLATE|INNER|SEMANTICKEYPHRASETABLE|  
|COLUMN|INSERT|SEMANTICSIMILARITYDETAILSTABLE|  
|COMMIT|INTERSECT|SEMANTICSIMILARITYTABLE|  
|COMPUTE|INTO|SESSION_USER|  
|CONSTRAINT|IS|SET|  
|CONTAINS|JOIN|SETUSER|  
|CONTAINSTABLE|KEY|SHUTDOWN|  
|CONTINUE|KILL|SOME|  
|CONVERT|LEFT|STATISTICS|  
|CREATE|LIKE|SYSTEM_USER|  
|CROSS|LINENO|TABLE|  
|CURRENT|LOAD|TABLESAMPLE|  
|CURRENT_DATE|MERGE|TEXTSIZE|  
|CURRENT_TIME|NATIONAL|THEN|  
|CURRENT_TIMESTAMP|NOCHECK|TO|  
|CURRENT_USER|NONCLUSTERED|INÍCIO|  
|CURSOR|NOT|TRAN|  
|DATABASE|NULL|TRANSACTION|  
|DBCC|NULLIF|TRIGGER|  
|DEALLOCATE|OF|TRUNCATE|  
|DECLARE|OFF|TRY_CONVERT|  
|DEFAULT|OFFSETS|TSEQUAL|  
|DELETE|ON|UNION|  
|DENY|OPEN|UNIQUE|  
|DESC|OPENDATASOURCE|UNPIVOT|  
|DISK|OPENQUERY|UPDATE|  
|DISTINCT|OPENROWSET|UPDATETEXT|  
|DISTRIBUTED|OPENXML|USE|  
|DOUBLE|OPÇÃO|Usuário|  
|DROP|OU|VALUES|  
|DUMP|ORDER|VARYING|  
|ELSE|OUTER|VIEW|  
|END|OVER|WAITFOR|  
|ERRLVL|PERCENT|WHEN|  
|ESCAPE|PIVOT|WHERE|  
|EXCEPT|PLAN|WHILE|  
|EXEC|PRECISION|com|  
|Execute|PRIMARY|WITHIN GROUP|  
|EXISTS|PRINT|WRITETEXT|  
|EXIT|PROC||  
  
 Adicionalmente, o padrão ISO define uma lista de palavras-chave reservadas. Evite usar palavras-chave reservadas ISO em nomes de objeto e identificadores. A lista de palavras-chave reservadas de ODBC, mostrada na tabela seguinte, é a mesma do ISO.  
  
> [!NOTE]  
>  A lista de palavras-chave reservadas dos padrões ISO pode às vezes ser mais restritiva que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, em outras vezes, menos restritiva. Por exemplo, a lista de palavras-chave reservadas ISO contém **INT**. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não precisa distinguir isso como uma palavra-chave reservada.  
  
 As palavras-chave reservadas [!INCLUDE[tsql](../../includes/tsql-md.md)] podem ser usadas como identificadores ou nomes de bancos de dados ou objetos de banco de dados, como tabelas, colunas, exibições etc. Use identificadores entre aspas ou delimitados. O uso de palavras-chave reservadas como os nomes de variáveis e parâmetros de procedimento armazenado não é restrito.  
  
## <a name="odbc-reserved-keywords"></a>Palavras-chave reservadas ODBC  
 As palavras seguintes são reservadas para uso em chamadas de função ODBC. Essas palavras não restringem a gramática SQL mínima; entretanto, para garantir a compatibilidade com drivers que oferecem gramática SQL principal, os aplicativos devem evitar o uso dessas palavras-chave.  
  
 Esta é a lista atual de palavras-chave reservadas de ODBC.  
  
||||  
|-|-|-|  
|**ABSOLUTE**|**EXEC**|**OVERLAPS**|  
|**AÇÃO**|**EXECUTE**|**PAD**|  
|**ADA**|**EXISTS**|**PARTIAL**|  
|**ADD**|**EXTERNAL**|**PASCAL**|  
|**ALL**|**EXTRACT**|**POSITION**|  
|**ALLOCATE**|**FALSE**|**PRECISION**|  
|**ALTER**|**FETCH**|**PREPARE**|  
|**AND**|**FIRST**|**PRESERVE**|  
|**ANY**|**FLOAT**|**PRIMARY**|  
|**SÃO**|**PARA**|**PRIOR**|  
|**AS**|**EXTERNA**|**PRIVILEGES**|  
|**ASC**|**FORTRAN**|**PROCEDURE**|  
|**ASSERTION**|**ENCONTRADO**|**PUBLIC**|  
|**AT**|**FROM**|**READ**|  
|**AUTHORIZATION**|**FULL**|**REAL**|  
|**AVG**|**OBTER**|**REFERÊNCIAS**|  
|**BEGIN**|**GLOBAL**|**RELATIVE**|  
|**BETWEEN**|**GO**|**RESTRICT**|  
|**BIT**|**GOTO**|**REVOKE**|  
|**BIT_LENGTH**|**GRANT**|**RIGHT**|  
|**BOTH**|**GROUP**|**ROLLBACK**|  
|**BY**|**TENDO**|**ROWS**|  
|**CASCADE**|**HOUR**|**SCHEMA**|  
|**CASCADED**|**IDENTITY**|**SCROLL**|  
|**CASE**|**IMMEDIATE**|**SECOND**|  
|**CAST**|**IN**|**SEÇÃO**|  
|**CATALOG**|**INCLUDE**|**SELECT**|  
|**CHAR**|**INDEX**|**SESSÃO**|  
|**CHAR_LENGTH**|**INDICADOR**|**SESSION_USER**|  
|**CARACTERE**|**INITIALLY**|**DEFINIR**|  
|**CHARACTER_LENGTH**|**INTERNA**|**SIZE**|  
|**CHECK**|**INPUT**|**SMALLINT**|  
|**CLOSE**|**INSENSITIVE**|**ALGUNS**|  
|**COALESCE**|**INSERT**|**SPACE**|  
|**COLLATE**|**INT**|**SQL**|  
|**AGRUPAMENTO**|**INTEGER**|**SQLCA**|  
|**COLUMN**|**INTERSECT**|**SQLCODE**|  
|**COMMIT**|**INTERVAL**|**SQLERROR**|  
|**CONNECT**|**INTO**|**SQLSTATE**|  
|**CONEXÃO**|**É**|**SQLWARNING**|  
|**CONSTRAINT**|**ISOLATION**|**SUBSTRING**|  
|**CONSTRAINTS**|**JOIN**|**SUM**|  
|**CONTINUE**|**CHAVE**|**SYSTEM_USER**|  
|**CONVERT**|**LANGUAGE**|**TABLE**|  
|**CORRESPONDING**|**LAST**|**TEMPORARY**|  
|**COUNT**|**À ESQUERDA**|**EM SEGUIDA**|  
|**CREATE**|**LEFT**|**TEMPO**|  
|**CROSS**|**LEVEL**|**TIMESTAMP**|  
|**CURRENT**|**LIKE**|**TIMEZONE_HOUR**|  
|**CURRENT_DATE**|**LOCAL**|**TIMEZONE_MINUTE**|  
|**CURRENT_TIME**|**LOWER**|**TO**|  
|**CURRENT_TIMESTAMP**|**MATCH**|**TRAILING**|  
|**CURRENT_USER**|**MAX**|**TRANSACTION**|  
|**CURSOR**|**MIN**|**TRANSLATE**|  
|**DATA**|**MINUTO**|**TRANSLATION**|  
|**DAY**|**MÓDULO**|**TRIM**|  
|**DEALLOCATE**|**MONTH**|**TRUE**|  
|**DEC**|**NAMES**|**UNIÃO**|  
|**DECIMAL**|**NACIONAL**|**UNIQUE**|  
|**DECLARE**|**NATURAL**|**DESCONHECIDO**|  
|**DEFAULT**|**NCHAR**|**UPDATE**|  
|**DEFERRABLE**|**AVANÇAR**|**UPPER**|  
|**ADIADO**|**NÃO**|**USO**|  
|**DELETE**|**NONE**|**USER**|  
|**DESC**|**NOT**|**USANDO O**|  
|**DESCRIBE**|**NULL**|**VALUE**|  
|**DESCRIPTOR**|**NULLIF**|**VALORES**|  
|**DIAGNÓSTICO**|**NUMERIC**|**VARCHAR**|  
|**DESCONECTAR**|**OCTET_LENGTH**|**VARIÁVEL**|  
|**DISTINCT**|**OF**|**VIEW**|  
|**DOMAIN**|**ON**|**QUANDO**|  
|**DUPLO**|**ONLY**|**WHENEVER**|  
|**DROP**|**OPEN**|**WHERE**|  
|**ELSE**|**OPTION**|**WITH**|  
|**END**|**OU**|**TRABALHO**|  
|**END-EXEC**|**ORDEM**|**WRITE**|  
|**ESCAPE**|**EXTERNA**|**YEAR**|  
|**EXCEPT**|**SAÍDA**|**ZONE**|  
|**EXCEPTION**|||  
  
## <a name="future-keywords"></a>Palavras-chave futuras  
 As palavras-chave seguintes poderão ser reservadas em versões futuras do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à medida que novos recursos forem implementados. Considere evitar o uso destas palavras como identificadores.  
  
||||  
|-|-|-|  
|ABSOLUTE|HOST|RELATIVE|  
|ACTION|HOUR|RELEASE|  
|ADMIN|IGNORE|RESULT|  
|AFTER|IMMEDIATE|RETURNS|  
|AGGREGATE|INDICATOR|ROLE|  
|ALIAS|INITIALIZE|ROLLUP|  
|ALLOCATE|INITIALLY|ROUTINE|  
|ARE|INOUT|ROW|  
|ARRAY|INPUT|ROWS|  
|ASENSITIVE|INT|SAVEPOINT|  
|ASSERTION|INTEGER|SCROLL|  
|ASYMMETRIC|INTERSECTION|SCOPE|  
|AT|INTERVAL|SEARCH|  
|ATOMIC|ISOLATION|SECOND|  
|BEFORE|ITERATE|SECTION|  
|BINARY|LANGUAGE|SENSITIVE|  
|BIT|LARGE|SEQUENCE|  
|BLOB|LAST|SESSION|  
|BOOLEAN|LATERAL|SETS|  
|BOTH|LEADING|SIMILAR|  
|BREADTH|LESS|SIZE|  
|CALL|LEVEL|SMALLINT|  
|CALLED|LIKE_REGEX|SPACE|  
|CARDINALITY|LIMIT|SPECIFIC|  
|CASCADED|LN|SPECIFICTYPE|  
|CAST|LOCAL|SQL|  
|CATALOG|LOCALTIME|SQLEXCEPTION|  
|CHAR|LOCALTIMESTAMP|SQLSTATE|  
|CHARACTER|LOCATOR|SQLWARNING|  
|CLASS|MAP|START|  
|CLOB|MATCH|STATE|  
|COLLATION|MEMBER|STATEMENT|  
|COLLECT|METHOD|STATIC|  
|COMPLETION|MINUTE|STDDEV_POP|  
|CONDITION|MOD|STDDEV_SAMP|  
|CONNECT|MODIFIES|STRUCTURE|  
|CONNECTION|MODIFY|SUBMULTISET|  
|CONSTRAINTS|MODULE|SUBSTRING_REGEX|  
|CONSTRUCTOR|MONTH|SYMMETRIC|  
|CORR|MULTISET|SYSTEM|  
|CORRESPONDING|NAMES|TEMPORARY|  
|COVAR_POP|NATURAL|TERMINATE|  
|COVAR_SAMP|NCHAR|THAN|  
|CUBE|NCLOB|TIME|  
|CUME_DIST|NEW|TIMESTAMP|  
|CURRENT_CATALOG|NEXT|TIMEZONE_HOUR|  
|CURRENT_DEFAULT_TRANSFORM_GROUP|Não|TIMEZONE_MINUTE|  
|CURRENT_PATH|Nenhuma|TRAILING|  
|CURRENT_ROLE|NORMALIZE|TRANSLATE_REGEX|  
|CURRENT_SCHEMA|NUMERIC|TRANSLATION|  
|CURRENT_TRANSFORM_GROUP_FOR_TYPE|OBJECT|TREAT|  
|CYCLE|OCCURRENCES_REGEX|TRUE|  
|DATA|OLD|UESCAPE|  
|DATE|ONLY|UNDER|  
|DAY|OPERATION|UNKNOWN|  
|DEC|ORDINALITY|UNNEST|  
|DECIMAL|OUT|USAGE|  
|DEFERRABLE|OVERLAY|USING|  
|DEFERRED|OUTPUT|VALUE|  
|DEPTH|PAD|VAR_POP|  
|DEREF|Parâmetro|VAR_SAMP|  
|DESCRIBE|PARAMETERS|VARCHAR|  
|DESCRIPTOR|PARTIAL|VARIABLE|  
|DESTROY|PARTITION|WHENEVER|  
|DESTRUCTOR|PATH|WIDTH_BUCKET|  
|DETERMINISTIC|POSTFIX|WITHOUT|  
|DICTIONARY|PREFIX|WINDOW|  
|DIAGNOSTICS|PREORDER|WITHIN|  
|DISCONNECT|PREPARE|WORK|  
|DOMAIN|PERCENT_RANK|WRITE|  
|DYNAMIC|PERCENTILE_CONT|XMLAGG|  
|EACH|PERCENTILE_DISC|XMLATTRIBUTES|  
|ELEMENT|POSITION_REGEX|XMLBINARY|  
|END-EXEC|PRESERVE|XMLCAST|  
|EQUALS|PRIOR|XMLCOMMENT|  
|EVERY|PRIVILEGES|XMLCONCAT|  
|EXCEPTION|RANGE|XMLDOCUMENT|  
|FALSE|READS|XMLELEMENT|  
|FILTER|REAL|XMLEXISTS|  
|FIRST|RECURSIVE|XMLFOREST|  
|FLOAT|REF|XMLITERATE|  
|FOUND|REFERENCING|XMLNAMESPACES|  
|GRATUITO|REGR_AVGX|XMLPARSE|  
|FULLTEXTTABLE|REGR_AVGY|XMLPI|  
|FUSION|REGR_COUNT|XMLQUERY|  
|GENERAL|REGR_INTERCEPT|XMLSERIALIZE|  
|GET|REGR_R2|XMLTABLE|  
|GLOBAL|REGR_SLOPE|XMLTEXT|  
|GO|REGR_SXX|XMLVALIDATE|  
|GROUPING|REGR_SXY|YEAR|  
|HOLD|REGR_SYY|ZONE|  
  
## <a name="see-also"></a>Consulte também  
 [SET QUOTED_IDENTIFIER &#40; Transact-SQL &#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  
