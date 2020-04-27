---
title: 'Especificando a profundidade em relações recursivas usando SQL: Max-Depth | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- max-depth annotation
- XPath queries [SQLXML], recursive relationships
- depth in recursive relationships [SQLXML]
- annotated XSD schemas, recursive relationships
- relationships [SQLXML], recursive relationships
- self joins
- recursive relationships [SQLXML]
- recursion [SQLXML]
- sql:max-depth
- recursive joins [SQLXML]
ms.assetid: 0ffdd57d-dc30-44d9-a8a0-f21cadedb327
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b247efb895f037965620c7430a3dc41c33fe550
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66013653"
---
# <a name="specifying-depth-in-recursive-relationships-by-using-sqlmax-depth"></a>Especificando a profundidade em relações recursivas usando sql:max-depth
  Em bancos de dados relacionais, quando uma tabela está envolvida em uma relação com si mesma, a relação é chamada de relação recursiva. Por exemplo, em uma relação supervisor-supervisionado, uma tabela que armazena os registros dos funcionários está envolvida em uma relação com si mesma. Nesse caso, a tabela de funcionários desempenha a função de supervisor em um lado da relação e a mesma tabela desempenha a função de supervisionado no outro lado.  
  
 O mapeamento de esquemas pode incluir relações recursivas, em que um elemento e seu ancestral são do mesmo tipo.  
  
## <a name="example-a"></a>Exemplo A  
 Considere a seguinte tabela:  
  
```  
Emp (EmployeeID, FirstName, LastName, ReportsTo)  
```  
  
 Nessa tabela, a coluna ReportsTo armazena a ID de funcionário do gerente.  
  
 Suponha que você deseje gerar uma hierarquia XML de funcionários na qual o funcionário gerente esteja no topo da hierarquia e na qual os funcionários subordinados a esse gerente apareçam na hierarquia correspondente como mostrado no exemplo de fragmento XML a seguir. O que este fragmento mostra é a *árvore recursiva* para o funcionário 1.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Emp FirstName="Nancy" EmployeeID="1" LastName="Devolio">  
     <Emp FirstName="Andrew" EmployeeID="2" LastName="Fuller" />   
     <Emp FirstName="Janet" EmployeeID="3" LastName="Leverling">  
        <Emp FirstName="Margaret" EmployeeID="4" LastName="Peacock">  
          <Emp FirstName="Steven" EmployeeID="5" LastName="Devolio">  
...  
...  
</root>  
```  
  
 Nesse fragmento, o funcionário 5 está subordinado ao funcionário 4, o funcionário 4 está subordinado ao funcionário 3 e os funcionários 3 e 2 estão subordinados ao funcionário 1.  
  
 Para gerar esse resultado, você pode usar o esquema XSD a seguir e especificar uma consulta XPath para ele. O esquema descreve um ** \<elemento de>EMP** do tipo EmployeeType, que consiste em um ** \<elemento filho EMP>** do mesmo tipo, EmployeeType. Essa é uma relação recursiva (o elemento e seu ancestral são do mesmo tipo). Além disso, o esquema usa uma ** \<relação de SQL:>** para descrever a relação pai-filho entre o supervisor e o Supervisionador. Observe que neste ** \<SQL: relationship>**, EMP é o pai e a tabela filho.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"  
                                  parent="Emp"  
                                  parent-key="EmployeeID"  
                                  child="Emp"  
                                  child-key="ReportsTo" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp" type="EmployeeType"   
                          sql:relation="Emp"   
                          sql:key-fields="EmployeeID"   
                          sql:limit-field="ReportsTo" />  
  <xsd:complexType name="EmployeeType">  
    <xsd:sequence>  
      <xsd:element name="Emp" type="EmployeeType"   
                              sql:relation="Emp"   
                              sql:key-fields="EmployeeID"  
                              sql:relationship="SupervisorSupervisee"  
                              sql:max-depth="6" />  
    </xsd:sequence>   
    <xsd:attribute name="EmployeeID" type="xsd:ID" />  
    <xsd:attribute name="FirstName" type="xsd:string"/>  
    <xsd:attribute name="LastName" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:schema>  
```  
  
 Como a relação é recursiva, você precisa de algum modo de especificar a profundidade de recursão no esquema. Caso contrário, o resultado será uma recursão infinita (funcionário subordinado a funcionário subordinado a funcionário e assim por diante). A anotação `sql:max-depth` permite especificar o nível de profundidade da recursão. Nesse exemplo específico, para especificar um valor para `sql:max-depth`, você precisa saber o nível de profundidade da hierarquia de gerenciamento na empresa.  
  
