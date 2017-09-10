---
title: "Contexto de expressão e avaliação de consulta (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- expression context [XQuery]
- XQuery, expression context
- XQuery, query evaluation
- static context
- dynamic context [XQuery]
ms.assetid: 5059f858-086a-40d4-811e-81fedaa18b06
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0aaa0fb28aa648018a4d9f562e5ac2452e0d2309
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="expression-context-and-query-evaluation-xquery"></a>Contexto de expressão e avaliação de consulta (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  O contexto de uma expressão é a informação usada para analisá-la e avaliá-la. A seguir há duas fases nas quais o XQuery é avaliado:  
  
-   **Contexto estático** – esta é a fase de compilação de consulta. Com base nas informações disponíveis, os erros às vezes ocorrem durante essa análise estática da consulta.  
  
-   **Contexto dinâmico** – esta é a fase de execução de consulta. Mesmo se uma consulta não tiver erros estáticos, como erros durante a compilação da consulta, a consulta poderá retornar erros durante sua execução.  
  
## <a name="static-context"></a>Contexto estático  
 A inicialização de contexto estático refere-se ao processo de reunir todas as informações para análise estática da expressão. Como parte da inicialização do contexto estático, o seguinte é completado:  
  
-   O **limite o espaço em branco** política é configurada para ser eliminada. Portanto, a boundary white space não é mantida pelo **qualquer elemento** e **atributo** construtores na consulta. Por exemplo:  
  
    ```  
    declare @x xml  
    set @x=''  
    select @x.query('<a>  {"Hello"}  </a>,  
  
        <b> {"Hello2"}  </b>')  
    ```  
  
     Esta consulta retorna o resultado a seguir, porque boundary space é retirado durante a análise da expressão XQuery:  
  
    ```  
    <a>Hello</a><b>Hello2</b>  
    ```  
  
-   O prefixo e a associação de namespace são inicializados para o seguinte:  
  
    -   Um conjunto de namespaces predefinidos.  
  
    -   Qualquer namespace definido usando WITH XMLNAMESPACES. Para obter mais informações, consulte [adicionar Namespaces a consultas com WITH XMLNAMESPACES](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)).  
  
    -   Qualquer namespace definido no prólogo da consulta. Observe que as declarações de namespace no prólogo podem substituir a declaração de namespace no WITH XMLNAMESPACES. Por exemplo, na consulta a seguir, WITH XMLNAMESPACES declara um prefixo (pd) que associa ao namespace (`http://someURI`). Entretanto, na cláusula WHERE, o prólogo da consulta substitui a associação.  
  
        ```  
        WITH XMLNAMESPACES ('http://someURI' AS pd)  
        SELECT ProductModelID, CatalogDescription.query('  
            <Product   
                ProductModelID= "{ sql:column("ProductModelID") }"   
                />  
        ') AS Result  
        FROM Production.ProductModel  
        WHERE CatalogDescription.exist('  
            declare namespace  pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
             /pd:ProductDescription[(pd:Specifications)]'  
            ) = 1  
        ```  
  
     Todas essas associações de namespace são resolvidas durante a inicialização de contexto estática.  
  
