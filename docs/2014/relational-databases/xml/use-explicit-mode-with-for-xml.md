---
title: Usar o modo EXPLICIT com FOR XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- EXPLICIT FOR XML mode
- FOR XML clause, EXPLICIT mode
- FOR XML EXPLICIT mode
ms.assetid: 8b26e8ce-5465-4e7a-b237-98d0f4578ab1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e5972f4dfb9ad47b4017acf36df45098c11eceb2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48086376"
---
# <a name="use-explicit-mode-with-for-xml"></a>Usar o modo EXPLICIT com FOR XML
  Conforme descrito no tópico [Construindo XML usando FOR XML](../xml/for-xml-sql-server.md), os modos RAW e AUTO não fornecem muito controle sobre a forma do XML gerado de um resultado da consulta. No entanto o modo EXPLICIT fornece máxima flexibilidade para gerar o XML desejado de um resultado de consulta.  
  
 A consulta em modo EXPLICIT deve ser escrita de uma maneira específica para que as informações adicionais sobre o XML necessário, como aninhamento esperado no XML, sejam especificadas explicitamente como parte da consulta. Dependendo do XML solicitado, pode ser trabalhoso escrever consultas em modo EXPLICIT. Você pode descobrir que [Usando o modo PATH](../xml/use-path-mode-with-for-xml.md) com aninhamento é uma alternativa mais simples para escrever consultas em modo EXPLICIT.  
  
 Como você descreve o XML desejado como parte da consulta no modo EXPLICIT, você deve garantir que o XML gerado seja bem formado e válido.  
  
## <a name="rowset-processing-in-explicit-mode"></a>Processamento de conjunto de linhas modo EXPLICIT  
 O modo EXPLICIT transforma o conjunto de linhas resultante da execução de uma consulta em um documento XML. Para que o modo EXPLICIT produza o documento XML, o conjunto de linhas deve ter um formato específico. Isso exige que você escreva a consulta SELECT para produzir o conjunto de linhas, a **tabela universal**, com um formato específico para que a lógica de processamento possa produzir o XML desejado.  
  
 Primeiro, a consulta deve produzir as duas colunas de metadados a seguir:  
  
-   A primeira coluna deve fornecer o número da marca, o tipo de inteiro, do elemento atual, e o nome da coluna deve ser **Tag**. A consulta deve fornecer um número de marca exclusivo para cada elemento que será construído do conjunto de linhas.  
  
-   A segunda coluna deve fornecer um número de marca do elemento pai e esse nome de coluna deve ser **Parent**. Dessa maneira, as colunas Tag e Parent fornecem informações da hierarquia.  
  
 Esses valores de colunas de metadados, juntamente com as informações nos nomes das colunas, são usados para produzir o XML desejado. Observe que sua consulta deve fornecer nomes de coluna de uma maneira específica. Observe também que um 0 ou NULL na coluna **Parent** indica que o elemento correspondente não tem nenhum pai. O elemento é adicionado ao XML como um elemento de nível superior.  
  
 Para entender como a tabela universal gerada por uma consulta é processada na geração do resultado XML, assuma que você escreveu uma consulta que produz essa tabela universal:  
  
 ![Tabela universal de amostra](../../database-engine/media/xmlutable.gif "tabela universal de amostra")  
  
 Observe o seguinte sobre essa tabela universal:  
  
-   As primeiras duas colunas são **Tag** e **Parent** e são colunas de meta. Esses valores determinam a hierarquia.  
  
-   Os nomes de coluna são especificados de uma certa maneira, conforme descrito mais adiante neste tópico.  
  
-   Para gerar o XML dessa tabela universal, os dados nessa tabela são particionados verticalmente em grupos de colunas. O agrupamento é determinado com base no valor da **Tag** e nos nomes de coluna. Para construir XML, a lógica de processamento seleciona um grupo de colunas para cada linha e constrói um elemento. O seguinte se aplica neste exemplo:  
  
    -   Para o valor 1 da coluna **Tag** na primeira linha, as colunas cujos nomes incluem o mesmo número de marca, **Customer!1!cid** e **Customer!1!name** formam um grupo. Essas colunas são usadas para processar a linha e você pode ter observado que a forma do elemento gerado é <`Customer id=... name=...`>. O formato do nome da coluna é descrito neste tópico.  
  
    -   Para o valor 2 da coluna **Tag**, as colunas **Order!2!id** e **Order!2!date** formam um grupo que é usado para construir elementos, <`Order id=... date=... /`>.  
  
    -   Para linhas com valor 3 da coluna **Tag** valor 3, as colunas **OrderDetail!3!id!id** e **OrderDetail!3!pid!idref** formam um grupo. Cada uma dessas linhas gera um elemento, <`OrderDetail id=... pid=...`>, dessas colunas.  
  