> [!NOTE]  
>  O esquema especifica a anotação `sql:limit-field`, mas não especifica a anotação `sql:limit-value`. Isso limita o nó superior da hierarquia resultante apenas aos funcionários que não estão subordinados a ninguém. (Reportto é nulo.) Especificar `sql:limit-field` e não especificar `sql:limit-value` (que usa como padrão nulo) a anotação realiza isso. Se você desejar que o XML resultante inclua todas as árvores de subordinação (a árvore de subordinação de cada funcionário da tabela), remova a anotação `sql:limit-field` do esquema.  
  
> [!NOTE]  
>  O procedimento a seguir usa o banco de dados tempdb.  
  
#### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para testar uma consulta XPath de exemplo com relação ao esquema  
  
1.  Crie uma tabela de exemplo chamada Emp no banco de dados tempdb para o qual a raiz virtual aponta.  
  
    ```  
    USE tempdb  
    CREATE TABLE Emp (  
           EmployeeID int primary key,   
           FirstName  varchar(20),   
           LastName   varchar(20),   
           ReportsTo int)  
    ```  
  
2.  Adicione estes dados de exemplo:  
  
    ```  
    INSERT INTO Emp values (1, 'Nancy', 'Devolio',NULL)  
    INSERT INTO Emp values (2, 'Andrew', 'Fuller',1)  
    INSERT INTO Emp values (3, 'Janet', 'Leverling',1)  
    INSERT INTO Emp values (4, 'Margaret', 'Peacock',3)  
    INSERT INTO Emp values (5, 'Steven', 'Devolio',4)  
    INSERT INTO Emp values (6, 'Nancy', 'Buchanan',5)  
    INSERT INTO Emp values (7, 'Michael', 'Suyama',6)  
    ```  
  
3.  Copie o código de esquema acima e cole-o em um arquivo de texto. Salve o arquivo como maxDepth.xml.  
  
4.  Copie o modelo a seguir e cole-o em um arquivo de texto. Salve o arquivo como maxDepthT.xml no mesmo diretório onde você salvou maxDepth.xml. A consulta no modelo retorna todos os funcionários na tabela Emp.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="maxDepth.xml">  
        /Emp  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho de diretório especificado para o esquema de mapeamento (maxDepth.xml) é relativo ao diretório onde o modelo está salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\MyDir\maxDepth.xml"  
    ```  
  
5.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo. Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este é o resultado:  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Emp FirstName="Nancy" EmployeeID="1" LastName="Devolio">  
  <Emp FirstName="Andrew" EmployeeID="2" LastName="Fuller" />   
    <Emp FirstName="Janet" EmployeeID="3" LastName="Leverling">  
      <Emp FirstName="Margaret" EmployeeID="4" LastName="Peacock">  
        <Emp FirstName="Steven" EmployeeID="5" LastName="Devolio">  
          <Emp FirstName="Nancy" EmployeeID="6" LastName="Buchanan">  
            <Emp FirstName="Michael" EmployeeID="7" LastName="Suyama" />   
          </Emp>  
        </Emp>  
      </Emp>  
    </Emp>  
  </Emp>  
</root>  
```  
  
> [!NOTE]  
>  Para produzir profundidades diferentes de hierarquias no resultado, altere o valor da anotação `sql:max-depth` no esquema e execute o modelo novamente após cada alteração.  
  
 No esquema anterior, todos os elementos de ** \<>EMP** tinham exatamente o mesmo conjunto de atributos (**EmployeeID**, **FirstName**e **LastName**). O esquema a seguir foi ligeiramente modificado para retornar um atributo **reportes** adicional para todos os elementos de ** \<>EMP** que se reportam a um gerente.  
  
 Por exemplo, este fragmento XML mostra os subordinados do funcionário 1:  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
<Emp FirstName="Nancy" EmployeeID="1" LastName="Devolio">  
  <Emp FirstName="Andrew" EmployeeID="2"   
       ReportsTo="1" LastName="Fuller" />   
  <Emp FirstName="Janet" EmployeeID="3"   
       ReportsTo="1" LastName="Leverling">  
