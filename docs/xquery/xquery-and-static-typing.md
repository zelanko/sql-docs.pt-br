---
title: XQuery e Static digitando | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- XQuery, static typing
- static typing
- checking static types
- inference [XQuery]
ms.assetid: d599c791-200d-46f8-b758-97e761a1a5c0
caps.latest.revision: "38"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2861a4b1460bebf51ea138678dd797e5f0048a41
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="xquery-and-static-typing"></a>XQuery e digitação estática
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  O XQuery no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é uma linguagem estaticamente digitada. Ou seja, ele gera erros de tipo durante a compilação de consulta quando uma expressão retornar um valor que tenha um tipo ou cardinalidade que não sejam aceitos por determinada função ou operador. Além disso, a verificação de tipo estático também poderá detectar se uma expressão de caminho em um documento XML digitado tiver sido digitada incorretamente. O compilador do XQuery primeiro aplica a fase de normalização que adiciona as operações implícitas, como atomização e, em seguida, executa a inferência e a verificação de tipo estático.  
  
## <a name="static-type-inference"></a>Inferência de tipo estático  
 A inferência de tipo estático determina o tipo de retorno de uma expressão. Ela determina isso considerando os tipos estáticos dos parâmetros de entrada e a semântica estática da operação e inferindo o tipo estático do resultado. Por exemplo, o tipo estático da expressão 1 + 2,3 é determinado da seguinte forma:  
  
-   O tipo estático de 1 é **xs: Integer** e o tipo estático de 2,3 é **xs: decimal**. Com base na semântica dinâmica, a semântica estática do  **+**  operação converte o inteiro em um decimal e retorna um decimal. O tipo estático inferido seria então **xs: decimal**.  
  
 Para instâncias XML não digitadas, há tipos especiais para indicar que os dados não foram digitados. Essas informações são usadas durante a verificação de tipo estático e para executar determinadas conversões implícitas.  
  
 Para dados digitados, o tipo de entrada é inferido da coleção de esquemas XML que restringe a instância do tipo de dados XML. Por exemplo, se o esquema só permitir elementos do tipo **xs: Integer**, os resultados de uma expressão de caminho usando esse elemento serão zero ou mais elementos do tipo **xs: Integer**. Isso é atualmente expresso usando uma expressão como `element(age,xs:integer)*` onde o asterisco (\*) indica a cardinalidade do tipo resultante. Neste exemplo, a expressão pode resultar em zero ou mais elementos de nome "age" e digite **xs: Integer**. Outras cardinalidades são exatamente um e são expressas usando o nome de tipo sozinho, zero ou um e expressas usando um ponto de interrogação (**?**) e 1 ou mais e expressas usando um sinal de adição (**+**) .  
  
 Às vezes, a inferência de tipo estático pode deduzir que uma expressão sempre retornará a sequência vazia. Por exemplo, se uma expressão de caminho em um tipo de dados XML com tipo procurará um \<nome > elemento dentro um \<cliente > elemento (/cliente/nome), mas o esquema não permite uma \<nome > dentro de um \<cliente >, a inferência de tipo estático deduzirá que o resultado será vazio. Isso será usado para detectar consultas incorretas e será relatado como um erro estático, a menos que a expressão seja () ou **(()) de dados**.  
  
 As regras de inferência detalhadas são fornecidas na semântica formal da especificação XQuery. A Microsoft somente as modificou levemente para que funcionem com instâncias do tipo de dados XML digitados. A mudança mais importante do padrão é que o nó de documento implícito sabe sobre o tipo da instância do tipo de dados XML. Consequentemente, uma expressão de caminho da forma /age será digitada precisamente com base nessas informações.  
  
 Usando [modelos do SQL Server Profiler e permissões](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md), você pode ver os tipos estáticos retornados como parte de compilações de consulta. Para vê-los, o seu rastreamento deve incluir o evento de tipo estático do XQuery na categoria de eventos TSQL.  
  
## <a name="static-type-checking"></a>Verificação de tipo estático  
 A verificação de tipo estático assegura que a execução do tempo de execução só receberá valores que sejam o tipo apropriado para a operação. Como os tipos não precisam ser verificados no tempo de execução, os erros em potencial podem ser detectados erros precocemente na compilação. Isso ajuda a melhorar o desempenho. No entanto, a digitação estática requer que o autor da consulta tenha mais cuidado ao formular uma consulta.  
  
 A seguir, são apresentados os tipos apropriados que podem ser usados:  
  
-   Tipos explicitamente permitidos por uma função ou operação.  
  
