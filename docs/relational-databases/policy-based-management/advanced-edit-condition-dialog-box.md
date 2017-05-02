---
title: "Caixa de diálogo (Condição de) Edição Avançada | Microsoft Docs"
ms.custom: 
ms.date: 08/12/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.dmf.condition.advancededit.f1
ms.assetid: a0bbe501-78c5-45ad-9087-965d04855663
caps.latest.revision: 44
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 553e8aece3969407a818d98cf69c20bf922d3601
ms.lasthandoff: 04/11/2017

---
# <a name="advanced-edit-condition-dialog-box"></a>Caixa de diálogo Edição Avançada (Condição)
  Use a caixa de diálogo **Edição Avançada** para criar expressões complexas para condições do Gerenciamento Baseado em Políticas.  
  
## <a name="options"></a>Opções  
 **Valor da célula**  
 Exibe a função ou a expressão que será usada para o valor de célula quando você o criar. Quando você clicar em **OK**, o valor da célula aparecerá na célula **Campo** ou **Valor** na caixa de expressão da condição da caixa de diálogo **Criar Nova Condição** ou **Abrir Condição** na página **Geral** .  
  
 **Funções e propriedades**  
 Exibe as funções e propriedades disponíveis.  
  
 **Detalhes**  
 Exibe informações sobre as funções e propriedades nos formatos assinatura de função, descrição de função, valor de retorno e exemplo.  
  
## <a name="syntax"></a>Sintaxe  
 Expressões válidas devem estar no seguinte formato:  
  
 `{property | function | constant}`  
  
 `{operator}`  
  
 `{property | function | constant}`  
  
## <a name="examples"></a>Exemplos  
 Alguns exemplos de expressões válidas incluem:  
  
-   *Property1*> 5  
  
-   *Property1*=*Property2*  
  
-   Add(5, Multiply(.2,*Property1*))<*Property2*  
  
-   *Sometext* IN *Property1*  
  
-   *Property1*< Fn(*Property2*)  
  
-   BitwiseAnd(*Property1*,*Property2*)= 0  
  
## <a name="additional-function-information"></a>Informações adicionais sobre as funções  
 A seção a seguir fornece informações adicionais sobre as funções que você pode usar para criar expressões complexas para condições de Gerenciamento Baseado em Políticas.  
  
> **IMPORTANTE:** As funções que você pode usar para criar condições de Gerenciamento Baseado em Políticas nem sempre usam a sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] . Não se esqueça de seguir a sintaxe de exemplo. Por exemplo, quando usar as funções **DateAdd** ou **DatePart** , você deverá colocar o argumento *datepart* entre aspas simples.  
  