...  
...  
```  
  
 Este é o esquema revisado:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:documentation>  
      Customer-Order-Order Details Schema  
      Copyright 2000 Microsoft. All rights reserved.  
    </xsd:documentation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"   
                  parent="Emp"  
                  parent-key="EmployeeID"  
                  child="Emp"  
                  child-key="ReportsTo" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp"   
                   type="EmpType"   
                   sql:relation="Emp"   
                   sql:key-fields="EmployeeID"   
                   sql:limit-field="ReportsTo" />  
  <xsd:complexType name="EmpType">  
    <xsd:sequence>  
       <xsd:element name="Emp"   
                    type="EmpType"   
                    sql:relation="Emp"   
                    sql:key-fields="EmployeeID"  
                    sql:relationship="SupervisorSupervisee"  
                    sql:max-depth="6"/>  
    </xsd:sequence>   
    <xsd:attribute name="EmployeeID" type="xsd:int" />  
    <xsd:attribute name="FirstName" type="xsd:string"/>  
    <xsd:attribute name="LastName" type="xsd:string"/>  
    <xsd:attribute name="ReportsTo" type="xsd:int" />  
  </xsd:complexType>  
</xsd:schema>  
```  
  
## <a name="sqlmax-depth-annotation"></a>Anotação sql:max-depth  
 Em um esquema que consiste em relações recursivas, a profundidade de recursão deve ser especificada explicitamente no esquema. Isso é necessário para gerar, com êxito, a consulta FOR XML EXPLICIT correspondente que retorna os resultados solicitados.  
  
 Use a anotação `sql:max-depth` no esquema para especificar a profundidade de recursão em uma relação recursiva que é descrita no esquema. O valor da anotação `sql:max-depth` é um inteiro positivo (de 1 a 50) que indica o número de recursões: um valor de 1 para a recursão no elemento para o qual a anotação `sql:max-depth` está especificada; um valor de 2 para a recursão no nível seguinte do elemento no qual `sql:max-depth` está especificada e assim por diante.  
  
> [!NOTE]  
>  Na implementação subjacente, uma consulta XPath especificada em um esquema de mapeamento é convertida em SELECT... Consulta FOR XML EXPLICIT. Essa consulta requer que você especifique uma profundidade finita de recursão. Quanto mais alto for o valor especificado para `sql:max-depth`, maior será a consulta FOR XML EXPLICIT que será gerada. Isso poderá pode tornar mais lenta a recuperação.  
  
> [!NOTE]  
>  Updategrams e o Carregamento em Massa de XML ignoram a anotação max-depth. Isso significa que atualizações ou inserções recursivas acontecerão, independentemente do valor especificado para max-depth.  
  
## <a name="specifying-sqlmax-depth-on-complex-elements"></a>Especificando sql:max-depth em elementos complexos  
 A anotação `sql:max-depth` pode ser especificada em qualquer elemento de conteúdo complexo.  
  
### <a name="recursive-elements"></a>Elementos recursivos  
 Se `sql:max-depth` for especificada no elemento pai e no elemento filho em uma relação recursiva, a anotação `sql:max-depth` especificada no pai terá precedência. Por exemplo, no esquema a seguir, a anotação `sql:max-depth` é especificada nos elementos funcionários pai e filho. Nesse caso, `sql:max-depth=4`, especificado no elemento pai ** \<EMP>** (desempenhando uma função de supervisor), tem precedência. O `sql:max-depth` especificado no elemento ** \<>EMP** filho (desempenhando uma função de supervisionar) é ignorado.  
  
#### <a name="example-b"></a>Exemplo B  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"  
                                  parent="Emp"  
                                  parent-key="EmployeeID"  
                                  child="Emp"  
                                  child-key="ReportsTo" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp" type="EmployeeType"   
                          sql:relation="Emp"   
                          sql:key-fields="EmployeeID"   
                          sql:limit-field="ReportsTo"   
                          sql:max-depth="3" />  
  <xsd:complexType name="EmployeeType">  
    <xsd:sequence>  
      <xsd:element name="Emp" type="EmployeeType"   
                              sql:relation="Emp"   
                              sql:key-fields="EmployeeID"  
                              sql:relationship="SupervisorSupervisee"  
                              sql:max-depth="2" />  
    </xsd:sequence>   
    <xsd:attribute name="EmployeeID" type="xsd:ID" />  
    <xsd:attribute name="FirstName" type="xsd:string"/>  
    <xsd:attribute name="LastName" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:schema>  