-   Observe que para gerar a hierarquia de XML, as linhas são processadas em ordem. A hierarquia de XML é determinada conforme mostrado a seguir:  
  
    -   A primeira linha especifica valor 1 de **Tag** e valor NULL de **Parent**. Portanto, o elemento <`Customer`> correspondente é adicionado como um elemento de nível superior no XML.  
  
        ```  
        <Customer cid="C1" name="Janine">  
        ```  
  
    -   A segunda linha identifica valor 2 de **Tag** valor 1 de **Parent**. Portanto o elemento <`Order`> é adicionado como um filho do elemento <`Customer`>.  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
        ```  
  
    -   As próximas duas linhas identificam o valor 3 de **Tag** e o valor 2 de **Parent**. Portanto os dois elementos <`OrderDetail`> são adicionados como filhos do elemento <`Order`>.  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
              <OrderDetail id="OD1" pid="P1"/>  
              <OrderDetail id="OD2" pid="P2"/>  
        ```  
  
    -   A última linha identifica 2 como o número da **Tag** e 1 como o número da marca **Parent**. Portanto outro filho do elemento <`Order`> é adicionado ao elemento pai <`Customer`>.  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
              <OrderDetail id="OD1" pid="P1"/>  
              <OrderDetail id="OD2" pid="P2"/>  
           </Order>  
           <Order id="O2" date="3/29/1997">  
        </Customer>  
        ```  
  
 Para resumir, os valores nas colunas de meta **Tag** e **Parent**, as informações fornecidas na coluna names e a ordenação correta das linhas produzem o XML desejado quando o modo EXPLICIT é usado.  
  
### <a name="universal-table-row-ordering"></a>Ordenação de linhas da tabela universal  
 Para construir o XML, as linhas na tabela universal são processadas na ordem. Portanto para recuperar as instâncias filho corretas associadas ao pai, as linhas no conjunto de linhas devem ser ordenadas de forma que cada nó pai seja imediatamente seguido por seus filhos.  
  
## <a name="specifying-column-names-in-a-universal-table"></a>Especificando nomes de colunas em uma tabela universal  
 Ao escrever consultas em modo EXPLICIT , os nomes das colunas no conjunto de linhas resultante devem ser especificados usando esse formato. Eles fornecem informações de transformação incluindo nomes de elementos e atributos e outras informações adicionais, especificadas usando diretivas.  
  
 Esse é o formato geral:  
  
```  
  
