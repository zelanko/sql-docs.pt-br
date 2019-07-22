---
title: SOUNDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SOUNDEX
- SOUNDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SOUNDEX function
- comparing string data
- strings [SQL Server], similarity
- strings [SQL Server], comparing
- SOUNDEX values
ms.assetid: 8f1ed34e-8467-4512-a211-e0f43dee6584
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3f0a8dd4c5faecc54b7d1c5a5d506fc7cf4ecd00
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907074"
---
# <a name="soundex-transact-sql"></a>SOUNDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna um código de quatro caracteres (SOUNDEX) para avaliar a semelhança de duas cadeias de caracteres.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SOUNDEX ( character_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) alfanumérica de dados de caractere. *character_expression* pode ser uma constante, variável ou coluna.  
  
## <a name="return-types"></a>Tipos de retorno  
 **varchar**  
  
## <a name="remarks"></a>Remarks  
 SOUNDEX converte uma cadeia de caracteres alfanumérica em código de quatro caracteres que se baseia no som da cadeia de caracteres quando ela é falada. O primeiro caractere do código é o primeiro caractere de *character_expression*, convertido em maiúsculas. O segundo até o quarto caractere do código são números que representam as letras da expressão. As letras A, E, I, O, U, H, W e Y serão ignoradas, a menos que elas sejam a primeira letra da cadeia de caracteres. Zeros serão adicionados ao término, se necessário, para gerar um código de quatro caracteres. Para obter mais informações sobre o código SOUNDEX, consulte [O sistema de indexação Soundex](https://www.archives.gov/research/census/soundex.html).  
  
 Os códigos de SOUNDEX de cadeias de caracteres diferentes podem ser comparados para verificar a similaridade do som das cadeias de caracteres quando faladas. A função DIFFERENCE executa um SOUNDEX de duas cadeias de caracteres, e retorna um número inteiro que representa o grau de similaridade dos códigos de SOUNDEX dessas cadeias de caracteres.  
  
 SOUNDEX diferencia ordenações. As funções de cadeia de caracteres podem ser aninhadas.  
  
## <a name="soundex-compatibility"></a>Compatibilidade com SOUNDEX  
 Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a função SOUNDEX aplicou um subconjunto das regras de SOUNDEX. No nível de compatibilidade de banco de dados 110 ou superior, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplica mais um conjunto mais completo das regras.  
  
 Após a atualização para o nível de compatibilidade 110 ou superior, talvez seja necessário recriar os índices, os heaps ou as restrições CHECK que usam a função SOUNDEX.  
  
-   Um heap que contém uma coluna computada persistente definida com SOUNDEX não pode ser consultado até que o heap seja reconstruído executando a instrução `ALTER TABLE <table> REBUILD`.  
  
-   As restrições CHECK definidas com SOUNDEX são desabilitadas após a atualização. Para habilitar a restrição, execute a instrução `ALTER TABLE <table> WITH CHECK CHECK CONSTRAINT ALL`.  
  
-   Índices (incluindo exibições indexadas) que contêm uma coluna computada persistida definida com SOUNDEX não pode ser consultado até que o índice seja reconstruído executando a instrução `ALTER INDEX ALL ON <object> REBUILD`.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra a função SOUNDEX e a função DIFFERENCE relacionada. No primeiro exemplo, os valores padrão de `SOUNDEX` são retornados para todas as consoantes. Retornar o `SOUNDEX` para `Smith` e `Smythe` gerará o mesmo resultado SOUNDEX, pois todas as vogais, a letra `y`, as letras duplicadas e a letra `h` não são incluídas.  
  
```  
-- Using SOUNDEX  
SELECT SOUNDEX ('Smith'), SOUNDEX ('Smythe');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] Válido para uma ordenação Latin1_General.  
  
```  
  
----- -----   
S530  S530    
  
(1 row(s) affected)  
```  
  
 A função `DIFFERENCE` compara a diferença dos resultados de padrão de `SOUNDEX`. O exemplo a seguir mostra duas cadeias de caracteres que diferem somente nas vogais. A diferença retornada é `4`, a mais baixa diferença possível.  
  
```  
-- Using DIFFERENCE  
SELECT DIFFERENCE('Smithers', 'Smythers');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] Válido para uma ordenação Latin1_General.  
  
```  
-----------   
4             
  
(1 row(s) affected)  
```  
  
 No exemplo a seguir, as cadeias de caracteres diferem em consoantes; portanto, a diferença retornada é `2`, a maior diferença.  
  
```  
SELECT DIFFERENCE('Anothers', 'Brothers');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] Válido para uma ordenação Latin1_General.  
  
```  
-----------   
2             
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DIFFERENCE &#40;Transact-SQL&#41;](../../t-sql/functions/difference-transact-sql.md)   
 [Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  