```  
  
 Para testar esse esquema, siga as etapas fornecidas para o exemplo A, anteriormente neste tópico.  
  
### <a name="nonrecursive-elements"></a>Elementos não recursivos  
 Se a anotação `sql:max-depth` for especificada em um elemento do esquema que não causa nenhuma recursão, ela será ignorado. No esquema a seguir, um ** \<elemento de>EMP** consiste em uma ** \<constante>** elemento filho, que, por sua vez, tem um ** \<elemento filho EMP>** .  
  
 Nesse `sql:max-depth` esquema, a anotação especificada na ** \<constante>** elemento é ignorada porque não há recursão entre a ** \<EMP>** pai e a ** \<constante>** elemento filho. Mas há uma recursão entre o ** \<EMP>** ancestral e o ** \<EMP>** filho. O esquema especifica a anotação `sql:max-depth` em ambos. Portanto, a `sql:max-depth` anotação especificada no ancestral (**\<EMP>** na função de supervisor) tem precedência.  
  
#### <a name="example-c"></a>Exemplo C  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"   
                  parent="Emp"   
                  child="Emp"   
                  parent-key="EmployeeID"   
                  child-key="ReportsTo"/>  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp"   
               sql:relation="Emp"   
               type="EmpType"  
               sql:limit-field="ReportsTo"  
               sql:max-depth="1" />  
    <xsd:complexType name="EmpType" >  
      <xsd:sequence>  
       <xsd:element name="Constant"   
                    sql:is-constant="1"   
                    sql:max-depth="20" >  
         <xsd:complexType >  
           <xsd:sequence>  
            <xsd:element name="Emp"   
                         sql:relation="Emp" type="EmpType"  
                         sql:relationship="SupervisorSupervisee"   
                         sql:max-depth="3" />  
         </xsd:sequence>  
         </xsd:complexType>  
         </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="EmployeeID" type="xsd:int" />  
    </xsd:complexType>  
</xsd:schema>  
```  
  
 Para testar esse esquema, siga as etapas fornecidas para o Exemplo A, anteriormente neste tópico.  
  
## <a name="complex-types-derived-by-restriction"></a>Tipos complexos derivados por restrição  
 Se você tiver uma derivação de tipo complexo por ** \<restrição>**, os elementos do tipo complexo base correspondente não `sql:max-depth` poderão especificar a anotação. Nesses casos, a anotação `sql:max-depth` poderá ser adicionada ao elemento do tipo derivado.  
  
 Por outro lado, se você tiver uma derivação de tipo complexo por ** \<extensão>**, os elementos do tipo complexo base correspondente poderão especificar a `sql:max-depth` anotação.  
  
 Por exemplo, o esquema XSD a seguir gera um erro porque a anotação `sql:max-depth` é especificada no tipo de base. Não há suporte para essa anotação em um tipo que é derivado por ** \<>de restrição** de outro tipo. Para corrigir esse problema, você deve alterar o esquema e especificar a anotação `sql:max-depth` em elemento no tipo derivado.  
  
#### <a name="example-d"></a>Exemplo D  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:msdata="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:complexType name="CustomerBaseType">   
    <xsd:sequence>  
       <xsd:element name="CID" msdata:field="CustomerID" />  
       <xsd:element name="CompanyName"/>  
       <xsd:element name="Customers" msdata:max-depth="3">  
         <xsd:annotation>  
           <xsd:appinfo>  
             <msdata:relationship  
                     parent="Customers"  
                     parent-key="CustomerID"  
                     child-key="CustomerID"  
                     child="Customers" />  
           </xsd:appinfo>  
         </xsd:annotation>  
       </xsd:element>  
    </xsd:sequence>  
  </xsd:complexType>  
  <xsd:element name="Customers" type="CustomerType"/>  
  <xsd:complexType name="CustomerType">  
    <xsd:complexContent>  
       <xsd:restriction base="CustomerBaseType">  
          <xsd:sequence>  
            <xsd:element name="CID"   
                         type="xsd:string"/>  
            <xsd:element name="CompanyName"   
                         type="xsd:string"  
                         msdata:field="CName" />  
            <xsd:element name="Customers"   
                         type="CustomerType" />  
          </xsd:sequence>  
       </xsd:restriction>  
    </xsd:complexContent>  
  </xsd:complexType>  
</xsd:schema>   
```  
  
 No esquema, `sql:max-depth` é especificada em um tipo complexo `CustomerBaseType`. O esquema também especifica um ** \<** elemento de>de cliente `CustomerType`do tipo, que é `CustomerBaseType`derivado de. Uma consulta XPath especificada nesse esquema gerará um erro porque não existe suporte para `sql:max-depth` em um elemento definido em um tipo de base de restrição.  
  
## <a name="schemas-with-a-deep-hierarchy"></a>Esquemas com uma hierarquia profunda  
 Você pode ter um esquema que inclua uma hierarquia profunda na qual um elemento contém um elemento filho que, por sua vez, contém outro elemento filho e assim por diante. Se a anotação `sql:max-depth` especificada nesse esquema gerar um documento XML que inclua uma hierarquia com mais de 500 níveis (com o elemento de nível superior no nível 1, seu filho no nível 2 e, assim, sucessivamente), será retornado um erro.  
  
  