|Função|Assinatura|Descrição|Argumentos|Valor de retorno|Exemplo|  
|--------------|---------------|-----------------|---------------|------------------|-------------|  
|**Add()**|Numeric Add (Numeric *expression1*, Numeric *expression2*)|Soma dois números.|*expression1* e *expression2* – Qualquer expressão válida de qualquer um dos tipos de dados na categoria numeric, exceto pelo tipo de dados **bit** . Pode ser uma constante, propriedade ou função que retorna um tipo numérico.|Retorna o tipo de dados do argumento que tem a maior precedência.|`Add(Property1, 5)`|  
|**Array()**|Array Array (VarArgs *expression*)|Cria uma matriz com base em uma lista de valores. Pode ser usado com funções de agregação como Sum() e Count().|*expression* – Uma expressão que será convertida em uma matriz.|A matriz|`Array(2,3,4,5,6)`|  
|**Avg()**|Numeric Avg (*VarArgs*)|Retorna a média dos valores na lista de argumentos.|*VarArgs* – Uma lista da expressão Variant da categoria de tipo de dados numeric ou approximate numeric exata, exceto pelo tipo de dados **bit** .|O tipo de retorno é determinado pelo tipo do resultado avaliado da expressão.<br /><br /> Se o resultado da expressão for as categorias **integer**, **decimal**, **money** e **smallmoney**, **float** e **real** , os tipos de retorno serão **int**, **decimal**, **money**e **float**, respectivamente.|`Avg(1.0, 2.0, 3.0, 4.0, 5.0)` retorna `3.0` neste exemplo.|  
|**BitwiseAnd()**|Numeric BitwiseAnd (Numeric *expression 1*, Numeric *expression2*)|Executa uma operação lógica AND bit a bit entre dois valores inteiros.|*expression1* e *expression2* – Qualquer expressão válida de um dos tipos de dados da categoria de tipo de dados integer.|Retorna um valor da categoria de tipo de dados integer.|`BitwiseAnd(Property1, Property2)`|  
|**BitwiseOr()**|Numeric BitwiseOr (Numeric *expression1*, Numeric *expression2*)|Executa uma operação OR lógica de bit a bit entre dois valores inteiros especificados.|*expression1* e *expression2* – Qualquer expressão válida de um dos tipos de dados da categoria de tipo de dados integer.|Retorna um valor da categoria de tipo de dados integer.|`BitwiseOr(Property1, Property2)`|  
|**Concatenate()**|String Concatenate (String *string1*, String *string2*)|Concatena duas cadeias de caracteres.|*string1* e *string2* – São as duas cadeias de caracteres que você deseja concatenar. Pode ser qualquer cadeia não nula válida.|A cadeia de caracteres concatenada, com *string1* seguida por *string2*.|`Concatenate("Hello", " World` `")` retorna "`Hello World`".|  
|**Count()**|Numeric Count (*VarArgs*)|Retorna o número de itens na lista de argumentos.|*VarArgs* – Uma expressão de qualquer tipo, exceto **text**, **image**e **ntext**.|Retorna um valor da categoria de tipo de dados integer.|`Count(1.0, 2.0, 3.0, 4.0, 5.0)` retorna `5` neste exemplo.|  
|**DateAdd()**|DateTime DateAdd (String *datepart*, Numeric *number*, DateTime *date*)|Retorna o novo valor **datetime** com base na adição de um intervalo à data especificada.|*datepart* – Parâmetro que especifica em qual parte da data um valor novo será retornado. Alguns dos tipos com suporte são year(aa, aaaa), month(mm, m) e dayofyear(da, a). Para obter mais informações, veja [DATEADD &#40;Transact-SQL&#41;](../../t-sql/functions/dateadd-transact-sql.md).<br /><br /> *number* – O valor usado para incrementar *datepart*.<br /><br /> *date* – Uma expressão que retorna um valor **datetime** ou uma cadeia de caracteres em um formato de data.|É o novo valor **datetime** com base na adição de um intervalo à data especificada.|**Example:** `DateAdd('day', 21, DateTime('2007-08-06 14:21:50'))` returns `'2007-08-27 14:21:50'` in this example.<br /><br /> Veja a seguir o *dateparts* e as abreviações que são aceitas por esta função.<br /><br /> **year**: aa, aaaa<br /><br /> **month**: mm, m<br /><br /> **dayofyear**: da, a<br /><br /> **day**: dd, d<br /><br /> **week**: wk, ww<br /><br /> **weekday**: dw, w<br /><br /> **hour**: hh<br /><br /> **minute**: mi, n<br /><br /> **second**: ss, s<br /><br /> **millisecond**: ms|  
|**DatePart()**|Numeric DatePart (String *datepart*, DateTime *date*)|Retorna um inteiro que representa a *datepart* especificada da data especificada.|*datepart* – Parâmetro que especifica a parte da data a ser retornada. Alguns dos tipos com suporte são year(yy, yyyy), month(mm., m) e dayofyear(dy, y). Para obter mais informações, veja [DATEPART &#40;Transact-SQL&#41;](../../t-sql/functions/datepart-transact-sql.md).<br /><br /> *date* – Uma expressão que retorna um valor **datetime** ou uma cadeia de caracteres em um formato de data.|Retorna o valor da categoria de tipo de dados inteiros que representa a *datepart* especificada da data especificada.|`DatePart('month', DateTime('2007-08-06 14:21:50.620'))` retorna `8` neste exemplo.|  
|**DateTime()**|DateTime DateTime (String *dateString*)|Cria um valor datetime com base em uma cadeia de caracteres.|*dateString* – O valor datetime como uma cadeia de caracteres.|Retorna um valor datatime criado a partir da cadeia de caracteres de entrada.|`DateTime('3/12/2006')`|  
|**Divide()**|Numeric Divide (Numeric *expression_dividend*, Numeric *expression_divisor*)|Divide um número por outro.|*expression_dividend* –Expressão numérica a ser dividida. O dividendo pode ser qualquer expressão válida para qualquer um dos tipos de dados da categoria de tipo de dados numéricos, com exceção do tipo de dados **datetime** .<br /><br /> *expression_divisor* – Expressão numérica pela qual o dividendo será dividido. O divisor pode ser qualquer expressão válida para qualquer um dos tipos de dados da categoria de tipo de dados numéricos, com exceção do tipo de dados **datetime** .|Retorna o tipo de dados do argumento que tem a maior precedência.|**Exemplo:** `Divide(Property1, 2)`<br /><br /> Observação: esta será uma operação dupla. Para fazer uma comparação de inteiro, você deve combinar os resultados com `Round()`. Por exemplo: `Round(Divide(10, 3), 0) = 3`.|  
|**Enum()**|Numeric Enum (String *enumTypeName*, String *enumValueName*)|Cria um valor de enumeração com base em uma cadeia de caracteres.|*enumTypeName* – O nome do tipo enum.<br /><br /> *enumValueName* – O valor do enum.|Retorna o valor de enum como um valor numérico.|`Enum('CompatibilityLevel','Version100')`|  
|**Escape()**|String Escape (String *replaceString*, String *stringToEscape*, String *escapeString*)|Escape de uma subcadeia da cadeia de entrada com uma determinada cadeia de caracteres de escape.|*replaceString* – é a cadeia de entrada.<br /><br /> *stringToEscape* – é uma subcadeia de *replaceString*. Esta é a cadeia em frente à qual você deseja adicionar uma cadeia de escape.<br /><br /> *escapeString* – é a cadeia de escape que você deseja adicionar na frente de cada instância de *stringToEscape*.|Retorna uma *replaceString* modificada na qual cada instância de *stringToEscape* é precedida por *escapeString*.|`Escape("Hello", "l", "[")` retorna "`He[l[lo`".|  
|**ExecuteSQL()**|Variant ExecuteSQL (String *returnType*, String *sqlQuery*)|Executa a consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] no servidor de destino.<br /><br /> Para obter mais informações sobre ExecuteSql(), veja [Função ExecuteSql()](http://blogs.msdn.com/b/sqlpbm/archive/2008/07/03/executesql.aspx).|*returnType* – especifica o tipo de retorno dos dados retornados pela instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] . Os literais válidos para *returnType* são os seguintes: **Numeric**, **String**, **Bool**, **DateTime**, **Array**e **Guid**.<br /><br /> *sqlQuery* – A cadeia de caracteres que contém a consulta a ser executada.||`ExecuteSQL ('Numeric', 'SELECT COUNT(*) FROM msdb.dbo.sysjobs') <> 0`<br /><br /> Executa uma consulta de Transact-SQL com valor escalar em uma instância de destino do SQL Server. Só uma coluna pode ser especificada em uma instrução `SELECT` ; são ignoradas colunas adicionais além da primeira. A consulta resultante deveria retornar só uma linha; são ignoradas linhas adicionais além da primeira. Se a consulta retornar um conjunto vazio, a expressão de condição compilada com base no `ExecuteSQL` será avaliada como falsa. `ExecuteSql` oferece suporte aos modos de avaliação **Sob demanda** e **Ao agendar** .<br /><br /> -`@@ObjectName`:<br />                      Corresponde ao campo de nome em [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md). A variável será substituída pelo nome do objeto atual.<br /><br /> -`@@SchemaName`: corresponde ao campo de nome em [sys.schemas](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md). A variável será substituída pelo nome do esquema para o objeto atual, se aplicável.<br /><br /> Observação: para incluir uma aspa simples em uma instrução ExecuteSQL, utilize uma segunda aspa simples. Por exemplo, para incluir uma referência a um usuário nomeado O'Brian, digite O"Brian.|  
|**ExecuteWQL()**|Variant ExecuteWQL (string *returnType* , string *namespace*, string *wql*)|Executa o script WQL no namespace que é fornecido. A instrução de seleção pode conter apenas uma única coluna de retorno. Se mais de uma coluna for fornecida, um erro será gerado.|*returnType* – Especifica o tipo de retorno de dados que é retornado pelo WQL. As literais válidas são **Numeric**, **String**, **Bool**, **DateTime**, **Array**e **Guid**.<br /><br /> *namespace* – Namespace WMI que será usado para a execução.<br /><br /> *wql* – Cadeia de caracteres que contém o WQL a ser executado.||`ExecuteWQL('Numeric', 'root\CIMV2', 'select NumberOfProcessors from win32_ComputerSystem') <> 0`|  
|**False()**|Bool False()|Retorna um valor booliano FALSE.|Nenhuma|Retorna um valor booliano FALSE.|`IsDatabaseMailEnabled = False()`|  
|**GetDate()**|DateTime GetDate()|Retorna a data do sistema.|Nenhuma|Retorna a data de sistema como DateTime.|`@DateLastModified = GetDate()`|  
|**Guid()**|Guid Guid(String *guidString*)|Retorna um GUID de uma cadeia de caracteres.|*guidString* – A representação de cadeia de caracteres do GUID a ser criado.|Retorna o GUID criado a partir da cadeia de caracteres.|`Guid('12340000-0000-3455-0000-000000000454')`|  
|**IsNull()**|Variant IsNull (Variant *check_expression*, Variant *replacement_value*)|O valor de *check_expression* será retornado se não for NULL; caso contrário, *replacement_value* será retornado. Se os tipos forem diferentes, *replacement_value* será implicitamente convertido para o tipo *check_expression*.|*check_expression* – A expressão a ser verificada quanto a NULL. *check_expression* pode ser qualquer um dos tipos de Gerenciamento Baseado em Políticas com suporte: Numeric, String, Bool, DateTime, Array e Guid.<br /><br /> *replacement_value* – A expressão a ser retornada se *check_expression* for NULL. *replacement_value* deve ser de um tipo que seja implicitamente convertido para o tipo *check_expression*.|O tipo de retorno será o tipo de *check_expression* se *check_expression* não for NULL; caso contrário, o tipo de *replacement_value* será retornado.||  
|**Len()**|Numeric Len (*string_expression*)|Retorna o número de caracteres, da expressão da cadeia de caracteres atribuída, excluindo espaços em branco à direita.|*string_expression* – A expressão de cadeia de caracteres a ser avaliada.|Retorna um valor da categoria de tipo de dados integer.|`Len('Hello')` retorna `5` neste exemplo.|  
|**Lower()**|String Lower (String*_expression*)|Retorna a cadeia de caracteres após converter todas as maiúsculas em minúsculas.|*expression* – A expressão de cadeia de caracteres de origem.|Retorna uma cadeia de caracteres que representa a expressão da cadeia de caracteres de origem após a conversão de todas as maiúsculas em minúsculas.|`Len('HeLlO')` retorna `'hello'` neste exemplo.|  
|**Mod()**|Numeric Mod (Numeric *expression_dividend*, Numeric *expression_divisor*)|Fornece o resto inteiro após dividir a primeira expressão numérica pela segunda expressão numérica.|*expression_dividend* –Expressão numérica a ser dividida. *expression_dividend* deve ser qualquer expressão válida de qualquer um dos tipos de dados nas categorias de tipos de dados integer ou numeric.<br /><br /> *expression_divisor* – A expressão numérica pela qual o dividendo será dividido. *expression_divisor* deve ser qualquer expressão válida de qualquer um dos tipos de dados nas categorias de tipos de dados integer ou numeric.|Retorna um valor da categoria de tipo de dados integer.|`Mod(Property1, 3)`|  
|**Multiply()**|Numeric Multiply (Numeric *expression1*, Numeric *expression2*)|Multiplica duas expressões.|*expression1* e *expression2* – Qualquer expressão válida de qualquer um dos tipos de dados na categoria numeric, exceto pelo tipo de dados **datetime** .|Retorna o tipo de dados do argumento que tem a maior precedência.|`Multiply(Property1, .20)`|  
|**Power()**|Numeric Power (Numeric *numeric_expression*, Numeric *expression_power*)|Retorna o valor da expressão especificada elevada à potência especificada.|*numeric_expression* – Uma expressão da categoria de tipo de dados exact numeric ou approximate numeric data, exceto pelo tipo de dados bit.<br /><br /> *expression_power* – A potência à qual *numeric_expression*será elevada. *expression_power* pode ser uma expressão da categoria de tipo de dados exact numeric ou approximate numeric data, exceto pelo tipo de dados **bit** .|O tipo de retorno é o mesmo que *numeric_expression*.|`Power(Property1, 3)`|  
|**Round()**|Numeric Round (Numeric *expression*, Numeric *expression_precision*)|Retorna uma expressão numérica arredondada ao comprimento ou precisão especificados.|*expression* – Uma expressão da categoria de tipo de dados exact numeric ou approximate numeric data, exceto pelo tipo de dados **bit** .<br /><br /> *expression_precision* – A precisão para a qual a expressão deve ser arredondada. Quando *expression_precision* é um número positivo, *numeric_expression* é arredondado para o número de posições decimais especificado pelo tamanho. Quando *expression_precision* é um número negativo, *numeric_expression* é arredondado à esquerda da vírgula decimal, conforme especificado por *expression_precision*.|Retorna o mesmo tipo que *numeric_expression*.|`Round(5.333, 0)`|  
|**String()**|String String (Variant*_expression*)|Converte uma variante em uma cadeia de caracteres.|*expression* – A expressão variante a ser convertida em uma cadeia de caracteres.|Retorna o valor da cadeia de caracteres da expressão variável.|`String(4)`|  
|**Sum()**|Numeric Sum (*VarArgs*)|Retorna a soma de todos os valores da lista de argumentos. Sum pode ser usada com valores numéricos.|*VarArgs*– Uma lista da expressão Variant da categoria de tipo de dados numeric ou approximate numeric exata, exceto pelo tipo de dados **bit** .|Retorna a adição de todos os valores da expressão no tipo de dados de expressão mais preciso.<br /><br /> Se o resultado da expressão for as categorias **integer**, **numeric**, **money** e **small money**, **float** e **real** , os tipos de retorno serão **int**, **numeric**, **money**e **float**, respectivamente.|`Sum(1.0, 2.0, 3.0, 4.0, 5.0)` retorna `15` neste exemplo.|  
|**True()**|Bool TRUE()|Retorna um valor booliano TRUE.||Retorna um valor booliano TRUE.|`IsDatabaseMailEnabled = True()`|  
|**Upper()**|String Upper (String*_expression*)|Retorna a cadeia de caracteres após converter todas as minúsculas em maiúsculas.|*expression* – A expressão de cadeia de caracteres de origem.|Retorna uma cadeia de caracteres que representa a expressão da cadeia de caracteres de origem após a conversão de todas as minúsculas em maiúsculas.|`Upper('HeLlO')` retorna `'HELLO'` neste exemplo.|  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo Criar Nova Condição ou Abrir Condição, Página Geral](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-general-page.md)   
 [Administrar servidores com Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  

