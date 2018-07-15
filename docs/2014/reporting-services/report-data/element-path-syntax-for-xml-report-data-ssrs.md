---
title: Sintaxe do caminho do elemento para dados de relatório XML (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ElementPath syntax
- XML [Reporting Services], data retrieval
ms.assetid: 07bd7a4e-fd7a-4a72-9344-3258f7c286d1
caps.latest.revision: 42
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: bcb0036fbf6d0c3f5af18d044d389bc8673cd5ce
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37238488"
---
# <a name="element-path-syntax-for-xml-report-data-ssrs"></a>Sintaxe do caminho do elemento para dados de relatório XML (SSRS)
  No Designer de Relatórios, você especifica os dados para uso em um relatório de uma fonte de dados XML definindo um caminho do elemento que faz distinção entre maiúsculas e minúsculas. Um caminho de elemento indica como transpor os nós hierárquicos XML e seus atributos na fonte de dados XML. Para usar o caminho do elemento padrão, deixe a consulta do conjunto de dados ou o `ElementPath` XML da `Query` XML vazio. Quando os dados são recuperados da fonte de dados XML, os nós do elemento que possuem valores de texto e os atributos do nó do elemento se tornam colunas no conjunto de resultados. Os valores dos nós e atributos tornam-se os dados da linha quando a consulta é executada. As colunas são exibidas como a coleção de campos do conjunto de dados no painel de dados do relatório. Este tópico descreve a sintaxe do caminho do elemento.  
  
> [!NOTE]  
>  A sintaxe do caminho do elemento é independente do namespace. Para usar namespaces em um caminho de elemento, use a sintaxe de consulta XML que inclui um XML `ElementPath` elemento descrito na [sintaxe de consulta XML para dados de relatório XML &#40;SSRS&#41;](report-data-ssrs.md).  
  
 A tabela a seguir descreve as convenções usadas para definir um caminho de elemento.  
  
|Convenção|Usado para|  
|----------------|--------------|  
|**bold**|Texto que deve ser digitado exatamente como mostrado.|  
|&#124; (barra vertical)|Separa itens de sintaxe. Somente um desses itens poderá ser selecionado.|  
|`[ ] (brackets)`|Itens de sintaxe opcionais. Não digite os colchetes.|  
|**{ }** (chaves)|Delimita parâmetros de itens de sintaxe.|  
|[**,**...*n*]|Indica que o item precedente pode ser repetido *n* vezes. As ocorrências são separadas por vírgulas.|  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Element path ::=  
    ElementNode[/Element path]  
ElementNode ::=  
    XMLName[(Encoding)][{[FieldList]}]  
XMLName ::=  
    [NamespacePrefix:]XMLLocalName  
Encoding ::=  
        HTMLEncoded | Base64Encoded  
FieldList ::=  
    Field[,FieldList]  
Field ::=  
    Attribute | Value | Element | ElementNode  
Attribute ::=  
        @XMLName[(Type)]  
Value ::=  
        @[(Type)]  
Element ::=  
    XMLName[(Type)]  
Type ::=  
        String | Integer | Boolean | Float | Decimal | Date | XML   
NamespacePrefix ::=  
    Identifier that specifies the namespace.  
XMLLocalName :: =  
    Identifier in the XML tag.   
```  
  
## <a name="remarks"></a>Remarks  
 A tabela a seguir resume os termos do caminho do elemento. Os exemplos na tabela referem-se ao documento XML de exemplo Customers.xml, que está incluído na seção Exemplos deste tópico.  
  
> [!NOTE]  
>  As marcas XML diferenciam maiúsculas de minúsculas. Ao especificar um ElementNode no caminho do elemento, você deve corresponder exatamente as marcas XML na fonte de dados.  
  
|Termo|Definição|  
|----------|----------------|  
|Caminho do elemento|Define a sequência de nós a serem transpostos dentro do documento XML para recuperar dados do campo para um conjunto de dados com uma fonte de dados XML.|  
|`ElementNode`|O nó XML no documento XML. Os nós são designados por marcas e existem em uma relação hierárquica com outros nós. Por exemplo, \<Clientes> é o nó do elemento raiz. \<Cliente> é um subelemento de \<Clientes>.|  
|`XMLName`|O nome do nó. Por exemplo, o nome do nó Clientes é Clientes. Um `XMLName` pode ser prefixado com um identificador de namespace para nomear exclusivamente cada nó.|  
|`Encoding`|Indica que o `Value` deste elemento é XML codificado e precisa ser decodificado e incluído como um subelemento desse elemento.|  
|`FieldList`|Define o conjunto de elementos e atributos a serem usados para recuperar dados.<br /><br /> Se não estiverem especificados, todos os atributos e subelementos serão usados como campos. Se a lista de campos vazia for especificada (**{}**), nenhum campo deste nó será usado.<br /><br /> Um `FieldList` não pode conter tanto um `Value` e uma `Element` ou `ElementNode`.|  
|`Field`|Especifica os dados recuperados como um campo do conjunto de dados.|  
|`Attribute`|Um par nome-valor dentro de `ElementNode`. Por exemplo, no nó do elemento \<Customer ID = "1" >, `ID` é um atributo e `@ID(Integer)` retorna "1" com um tipo inteiro no campo de dados correspondente `ID`.|  
|`Value`|O valor do elemento. `Value` pode ser usado apenas no último `ElementNode` no caminho do elemento. Por exemplo, porque \<retornar > é um nó folha, se ele for incluído no final de um caminho de elemento, o valor da `Return {@}` é `Chair`.|  
|`Element`|O valor do subelemento nomeado. Por exemplo, Clientes {}/Cliente {}/Sobrenome recupera valores apenas para o elemento Sobrenome.|  
|`Type`|O tipo de dados opcional a ser usado para o campo criado desse elemento.|  
|`NamespacePrefix`|O `NamespacePrefix` é definido no elemento Consulta XML. Se nenhum elemento consulta XML existir, os namespaces no XML `ElementPath` são ignorados. Se existir um elemento Consulta XML, o `ElementPath` XML terá um atributo opcional `IgnoreNamespaces`. Se IgnoreNamespaces for `true`, namespaces no XML `ElementPath` e o documento XML serão ignorados. Para obter mais informações, consulte [Sintaxe de consulta XML para dados de relatório XML &#40;SSRS&#41;](report-data-ssrs.md).|  
  
## <a name="example---no-namespaces"></a>Exemplo – Nenhum namespace  
 Os exemplos a seguir usam o documento XML Customers.xml. Esta tabela mostra exemplos de sintaxe do caminho do elemento e os resultados do uso do caminho do elemento em uma consulta que define um conjunto de dados, baseado no documento XML como uma fonte de dados.  
  
 Observe que, quando o caminho do elemento está vazio, a consulta usa o caminho do elemento padrão: o primeiro caminho para uma coleção de nós folha. No primeiro exemplo, deixar o caminho do elemento vazio é equivalente a especificar o caminho do elemento /Clientes/Cliente/Pedidos/Pedido. Todos os valores e atributos do nó ao longo do caminho são retornados no conjunto de resultados, e os nomes de nós e de atributos são exibidos como campos do conjunto de dados.  
  
-   *Empty (vazio)*  
  
    |Order|Qty|ID|FirstName|LastName|Customer.ID|xmlns|  
    |-----------|---------|--------|---------------|--------------|-----------------|-----------|  
    |Chair|6|1|Bobby|Moore|11|http://www.adventure-works.com|  
    |Table|1|2|Bobby|Moore|11|http://www.adventure-works.com|  
    |Sofa|2|8|Crystal|Hu|20|http://www.adventure-works.com|  
    |EndTables|2|15|Wyatt|Diaz|33|http://www.adventure-works.com|  
  
-   `Customers {}/Customer`  
  
    |FirstName|LastName|ID|  
    |---------------|--------------|--------|  
    |Bobby|Moore|11|  
    |Crystal|Hu|20|  
    |Wyatt|Diaz|33|  
  
-   `Customers {}/Customer {}/LastName`  
  
    |LastName|  
    |--------------|  
    |Moore|  
    |Hu|  
    |Diaz|  
  
-   `Customers {}/Customer {}/Orders/Order {@,@Qty}`  
  
    |Order|Qty|  
    |-----------|---------|  
    |Chair|6|  
    |Table|1|  
    |Sofa|2|  
    |EndTables|2|  
  
-   `Customers {}/Customer/Orders/Order{ @ID(Integer)}`  
  
    |Order.ID|FirstName|LastName|ID|  
    |--------------|---------------|--------------|--------|  
    |1|Bobby|Moore|11|  
    |2|Bobby|Moore|11|  
    |8|Crystal|Hu|20|  
    |15|Wyatt|Diaz|33|  
  
#### <a name="xml-document-customersxml"></a>Documento XML: Customers.xml  
 Para tentar os exemplos de caminhos de elementos na seção anterior, você pode copiar esse XML e salvá-lo em uma URL acessível pelo Designer de Relatórios e, em seguida, usar o documento XML como uma fonte de dados: por exemplo, `http://localhost/Customers.xml`.  
  
```  
<?xml version="1.0"?>  
<Customers xmlns="http://www.adventure-works.com">  
   <Customer ID="11">  
      <FirstName>Bobby</FirstName>  
      <LastName>Moore</LastName>  
      <Orders>  
         <Order ID="1" Qty="6">Chair</Order>  
         <Order ID="2" Qty="1">Table</Order>  
      </Orders>  
      <Returns>  
         <Return ID="1" Qty="2">Chair</Return>  
      </Returns>  
   </Customer>  
   <Customer ID="20">  
      <FirstName>Crystal</FirstName>  
      <LastName>Hu</LastName>  
      <Orders>  
         <Order ID="8" Qty="2">Sofa</Order>  
      </Orders>  
      <Returns/>  
   </Customer>  
   <Customer ID="33">  
      <FirstName>Wyatt</FirstName>  
      <LastName>Diaz</LastName>  
      <Orders>  
         <Order ID="15" Qty="2">EndTables</Order>  
      </Orders>  
      <Returns/>  
   </Customer>  
</Customers>  
```  
  
 Como alternativa, é possível criar uma fonte de dados XML que não possui nenhuma cadeia de conexão e inserir Customers.XML na consulta, usando o seguinte procedimento:  
  
###### <a name="to-embed-customersxml-in-a-query"></a>Para inserir Customers.XML em um consulta  
  
1.  Crie uma fonte de dados XML com uma cadeia de conexão em branco.  
  
2.  Crie um novo conjunto de dados para a fonte de dados XML.  
  
3.  Na caixa de diálogo **Propriedades do Conjunto de Dados** , clique em **Designer de Consulta**. A caixa de diálogo do Designer de Consulta baseada em texto é aberta.  
  
4.  No painel de consulta, digite as duas linhas a seguir:  
  
     `<Query>`  
  
     `<XmlData>`  
  
5.  Copie Customers.XML e cole o texto no painel de consulta depois de `<XmlData>`.  
  
6.  No painel de consulta, exclua a primeira linha que você copiou de Customers.XML: `<?xml version="1.0"?>`  
  
7.  No final da consulta, adicione as duas linhas seguintes:  
  
     `<XmlData>`  
  
     `<Query>`  
  
8.  Clique em **Executar consulta** (!).  
  
     O conjunto de resultados exibe 4 linhas de dados com as seguintes colunas: `xmlns`, `Customer.ID`, `FirstName`, `LastName`, `ID`, `Qty`, `Order`.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de conexão XML &#40;SSRS&#41;](xml-connection-type-ssrs.md)   
 [Tutoriais do Reporting Services &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)   
 [Adicionar, editar e atualizar campos no painel de dados do relatório &#40;Construtor de Relatórios e SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)  
  
  