ElementName!TagNumber!AttributeName!Directive  
```  
  
 Uma descrição das partes do formato é fornecida a seguir.  
  
 *ElementName*  
 É o identificador genérico resultante do elemento. Por exemplo, se **Customers** for especificado como *ElementName*, o elemento \<Customers> será gerado.  
  
 *TagNumber*  
 É um valor de marca exclusivo atribuído a um elemento. Esse valor, com a ajuda das duas colunas de metadados, **Tag** e **Parent**, determina o aninhamento dos elementos no XML resultante.  
  
 *AttributeName*  
 Fornece o nome do atributo a ser construído no *ElementName*especificado. Esse será o comportamento se *Directive* não for especificada.  
  
 Se *Directive* for especificada e for **xml**, **cdata**ou **element**, esse valor será usado para construir um filho de *ElementName*e o valor da coluna será adicionado a ele.  
  
 Se você especificar a *Directive*, o *AttributeName* poderá estar vazio. Por exemplo, ElementName!TagNumber!!Directive. Nesse caso, o valor da coluna será contido diretamente pelo *ElementName*.  
  
 *Directive*  
 *Directive* é opcional e você pode usá-la para fornecer informações adicionais para construção do XML. *Directive* tem dois propósitos.  
  
 Um dos propósitos é codificar valores como ID, IDREF e IDREFS. É possível especificar as palavras-chave **ID**, **IDREF**e **IDREFS** como *Directives*. Essas diretivas substituem os tipos de atributo. Isso permite criar vínculos intradocumento.  
  
 Também é possível usar *Directive* para indicar como mapear os dados de cadeia de caracteres para XML. É possível usar as palavras-chave **hide**, **element, elementxsinil**, **xml**, **xmltext**e **cdata** como a *Directive*. A diretiva **hide** oculta o nó. Isso é útil para recuperar valores apenas para fins de classificação, mas não para tê-los no XML resultante.  
  
 A diretiva **element** gera um elemento contido em vez de um atributo. Os dados contidos são codificados como uma entidade. Por exemplo, o caractere **<** se torna &lt;. Nenhum elemento é gerado para valores NULL da coluna. Se você quiser um elemento gerado para obter valores de coluna nulos, poderá especificar a diretiva **elementxsinil** . Isso gerará um elemento que tem o atributo xsi:nil=TRUE.  
  
 A diretiva **xml** é igual a uma diretiva **element** , exceto que não ocorre nenhuma codificação de entidade. Observe que a diretiva **element** pode ser combinada com **ID**, **IDREF**ou **IDREFS**, enquanto que a diretiva **xml** não é permitida com nenhuma outra diretiva, exceto **hide**.  
  
 A diretiva **cdata** contém os dados encapsulando-os com uma seção CDATA. O conteúdo não é codificado pela entidade. O tipo de dados original deve ser um tipo de texto como **varchar**, **nvarchar**, **text**ou **ntext**. Essa diretiva pode ser usada apenas com **hide**. Quando essa diretiva é usada, *AttributeName* não deve ser especificado.  
  
 A combinação de diretivas entre esses dois grupos é permitida na maioria dos casos, mas a combinação entre elas mesmas não é permitida.  
  
 Se *Directive* e *AttributeName* não forem especificados, por exemplo, **Customer!1**, uma diretiva de **element** será implícita, como **Customer!1!!element**, e os dados da coluna serão contidos no *ElementName*.  
  
 Se a diretiva **xmltext** for especificada, o conteúdo da coluna será encapsulado em uma marca única que é integrada com o restante do documento. Essa diretiva é útil para buscar dados XML armazenados, excedentes e não consumidos em uma coluna por OPENXML. Para obter mais informações, veja [OPENXML &#40;SQL Server&#41;](../xml/openxml-sql-server.md).  
  
 Se o *AttributeName* for especificado, o nome da marca será substituído pelo nome especificado. Caso contrário, o atributo será anexado à lista de atributos atual dos elementos circunscritos colocando o conteúdo no início do confinamento sem codificação de entidade. A coluna com essa diretiva deve ser de um tipo de texto, como **varchar**, **nvarchar**, **char**, **nchar**, **text**ou **ntext**. Essa diretiva pode ser usada apenas com **hide**. Essa diretiva é útil para buscar dados excedentes armazenados em uma coluna. Se o conteúdo não for um XML bem formado, o comportamento será indefinido.  
  
## <a name="in-this-section"></a>Nesta seção  
 Os exemplos a seguir ilustram o uso do modo EXPLICIT.  
  
-   [Exemplo: Recuperando informações de funcionários](../xml/example-retrieving-employee-information.md)  
  
-   [Exemplo: Especificando a diretiva ELEMENT](../xml/example-specifying-the-element-directive.md)  
  
-   [Exemplo: Especificando a diretiva ELEMENTXSINIL](../xml/example-specifying-the-elementxsinil-directive.md)  
  
-   [Exemplo: Construindo irmãos com o modo EXPLICIT](../xml/example-constructing-siblings-with-explicit-mode.md)  
  
-   [Exemplo: Especificando as diretivas ID e IDREF](../xml/example-specifying-the-id-and-idref-directives.md)  
  
-   [Exemplo: Especificando as diretivas ID e IDREFS](../xml/example-specifying-the-id-and-idrefs-directives.md)  
  
-   [Exemplo: Especificando a diretiva HIDE](../xml/example-specifying-the-hide-directive.md)  
  
-   [Exemplo: Especificando a diretiva ELEMENT e codificação de entidade](../xml/example-specifying-the-element-directive-and-entity-encoding.md)  
  
-   [Exemplo: Especificando a diretiva CDATA](../xml/example-specifying-the-cdata-directive.md)  
  
-   [Exemplo: Especificando a diretiva XMLTEXT](../xml/example-specifying-the-xmltext-directive.md)  
  
## <a name="see-also"></a>Consulte também  
 [Usar modo RAW com FOR XML](../xml/use-raw-mode-with-for-xml.md)   
 [Usar o modo AUTO com FOR XML](../xml/use-auto-mode-with-for-xml.md)   
 [Usar o modo PATH com FOR XML](../xml/use-path-mode-with-for-xml.md)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [FOR XML &#40;SQL Server&#41;](../xml/for-xml-sql-server.md)  
  
  