-   Um subtipo de um tipo explicitamente permitido.  
  
 Os subtipos são definidos, com base nas regras de subdigitação por usar derivação por restrição ou extensão do esquema XML. Por exemplo, um tipo S é um subtipo do tipo T, se todos os valores que tiverem o tipo S também forem instâncias do tipo T.  
  
 Além disso, todos os valores inteiros também são valores decimais com base na hierarquia do tipo de esquemas XML. No entanto, nem todos os valores decimais são inteiros. Portanto, um inteiro é um subtipo de decimal, mas não vice-versa. Por exemplo, o  **+**  operação permite apenas os valores de determinados tipos, como os tipos numéricos **xs: Integer**, **xs: decimal**, **xs: float**, e **xs: Double**. Se os valores de outros tipos, como **xs: string**, são passados, a operação gerará um erro de tipo. Isso será referido como digitação forte. Os valores de outros tipos, como o tipo atômico usado para indicar XML não digitado, podem ser convertidos implicitamente em um valor de um tipo que a operação aceite. Isso é referido como digitação fraca.  
  
 Se for necessário depois de uma conversão implícita, a verificação de tipo estático garantirá que somente valores dos tipos permitidos com a cardinalidade correta serão passados em uma operação. Para "cadeia de caracteres" + 1, ele reconhece que é o tipo estático da "cadeia de caracteres" **xs: string**. Como isso não é um tipo permitido para o  **+**  operação, um erro de tipo é gerada.  
  
 No caso de adicionar o resultado de uma expressão arbitrária E1 a uma expressão arbitrária E2 (E1 + E2), a inferência de tipo estático determina os tipos estáticos de E1 e E2 primeiro e, em seguida, verifica os tipos estáticos com os tipos permitidos para a operação. Por exemplo, se o tipo estático de E1 pode ser um **xs: string** ou um **xs: Integer**, a verificação de tipo estático gera um erro de digitação, mesmo que alguns valores em tempo de execução pode ser números inteiros. O mesmo seria o caso se o tipo estático de E1 fosse **xs: Integer\***. Porque o  **+**  operação só aceita exatamente um valor inteiro e E1 poderia retornar zero ou mais de 1, a verificação de tipo estático gera um erro.  
  
 Como mencionado anteriormente, a inferência de tipo frequentemente infere um tipo que é mais amplo do que aquilo que o usuário sabe sobre o tipo de dados sendo passados. Nesses casos, o usuário precisa reescrever a consulta. Alguns casos característicos incluem o seguinte:  
  
-   O tipo infere um tipo mais geral, como um supertipo ou uma união de tipos. Se o tipo for um tipo atômico, você deve usar a expressão de conversão ou função de construtor para indicar o tipo estático real. Por exemplo, se o tipo inferido da expressão E1 for uma escolha entre **xs: string** ou **xs: Integer** e requer a adição **xs: Integer**, você deve escrever `xs:integer(E1) + E2` em vez de `E1+E2`. Essa expressão pode falhar em tempo de execução, se for encontrado um valor de cadeia de caracteres que não pode ser convertido em **xs: Integer**. No entanto, a expressão agora passará a verificação de tipo estático. Essa expressão é mapeada para a sequência vazia.  
  
-   O tipo infere uma cardinalidade superior àquela que os dados realmente contêm. Isso ocorre com frequência, porque o **xml** tipo de dados pode conter mais de um elemento de nível superior, e uma coleção de esquemas XML não pode restringir isso. Para reduzir o tipo estático e garantir que realmente haja um valor máximo sendo passado, você deve usar o predicado posicional `[1]`. Por exemplo, para adicionar 1 ao valor do atributo `c` do elemento `b` no elemento de nível superior, é necessário `write (/a/b/@c)[1]+1`. Além disso, uma palavra-chave DOCUMENT pode ser usada junto com uma coleção de esquemas XML.  
  
-   Algumas operações perdem informações de tipo durante a inferência. Por exemplo, se o tipo de um nó não pode ser determinado, ele se tornará **anyType**. Isso não é convertido implicitamente em qualquer outro tipo. Tais conversões ocorrem mais notavelmente durante a navegação usando o eixo pai. Você deve evitar o uso de tais operações e reescrever a consulta, se a expressão for criar um erro de tipo estático.  
  
## <a name="type-checking-of-union-types"></a>Verificação de tipo de tipos de união  
 Os tipos de união requerem o tratamento cuidadoso devido à verificação de tipo. São ilustrados dois dos problemas nos exemplos a seguir.  
  
### <a name="example-function-over-union-type"></a>Exemplo: função em relação ao tipo de união  
 Considere uma definição de elemento para <`r`> de um tipo de união:  
  
```  
<xs:element name="r">  
<xs:simpleType>  
   <xs:union memberTypes="xs:int xs:float xs:double"/>  
</xs:simpleType>  
</xs:element>  
```  
  
 No contexto do XQuery, a função "average" `fn:avg (//r)` retorna um erro estático, pois o compilador do XQuery não é possível adicionar valores de tipos diferentes (**xs: int**, **xs: float** ou **xs: duplo**) para o <`r`> elementos no argumento de **fn:avg()**. Para solucionar isso, reescreva a invocação de função como `fn:avg(for $r in //r return $r cast as xs:double ?)`.  
  
### <a name="example-operator-over-union-type"></a>Exemplo: operador em relação ao tipo de união  
 A operação de adição ('+') requer tipos precisos dos operandos. Como resultado, a expressão `(//r)[1] + 1` retorna um erro estático que tem a definição de tipo previamente descrita para o elemento <`r`>. Uma solução é reescrevê-la como `(//r)[1] cast as xs:int? +1`, onde o “?” " indica 0 ou 1 ocorrência. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] exige "cast as" com "?", pois qualquer conversão pode causar a sequência vazia como resultado de erros em tempo de execução.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
