---
title: '&lt; (Menor que) (Expressão SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- less than (<)
- < (less than operator)
ms.assetid: 8674afdc-4276-46cb-be08-5aadfe8b9624
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 68076395e95e50118b9842d9cee2ef6bb428d622
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725306"
---
# <a name="lt-less-than-ssis-expression"></a>&lt; (Menor que) (Expressão SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Executa uma comparação para determinar se a primeira expressão é menor que a segunda. O avaliador de expressões converte automaticamente muitos tipos de dados antes de executar a comparação.  
  
> [!NOTE]  
>  Este operador não aceita comparações que usam os tipos de dados DT_TEXT, DT_NTEXT ou DT_IMAGE.  
  
 No entanto, alguns tipos de dados requerem que a expressão inclua uma conversão explícita antes de ser avaliada com êxito. Para obter mais informações sobre conversões legais entre tipos de dados, consulte [Conversão &#40;Expressão do SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
expression1 < expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression1, expression2*  
 É qualquer expressão válida.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_BOOL  
  
## <a name="remarks"></a>Remarks  
 Se qualquer expressão na comparação for nula, o resultado da comparação será nulo. Se ambas as expressões forem nulas, o resultado será nulo.  
  
 O conjunto de expressões, *expression1* e *expression2*, deve seguir uma destas regras:  
  
-   **Numérico** Ambas *expression1* e *expression2* devem ser um tipo de dados numérico. A intersecção dos tipos de dados deve ser um tipo de dados numérico, como especificado nas regras sobre as conversões numéricas implícitas que o avaliador de expressões executa. A interseção dos dois tipos de dados numéricos não pode ser nula. Para obter mais informações, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
-   **Character** Tanto *expression1* quanto *expression2* devem ser avaliadas como um tipo de dados DT_STR ou DT_WSTR. As duas expressões podem ser avaliadas como tipos de dados de cadeia diferentes.  
  
    > [!NOTE]  
    >  Comparações de cadeia de caracteres diferenciam maiúsculas de minúsculas, acentuação, kana e largura.  
  
-   **Date, Time ou Date/Time** Tanto *expression1* quanto *expression2* devem ser avaliadas como um dos seguintes tipos de dados: DT_DBDATE, DT_DATE, DT_DBTIME, DT_DBTIME2, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAPMOFFSET ou DT_FILETIME.  
  
    > [!NOTE]  
    >  O sistema não aceita comparações entre uma expressão que avalia um tipo de dados de hora e uma expressão que avalia um tipo de dados de data ou data/hora. O sistema gera um erro.  
  
     Ao comparar as expressões, o sistema aplica as seguintes regras de conversão na ordem listada:  
  
    -   Quando as duas expressões avaliarem o mesmo tipo de dados, uma comparação daquele tipo de dados é executada.  
  
    -   Se uma expressão for um tipo de dados DT_DBTIMESTAMPOFFSET, a outra expressão será convertida implicitamente para DT_DBTIMESTAMPOFFSET, e uma comparação de DT_DBTIMESTAMPOFFSET será executada. Para obter mais informações, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
    -   Se uma expressão for um tipo de dados DT_DBTIMESTAMP2, a outra expressão será convertida implicitamente para DT_DBTIMESTAMP2, e uma comparação de DT_DBTIMESTAMP2 será executada.  
  
    -   Se uma expressão for um tipo de dados DT_DBTIME2, a outra expressão será convertida implicitamente para DT_DBTIME2, e uma comparação de DT_DBTIME2 será executada.  
  
    -   Se uma expressão for de um tipo diferente de DT_DBTIMESTAMPOFFSET, DT_DBTIMESTAMP2 ou DT_DBTIME2, as expressões serão convertidas para o tipo de dados DT_DBTIMESTAMP antes de serem comparadas.  
  
     Ao comparar as expressões, o sistema faz as seguintes suposições:  
  
    -   Se cada expressão for um tipo de dados que inclui segundos fracionais, o sistema assumirá que o tipo de dados com o número de dígitos mínimo para os segundos fracionais tem zeros nos dígitos restantes.  
  
    -   Se cada expressão for um tipo de dados de data, mas somente um tiver um deslocamento de fuso horário, o sistema assumirá que o tipo de dados de data sem o deslocamento de fuso horário estará em UTC (Tempo Universal Coordenado).  
  
 Para obter mais informações sobre tipos de dados, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo será avaliado como TRUE se a data atual for posterior a 4 de julho de 2003. Para obter mais informações, consulte [GETDATE &#40;Expressão SSIS&#41;](../../integration-services/expressions/getdate-ssis-expression.md).  
  
```  
"7/4/2003" < GETDATE()  
```  
  
 Este exemplo avaliará TRUE se o valor na coluna **ListPrice** for menor que 500.  
  
```  
ListPrice < 500  
```  
  
 Este exemplo usa a variável **LPrice**. Ela será avaliada como TRUE se o valor de **LPrice** for menor que 500. O tipo de dados da variável deve ser numérico para que a expressão seja analisada.  
  
```  
@LPrice < 500  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#62; &#40;Maior que&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/greater-than-ssis-expression.md)   
 [&#62;= &#40;Maior ou igual a&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/greater-than-or-equal-to-ssis-expression.md)   
 [&#60;= &#40;Menor ou igual a&#41; &#40;Expressão SSIS&#41;](../../integration-services/expressions/less-than-or-equal-to-ssis-expression.md)   
 [Precedência de operador e capacidade de associação](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
