---
title: Especificar caminhos e dicas de otimização para índices XML seletivos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 486ee339-165b-4aeb-b760-d2ba023d7d0a
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf5afdd80580bb3dde89a7f372b34b4ac7a67d11
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="specify-paths-and-optimization-hints-for-selective-xml-indexes"></a>Especificar caminhos e dicas de otimização para índices XML seletivos
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como especificar caminhos de nós a serem indexados e dicas de otimização de indexação ao criar ou alterar índices XML seletivos.  
  
 Especifique caminhos de nós e dicas de otimização ao mesmo tempo em uma das seguintes instruções:  
  
-   Na cláusula **FOR** de uma instrução **CREATE**. Para obter mais informações, veja [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md).  
  
-   Na cláusula **ADD** de uma instrução **ALTER**. Para obter mais informações, veja [ALTER INDEX &#40;Índices XML Seletivos&#41;](../../t-sql/statements/alter-index-selective-xml-indexes.md).  
  
 Para obter mais informações sobre índices XML seletivos, veja [Índices XML Seletivos &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md).  
  
##  <a name="untyped"></a> Noções básicas sobre tipos XQuery e tipos do SQL Server em XML não tipado  
 Os índices XML seletivos dão suporte a dois sistemas de tipos: tipos XQuery e tipos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O caminho indexado pode ser usado para corresponder a uma expressão XQuery ou para corresponder ao tipo de retorno do método value() do tipo de dados XML.  
  
-   Quando um caminho a ser indexado não é anotado, ou é anotado com a palavra-chave XQUERY, o caminho corresponde a uma expressão XQuery. Há duas variações para caminhos de nós anotados de XQUERY:  
  
    -   Se você não especificar a palavra-chave XQUERY e o tipo de dados XQuery, os mapeamentos padrão serão usados. Normalmente, o desempenho e o armazenamento não são os ideais.  
  
    -   Se você especificar a palavra-chave XQUERY e o tipo de dados XQuery e, opcionalmente, outras dicas de otimização, poderá obter o melhor desempenho possível e um armazenamento o mais eficiente possível. Entretanto, uma conversão pode falhar.  
  
-   Quando um caminho a ser indexado é anotado com a palavra-chave SQL, o caminho corresponde ao tipo de retorno do método value() do tipo de dados XML. Especifique o tipo de dados apropriado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que é o tipo de retorno esperado do método value().  
  
 Há diferenças sutis entre o sistema de tipos XML de expressões XQuery e o sistema de tipos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplicados ao método value() do tipo de dados XML. As principais diferenças incluem:  
  
-   O sistema de tipos XQuery reconhece os espaços à direita. Por exemplo, de acordo com a semântica do tipo XQuery, as cadeias de caracteres "abc" e "abc " não são iguais; já no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , essas cadeias são iguais.  
  
-   Os tipos de dados de ponto flutuante de XQuery dá suporte aos valores especiais +/- zero e +/- infinito. Esses valores especiais não têm suporte em tipos de dados de ponto flutuante do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="xquery-types-in-untyped-xml"></a>Tipos XQuery em XML não tipado  
  
-   Os tipos XQuery correspondem a expressões XQuery em todos os métodos do tipo de dados XML que inclui o método value().  
  
-   Os tipos XQuery dão suporte a estas dicas de otimização: node(), SINGLETON, DATA TYPE e MAXLENGTH.  
  
 Para expressões XQuery em XML não tipado, é possível escolher entre dois modos de operação:  
  
-   **Modo de mapeamento padrão**. Nesse modo, você especifica somente o caminho ao criar um índice XML seletivo.  
  
-   **Modo de mapeamento especificado pelo usuário**. Nesse modo, você especifica o caminho e as dicas de otimização opcionais.  
  
 O modo de mapeamento padrão usa uma opção de armazenamento conservadora, que é sempre segura e geral. Ela pode corresponder a qualquer tipo da expressão. Uma limitação do modo de mapeamento padrão é um desempenho abaixo do ideal, pois é necessário um maior número de conversões de tempo de execução, e os índices secundários não estão disponíveis.  
  
 Veja aqui um exemplo de índice XML seletivo criado com mapeamentos padrão. Para todos os três caminhos, o tipo de nó padrão (**xs:untypedAtomic**) e a cardinalidade são usados.  
  
```sql  
CREATE SELECTIVE XML INDEX example_sxi_UX_default  
ON Tbl(xmlcol)  
FOR  
(  
mypath01 =  '/a/b',  
mypath02 = '/a/b/c',  
mypath03 = '/a/b/d'  
)  
```  
  
 O modo de mapeamento especificado pelo usuário permite especificar um tipo e uma cardinalidade para que o nó obtenha melhor desempenho. Entretanto, esse desempenho aprimorado é obtido desistindo-se da segurança (pois uma conversão pode falhar) porque apenas o tipo especificado corresponde ao índice XML seletivo.  
  
 Os tipos XQuery com suporte para ocorrências XML não tipadas são:  
  
-   **xs:boolean**  
  
-   **xs:double**  
  
-   **xs:string**  
  
-   **xs:date**  
  
-   **xs:time**  
  
-   **xs:dateTime**  
  
 Se o tipo não for especificado, o nó será considerado do tipo de dados **xs:untypedAtomic** .  
  
 É possível otimizar o índice XML seletivo mostrado da seguinte maneira:  
  
```sql  
CREATE SELECTIVE XML INDEX example_sxi_UX_optimized  
ON Tbl(xmlcol)  
FOR  
(  
mypath= '/a/b' as XQUERY 'node()',  
pathX = '/a/b/c' as XQUERY 'xs:double' SINGLETON,  
pathY = '/a/b/d' as XQUERY 'xs:string' MAXLENGTH(200) SINGLETON  
)  
-- mypath – Only the node value is needed; storage is saved.  
-- pathX – Performance is improved; secondary indexes are possible.  
-- pathY - Performance is improved; secondary indexes are possible; storage is saved.  
```  
  
### <a name="sql-server-types-in-untyped-xml"></a>Tipos do SQL Server em XML não tipado  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os tipos correspondem ao valor retornado do método value().  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os tipos dão suporte a esta dica de otimização: SINGLETON.  
  
 É obrigatório especificar um tipo para caminhos que retornam tipos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Use o mesmo tipo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você usaria no método value().  
  
 Considere a consulta a seguir.  
  
```sql  
SELECT T.record,  
    T.xmldata.value('(/a/b/d)[1]', 'NVARCHAR(200)')  
FROM myXMLTable T  
```  
  
 A consulta especificada retorna um valor do caminho `/a/b/d` empacotado em um tipo de dados NVARCHAR(200); assim o tipo de dados a ser especificado para o nó é óbvio. Entretanto, não há nenhum esquema para especificar a cardinalidade do nó em XML não tipado. Para especificar que o nó `d` aparece no máximo uma vez no nó pai `b`, crie um índice XML seletivo que use a dica de otimização SINGLETON da seguinte maneira:  
  
```sql  
CREATE SELECTIVE XML INDEX example_sxi_US  
ON Tbl(xmlcol)  
FOR  
(  
node1223 = '/a/b/d' as SQL NVARCHAR(200) SINGLETON  
)  
```  
  
  
##  <a name="typed"></a> Noções básicas sobre suporte à índice XML seletivo para XML tipado  
 O XML tipado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é um esquema associado a determinado documento XML. O esquema define a estrutura geral do documento e tipos de nós. Se um esquema existe, o índice XML seletivo aplica a estrutura do esquema quando o usuário promove caminhos; assim, não há necessidade de especificar os tipos XQUERY para caminhos.  
  
 O índice XML seletivo dá suporte aos seguintes tipos XSD:  
  
-   **xs:anyUri**  
  
-   **xs:boolean**  
  
-   **xs:date**  
  
-   **xs:dateTime**  
  
-   **xs:day**  
  
-   **xs:decimal**  
  
-   **xs:double**  
  
-   **xs:float**  
  
-   **xs:int**  
  
-   **xs:integer**  
  
-   **xs:language**  
  
-   **xs:long**  
  
-   **xs:name**  
  
-   **xs:NCName**  
  
-   **xs:negativeInteger**  
  
-   **xs: nmtoken**  
  
-   **xs:nonNegativeInteger**  
  
-   **xs:nonPositiveInteger**  
  
-   **xs:positiveInteger**  
  
-   **xs:qname**  
  
-   **xs:short**  
  
-   **xs:string**  
  
-   **xs:time**  
  
-   **xs:token**  
  
-   **xs:unsignedByte**  
  
-   **xs:unsignedInt**  
  
-   **xs:unsignedLong**  
  
-   **xs:unsignedShort**  
  
 Quando o índice XML seletivo é criado em um documento que tem um esquema associado a ele, a especificação de um tipo XQUERY na criação ou alteração de índice retorna um erro. O usuário pode usar anotações do tipo SQL na parte de promoção de caminho. O tipo SQL deve ser uma conversão válida do tipo XSD definido no esquema, ou um erro será gerado. Todos os tipos SQL que têm representação adequada em XSD têm suporte, com exceção dos tipos de data/hora.  
  
> [!NOTE]  
>  O índice seletivo será usado se o tipo especificado na promoção de caminho do índice XML seletivo for igual ao valor de retorno do método value().  
  
 As seguintes dicas de otimização podem ser usadas com documentos XML tipados:  
  
-   Dica de otimização node().  
  
-   A dica de otimização MAXLENGTH pode ser usada com tipos xs:string para encurtar o valor indexado.  
  
 Para obter mais informações sobre dicas de otimização, consulte [Especificando dicas de otimização](#hints).  
  
##  <a name="paths"></a> Especificando caminhos  
 Um índice XML seletivo permite indexar somente um subconjunto de nós dos dados XML armazenados relevantes para as consultas que você pretende realizar. Quando o subconjunto de nós relevantes é muito menor que o número total de nós no documento XML, o índice XML seletivo armazena somente os nós relevantes. Para se beneficiar de um índice XML seletivo, identifique o subconjunto correto de nós para indexação.  
  
### <a name="choosing-the-nodes-to-index"></a>Escolhendo os nós a serem indexados  
 É possível usar os dois princípios simples a seguir para identificar o subconjunto correto de nós a ser adicionado a um índice XML seletivo.  
  
1.  **Princípio 1**: para avaliar determinada expressão XQuery, indexe todos os nós que você precisa examinar.  
  
    -   Indexe todos os nós cuja existência ou valor é usado na expressão XQuery.  
  
    -   Indexe todos os nós na expressão XQuery aos quais predicados XQuery são aplicados.  
  
     Considere a seguinte consulta simples no [documento XML de exemplo](#sample) neste tópico:  
  
    ```sql  
    SELECT T.record FROM myXMLTable T  
    WHERE T.xmldata.exist('/a/b[./c = "43"]') = 1  
    ```  
  
     Para retornar as instâncias XML compatíveis com essa consulta, um índice XML seletivo precisa examinar dois nós em cada instância XML:  
  
    -   Nó `c`, porque seu valor é usado na expressão XQuery.  
  
    -   Nó `b`, porque um predicado é aplicado ao nó`b` na expressão XQuery.  
  
2.  **Princípio 2**: para obter o melhor desempenho, indexe todos os nós necessários para avaliar determinada expressão XQuery. Se você indexar apenas alguns dos nós, o índice XML seletivo melhorará somente a avaliação de subexpressões que incluam nós indexados.  
  
 Para melhorar o desempenho da instrução SELECT mostrada acima, é possível criar o seguinte índice XML seletivo:  
  
```sql  
CREATE SELECTIVE XML INDEX simple_sxi  
ON Tbl(xmlcol)  
FOR  
(  
    path123 =  '/a/b',  
    path124 =  '/a/b/c'  
)  
```  
  
### <a name="indexing-identical-paths"></a>Indexando caminhos idênticos  
 Não é possível promover caminhos idênticos ao mesmo tipo de dados em nomes de caminho diferentes. Por exemplo, a consulta a seguir gera um erro, porque `pathOne` e `pathTwo` são idênticos:  
  
```sql  
CREATE SELECTIVE INDEX test_simple_sxi ON T1(xmlCol)  
FOR  
(  
    pathOne = 'book/authors/authorID' AS XQUERY 'xs:string',  
    pathTwo = 'book/authors/authorID' AS XQUERY 'xs:string'  
)  
```  
  
 Entretanto, é possível promover caminhos idênticos como tipos de dados diferentes com nomes diferentes. Por exemplo, agora a consulta a seguir é aceitável, porque os tipos de dados são diferentes:  
  
```sql  
CREATE SELECTIVE INDEX test_simple_sxi ON T1(xmlCol)  
FOR  
(  
    pathOne = 'book/authors/authorID' AS XQUERY 'xs:double',  
    pathTwo = 'book/authors/authorID' AS XQUERY 'xs:string'  
)  
```  
  
### <a name="examples"></a>Exemplos  
 Veja alguns exemplos adicionais de seleção de nós corretos a serem indexados para diferentes tipos XQuery.  
  
 **Exemplo 1**  
  
 Esta é uma XQuery simples que usa o método exist():  
  
```sql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b/c/d/e/h') = 1  
```  
  
 A tabela a seguir mostra os nós que devem ser indexados para permitir que essa consulta use o índice XML seletivo.  
  
|Nó a ser incluído no índice|Motivo para indexar este nó|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e/h**|A existência do nó `h` é avaliada no método exist().|  
  
 **Exemplo 2**  
  
 Esta é uma variação mais complexa da XQuery anterior, com um predicado aplicado:  
  
```sql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b/c/d/e[./f = "SQL"]') = 1  
```  
  
 A tabela a seguir mostra os nós que devem ser indexados para permitir que essa consulta use o índice XML seletivo.  
  
|Nó a ser incluído no índice|Motivo para indexar este nó|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|Um predicado é aplicado ao nó `e`.|  
|**/a/b/c/d/e/f**|O valor do nó `f` é avaliado no predicado.|  
  
 **Exemplo 3**  
  
 Esta é uma consulta mais complexa com uma cláusula value():  
  
```sql  
SELECT T.record,  
    T.xmldata.value('(/a/b/c/d/e[./f = "SQL"]/g)[1]', 'nvarchar(100)')  
FROM myXMLTable T  
```  
  
 A tabela a seguir mostra os nós que devem ser indexados para permitir que essa consulta use o índice XML seletivo.  
  
|Nó a ser incluído no índice|Motivo para indexar este nó|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|Um predicado é aplicado ao nó `e`.|  
|**/a/b/c/d/e/f**|O valor do nó `f` é avaliado no predicado.|  
|**/a/b/c/d/e/g**|O valor do nó `g` é retornado pelo método value().|  
  
 **Exemplo 4**  
  
 Veja aqui uma consulta que usa uma cláusula FLWOR em uma cláusula exist(). (O nome FLWOR vem das cinco cláusulas que podem formar uma expressão XQuery FLWOR: for, let, where, order by e return.)  
  
```sql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('  
  For $x in /a/b/c/d/e  
  Where $x/f = "SQL"  
  Return $x/g  
') = 1  
```  
  
 A tabela a seguir mostra os nós que devem ser indexados para permitir que essa consulta use o índice XML seletivo.  
  
|Nó a ser incluído no índice|Motivo para indexar este nó|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|A existência do nó `e` é avaliada na cláusula FLWOR.|  
|**/a/b/c/d/e/f**|O valor do nó `f` é avaliado na cláusula FLWOR.|  
|**/a/b/c/d/e/g**|A existência do nó `g` é avaliada pelo método exist().|  
  
  
##  <a name="hints"></a> Especificando dicas de otimização  
 Você pode usar dicas de otimização opcionais para especificar detalhes adicionais de mapeamento para um nó indexado por um índice XML seletivo. Por exemplo, você pode especificar o tipo de dados e a cardinalidade de um nó, bem como certas informações sobre a estrutura dos dados. Essas informações adicionais dão suporte a um melhor mapeamento. Também resultam em melhorias no desempenho ou economia no armazenamento, ou ambas.  
  
 O uso de dicas de otimização é opcional. Sempre é possível aceitar os mapeamentos padrão, que são confiáveis, mas que podem não proporcionar um desempenho e um armazenamento ideais.  
  
 Algumas dicas de otimização, por exemplo, a dica SINGLETON, apresentam restrições aos seus dados. Em alguns casos, erros podem ser gerados quando essas restrições não são atendidas.  
  
### <a name="benefits-of-optimization-hints"></a>Benefícios de dicas de otimização  
 A tabela a seguir identifica as dicas de otimização que dão suporte a um armazenamento mais eficiente ou a um melhor desempenho.  
  
|Dica de otimização|Armazenamento mais eficiente|Melhor desempenho|  
|-----------------------|----------------------------|--------------------------|  
|**node()**|Sim|não|  
|**SINGLETON**|não|Sim|  
|**DATA TYPE**|Sim|Sim|  
|**MAXLENGTH**|Sim|Sim|  
  
### <a name="optimization-hints-and-data-types"></a>Dicas e tipos de dados de otimização  
 É possível indexar nós como tipos de dados XQuery ou como tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A tabela a seguir mostra as dicas de otimização com suporte para cada tipo de dados.  
  
|Dica de otimização|Tipos de dados XQuery|Tipos de dados SQL|  
|-----------------------|-----------------------|--------------------|  
|**node()**|Sim|não|  
|**SINGLETON**|Sim|Sim|  
|**DATA TYPE**|Sim|não|  
|**MAXLENGTH**|Sim|não|  
  
### <a name="node-optimization-hint"></a>Dica de otimização node()  
 Aplica-se a: tipos de dados XQuery  
  
 Você pode usar a otimização node() para especificar um nó cujo valor não seja obrigatório para avaliar a consulta típica. Essa dica reduz os requisitos de armazenamento quando a consulta típica só precisa avaliar a existência do nó. (Por padrão, um índice XML seletivo armazena o valor de todos os nós promovidos, exceto de tipos de nós complexos.)  
  
 Considere o seguinte exemplo:  
  
```sql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b[./c=5]') = 1  
```  
  
 Para usar um índice XML seletivo para avaliar essa consulta, promova os nós `b` e `c`. Entretanto, como o valor do nó `b` não é obrigatório, você pode usar a dica node() com a seguinte sintaxe:  
  
 `/a/b/ as node()`  
  
 Se uma consulta exigir o valor de um nó que tenha sido indexado com a dica node(), o índice XML seletivo não poderá ser usado.  
  
### <a name="singleton-optimization-hint"></a>Dica de otimização SINGLETON  
 Aplica-se a: tipos de dados XQuery ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 A dica de otimização SINGLETON especifica a cardinalidade de um nó. Essa dica melhora o desempenho da consulta, pois sabe-se antecipadamente que um nó é exibido no máximo uma vez em seu pai ou ancestral.  
  
 Considere o [documento XML de exemplo](#sample) neste tópico.  
  
 Para usar um índice XML seletivo para consultar este documento, você pode especificar a dica SINGLETON para o nó `d` , pois ele aparece no máximo uma vez em seu pai.  
  
 Se a dica SINGLETON for especificada, mas um nó aparecer mais de uma vez em seu pai ou ancestral, um erro será gerado quando o índice for criado (de dados existentes) ou quando uma consulta for executada (de novos dados).  
  
### <a name="data-type-optimization-hint"></a>Dica de otimização DATA TYPE  
 Aplica-se a: tipos de dados XQuery  
  
 A dica de otimização CREATE DATABASE permite especificar um tipo de dados XQuery ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o nó indexado. O tipo de dados é usado para a coluna na tabela de dados do índice XML seletivo que corresponde ao nó indexado.  
  
 Quando a conversão de um valor existente no tipo de dados especificado falha, a operação de inserção (no índice) não falha; entretanto, um valor nulo é inserido na tabela de dados do índice.  
  
### <a name="maxlength-optimization-hint"></a>Dica de otimização MAXLENGTH  
 Aplica-se a: tipos de dados XQuery  
  
 A dica de otimização MAXLENGTH permite limitar o comprimento dos dados xs:string. MAXLENGTH não é relevante para tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , desde que você especifique o comprimento quando especificar os tipos de dados VARCHAR ou NVARCHAR.  
  
 Quando uma cadeia de caracteres existente é maior que MAXLENGTH especificado, a inserção desse valor no índice falha.  
  
  
##  <a name="sample"></a> Documento XML de exemplo  
 O documento XML de exemplo a seguir é referenciado nos exemplos deste tópico:  
  
```xml  
<a>  
    <b>  
         <c atc="aa">10</c>  
         <c atc="bb">15</c>  
         <d atd1="dd" atd2="ddd">md </d>  
    </b>  
     <b>  
        <c></c>  
        <c atc="">117</c>  
     </b>  
</a>  
```  
  
  
## <a name="see-also"></a>Consulte Também  
 [Índices XML Seletivos &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [Criar, alterar e remover índices XML seletivos](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)  
  
  