-   Se a consulta com um tipo **xml** coluna ou variável, os componentes da coleção de esquemas XML associada com a coluna ou variável são importados para o contexto estático. Para obter mais informações, consulte [Comparar XML digitado com XML não digitado](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
-   Para todo tipo atômico nos esquemas importados, uma função de conversão também se torna disponível no contexto estático. Isso é ilustrado no exemplo a seguir. Neste exemplo, uma consulta é especificada em relação a um tipo **xml** variável. A coleção de esquemas XML associada a essa variável define um tipo atômico, myType. Correspondendo a esse tipo, uma função de conversão, **myType()**, está disponível durante a análise estática. A expressão de consulta (`ns:myType(0)`) retorna um valor de myType.  
  
    ```  
    -- DROP XML SCHEMA COLLECTION SC  
    -- go  
    CREATE XML SCHEMA COLLECTION SC AS '<schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="myNS" xmlns:ns="myNS"  
    xmlns:s="http://schemas.microsoft.com/sqlserver/2004/sqltypes">  
          <import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
          <simpleType name="myType">  
                <restriction base="int">  
                 <enumeration value="0" />  
                  <enumeration value="1"/>  
                </restriction>  
          </simpleType>  
          <element name="root" type="ns:myType"/>  
    </schema>'  
    go  
  
    DECLARE @var XML(SC)  
    SET @var = '<root xmlns="myNS">0</root>'  
    -- specify myType() casting function in the query  
    SELECT @var.query('declare namespace ns="myNS"; ns:myType(0)')  
    ```  
  
     No exemplo a seguir, a função de conversão de **int** tipo XML interno é especificado na expressão.  
  
    ```  
    declare @x xml  
    set @x = ''  
    select @x.query('xs:int(5)')  
    go  
    ```  
  
 Depois que o contexto estático é inicializado, a expressão de consulta é analisada (compilada). A análise estática envolve o seguinte:  
  
1.  Análise de consulta.  
  
2.  Resolução dos nomes de tipo e função especificados na expressão.  
  
3.  Digitação estática da consulta. Isso garante que a consulta é do tipo seguro. Por exemplo, a consulta a seguir retorna um erro estático, pois o  **+**  operador requer argumentos de tipo primitivo numéricos:  
  
    ```  
    declare @x xml  
    set @x=''  
    SELECT @x.query('"x" + 4')  
    ```  
  
     No exemplo a seguir, o **Value ()** operador requer um singleton. Conforme especificado no esquema XML, pode haver vários \<Elem > elementos. A análise estática da expressão estabelece que não é de tipo seguro e um erro estático é retornado. Para resolver o erro, a expressão deve ser reescrita para especificar um singleton (`data(/x:Elem)[1]`) explicitamente.  
  
    ```  
    DROP XML SCHEMA COLLECTION SC  
    go  
    CREATE XML SCHEMA COLLECTION SC AS '<schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="myNS" xmlns:ns="myNS"  
    xmlns:s="http://schemas.microsoft.com/sqlserver/2004/sqltypes">  
          <import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
          <element name="Elem" type="string"/>  
    </schema>'  
    go  
  
    declare @x xml (SC)  
    set @x='<Elem xmlns="myNS">test</Elem><Elem xmlns="myNS">test2</Elem>'  
    SELECT @x.value('declare namespace x="myNS"; data(/x:Elem)[1]','varchar(20)')  
    ```  
  
     Para obter mais informações, consulte [XQuery e digitação estática](../xquery/xquery-and-static-typing.md).  
  
### <a name="implementation-restrictions"></a>Restrições de implementação  
 A seguir são apresentadas as limitações relacionadas ao contexto estático:  
  
-   Não há suporte para o modo de compatibilidade XPath.  
  
-   Para a construção XML, só há suporte para o modo de construção de tira. Essa é a configuração padrão. Portanto, o tipo do nó de elemento construído é **xdt: sem tipo** tipo e os atributos são do **XDT: untypedatomic** tipo.  
  
-   Só há suporte para o modo de ordenação ordenada.  
  
-   Só há suporte para a política de espaço de tira XML.  
  
-   Não há suporte para a funcionalidade de URI base.  
  
-   **Fn:doc()** não tem suporte.  
  
-   **Fn:Collection()** não tem suporte.  
  
-   O sinalizador estático do XQuery não é fornecido.  
  
-   O agrupamento associado a **xml** tipo de dados é usado. Este agrupamento sempre é definido como agrupamento Unicode Codepoint.  
  
## <a name="dynamic-context"></a>Contexto dinâmico  
 O contexto dinâmico refere-se a informações que devem estar disponíveis no momento que a expressão é executada. Além do contexto estático, as informações a seguir são inicializadas como parte do contexto dinâmico:  
  
-   O foco de expressão, como item de contexto, posição de contexto e tamanho de contexto, é inicializado como mostrado a seguir. Observe que todos esses valores podem ser substituídos pelo [método Nodes ()](../t-sql/xml/nodes-method-xml-data-type.md).  
  
    -   O **xml** tipo de dados define o item de contexto, o nó sendo processado para o nó de documento.  
  
    -   A posição de contexto, a posição do item de contexto relativo aos nós que são processados, é primeiro configurada como 1.  
  
    -   O tamanho de contexto, o número de itens na sequência sendo processada, é primeiro definido como 1, pois sempre há um nó de documento.  
  
### <a name="implementation-restrictions"></a>Restrições de implementação  
 A seguir são descritas as limitações relacionadas ao contexto dinâmico:  
  
-   O **data e hora atuais** funções de contexto, **fn:current-data**, **fn:current-tempo**, e **fn:current-dateTime**, não são com suporte.  
  
-   O **fuso horário implícito** é fixado como UTC + 0 e não pode ser alterado.  
  
-   O **fn:doc()** não há suporte para a função. Todas as consultas são executadas em **xml** colunas ou variáveis de tipo.  
  
-   O **fn:collection()** não há suporte para a função.  
  
## <a name="see-also"></a>Consulte também  
 [Fundamentos de XQuery](../xquery/xquery-basics.md)   
 [Comparar XML digitado com XML não digitado](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Coleções de esquemas XML &#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
