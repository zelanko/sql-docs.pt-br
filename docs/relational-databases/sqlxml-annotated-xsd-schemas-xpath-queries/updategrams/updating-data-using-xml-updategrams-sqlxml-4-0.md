---
title: Atualizando dados usando Updategrams XML (SQLXML)
description: Saiba como atualizar os dados existentes usando um updategram XML no SQLXML 4,0.
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- IDREF type attribute [SQLXML]
- before attribute
- <sync> block
- <after> block
- id attribute
- <before> block
- updg:after attribute
- mapping-schema attribute
- IDREFS type attribute [SQLXML]
- updg:id attribute
- multiple record updates
- after attribute
- updategrams [SQLXML], updating data
- updg:before attribute
- record updates [SQLXML]
ms.assetid: 90ef8a33-5ae3-4984-8259-608d2f1d727f
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 01fd8e99d6eb770c2f5680ead1e2c4d9b9ec98b8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85733659"
---
# <a name="updating-data-using-xml-updategrams-sqlxml-40"></a>Atualizando dados que usam diagramas de atualização XML (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Ao atualizar os dados existentes, você deve especificar os **\<before>** blocos e **\<after>** . Os elementos especificados nos **\<before>** blocos e **\<after>** descrevem a alteração desejada. O updategram usa os elementos que são especificados no **\<before>** bloco para identificar os registros existentes no banco de dados. Os elementos correspondentes no **\<after>** bloco indicam como os registros devem ser examinados após a execução da operação de atualização. A partir dessas informações, o updategram cria uma instrução SQL que corresponde ao **\<after>** bloco. O diagrama de atualização usa esta instrução para atualizar o banco de dados.  
  
 Este é o formato do diagrama de atualização para uma operação de atualização:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync [mapping-schema="SampleSchema.xml"]  >  
   <updg:before>  
      <ElementName [updg:id="value"] .../>  
      [<ElementName [updg:id="value"] .../> ... ]  
   </updg:before>  
   <updg:after>  
      <ElementName [updg:id="value"] ... />  
      [<ElementName [updg:id="value"] .../> ...]  
   </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 **\<updg:before>**  
 Os elementos no **\<before>** bloco identificam os registros existentes nas tabelas do banco de dados.  
  
 **\<updg:after>**  
 Os elementos no **\<after>** bloco descrevem como os registros especificados no **\<before>** bloco devem ser examinados depois que as atualizações são aplicadas.  
  
 O atributo **Mapping-Schema** identifica o esquema de mapeamento a ser usado pelo updategram. Se o updategram especificar um esquema de mapeamento, os nomes de elemento e atributo especificados **\<before>** nos **\<after>** blocos e deverão corresponder aos nomes no esquema. O esquema de mapeamento mapeia esses nomes de elemento ou atributo para os nomes de tabela de banco de dados e de coluna.  
  
 Se um diagrama de atualização não especificar um esquema, o diagrama usará mapeamento padrão. No mapeamento padrão, o **\<ElementName>** especificado no updategram mapeia para a tabela de banco de dados e os elementos filho ou atributos são mapeados para as colunas do banco de dados.  
  
 Um elemento no **\<before>** bloco deve corresponder a apenas uma linha de tabela no banco de dados. Se o elemento corresponder a várias linhas da tabela ou não corresponder a nenhuma linha da tabela, o updategram retornará um erro e cancelará o **\<sync>** bloco inteiro.  
  
 Um updategram pode incluir vários **\<sync>** blocos. Cada **\<sync>** bloco é tratado como uma transação. Cada **\<sync>** bloco pode ter vários **\<before>** **\<after>** blocos e. Por exemplo, se você estiver atualizando dois dos registros existentes, poderá especificar dois **\<before>** **\<after>** pares, um para cada registro que está sendo atualizado.  
  
## <a name="using-the-updgid-attribute"></a>Usando o atributo updg:id  
 Quando vários elementos são especificados nos **\<before>** blocos e **\<after>** , use o atributo **updg: ID** para marcar linhas nos **\<before>** **\<after>** blocos e. A lógica de processamento usa essas informações para determinar qual registro nos **\<before>** pares de blocos com qual registro no **\<after>** bloco.  
  
 O atributo **updg: ID** não é necessário (embora recomendado) se uma das seguintes opções existir:  
  
-   Os elementos no esquema de mapeamento especificado têm o atributo **SQL: key-fields** definido neles.  
  
-   Há um ou mais valor específico fornecido para o campo chave no diagrama de atualização.  
  
 Se for o caso, o updategram usará as colunas de chave especificadas nos **campos SQL: Key** para emparelhar os elementos nos **\<before>** **\<after>** blocos e.  
  
 Se o esquema de mapeamento não identificar as colunas de chave (usando **SQL: key-fields**) ou se o updategram estiver atualizando um valor de coluna de chave, você deverá especificar **updg: ID**.  
  
 Os registros que são identificados nos **\<before>** blocos e **\<after>** não precisam estar na mesma ordem. O atributo **updg: ID** força a associação entre os elementos que são especificados nos **\<before>** blocos e **\<after>** .  
  
 Se você especificar um elemento no **\<before>** bloco e apenas um elemento correspondente no **\<after>** bloco, o uso de **updg: ID** não será necessário. No entanto, é recomendável que você especifique **updg: ID** de qualquer forma para evitar ambigüidade.  
  
## <a name="examples"></a>Exemplos  
 Antes de você usar os exemplos do diagrama de atualização, observe o seguinte:  
  
-   A maioria dos exemplos usa mapeamento padrão (ou seja, nenhum esquema de mapeamento é especificado no diagrama de atualização). Para obter mais exemplos de Updategrams que usam esquemas de mapeamento, consulte [especificando um esquema de mapeamento anotado em um Updategram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
-   A maioria dos exemplos usa o banco de dados de exemplo do AdventureWorks. Todas as atualizações são aplicadas às tabelas deste banco de dados. É possível restaurar o banco de dados AdventureWorks.  
  
### <a name="a-updating-a-record"></a>a. Atualizando um registro  
 O diagrama de atualização a seguir atualiza o sobrenome do funcionário para Silva na tabela Person.Contact no banco de dados do AdventureWorks. O diagrama de atualização não especifica nenhum esquema de mapeamento; portanto, o diagrama de atualização usa o mapeamento padrão.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" />  
</updg:before>  
<updg:after>  
   <Person.Contact LastName="Abel-Achong" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 O registro descrito no **\<before>** bloco representa o registro atual no banco de dados. O updategram usa todos os valores de coluna especificados no **\<before>** bloco para pesquisar o registro. Nesse updategram, o **\<before>** bloco fornece apenas a coluna ContactID; portanto, o updategram usa apenas o valor para pesquisar o registro. Se você fosse acrescentar o valor LastName a esse bloco, o diagrama de atualização usaria os valores ContactID e LastName para pesquisar.  
  
 Nesse updategram, o **\<after>** bloco fornece apenas o valor de coluna LastName porque esse é o único valor que está sendo alterado.  
  
##### <a name="to-test-the-updategram"></a>Para testar o diagrama de atualização  
  
1.  Copie o modelo de diagrama de atualização acima e cole-o em um arquivo de texto. Salve o arquivo como UpdateLastName.xml.  
  
2.  Crie e use o Script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o diagrama de atualização.  

     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="b-updating-multiple-records-by-using-the-updgid-attribute"></a>B. Atualizando vários registros usando o atributo updg:id  
 Neste exemplo, o diagrama de atualização executa duas atualizações na tabela HumanResources.Shift no banco de dados do AdventureWorks:  
  
-   Ele altera o nome do turno do dia original que inicia às 7h00 do "Dia" até a "Madrugada".  
  
-   Insere um novo turno denominado "Fim da Manhã" que inicia às 10h00.  
  
 No updategram, o atributo **updg: ID** cria associações entre elementos nos **\<before>** **\<after>** blocos e.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift updg:id="x" Name="Day" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift updg:id="y" Name="Late Morning"   
                            StartTime="1900-01-01 10:00:00.000"  
                            EndTime="1900-01-01 18:00:00.000"  
                            ModifiedDate="2004-06-01 00:00:00.000"/>  
      <HumanResources.Shift updg:id="x" Name="Early Morning" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Observe como o atributo **updg: ID** emparelha a primeira instância do \<HumanResources.Shift> elemento no **\<before>** bloco com a segunda instância do \<HumanResources.Shift> elemento no **\<after>** bloco.  
  
##### <a name="to-test-the-updategram"></a>Para testar o diagrama de atualização  
  
1.  Copie o modelo de diagrama de atualização acima e cole-o em um arquivo de texto. Salve o arquivo como UpdateMultipleRecords.xml.  
  
2.  Crie e use o Script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o diagrama de atualização.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="c-specifying-multiple-before-and-after-blocks"></a>C. Especificando vários \<before> \<after> blocos e  
 Para evitar ambigüidade, você pode escrever o updategram no exemplo B usando vários **\<before>** **\<after>** pares de blocos e. Especificar **\<before>** **\<after>** pares e é uma maneira de especificar várias atualizações com um mínimo de confusão. Além disso, se cada um **\<before>** dos **\<after>** blocos e especificar no máximo um elemento, você não precisará usar o atributo **updg: ID** .  
  
> [!NOTE]  
>  Para formar um par, a **\<after>** marca deve seguir imediatamente sua **\<before>** marca correspondente.  
  
 No updategram a seguir, o primeiro **\<before>** e o **\<after>** par atualiza o nome da mudança para o turno do dia. O segundo par insere um novo registro de turno.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="1" Name="Day" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="Early Morning" />  
    </updg:after>  
    <updg:before>  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="Late Morning"   
                            StartTime="1900-01-01 10:00:00.000"  
                            EndTime="1900-01-01 18:00:00.000"  
                            ModifiedDate="2004-06-01 00:00:00.000"/>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Para testar o diagrama de atualização  
  
1.  Copie o modelo de diagrama de atualização acima e cole-o em um arquivo de texto. Salve o arquivo como UpdateMultipleBeforeAfter.xml.  
  
2.  Crie e use o Script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o diagrama de atualização.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="d-specifying-multiple-sync-blocks"></a>D. Especificando vários \<sync> blocos  
 Você pode especificar vários **\<sync>** blocos em um updategram. Cada **\<sync>** bloco especificado é uma transação independente.  
  
 No updategram a seguir, o primeiro **\<sync>** bloco atualiza um registro na tabela Sales. Customer. Por causa da simplicidade, o diagrama de atualização especifica só os valores de coluna exigidos; o valor de identidade (CustomerID) e o valor que está sendo atualizado (SalesPersonID).  
  
 O segundo **\<sync>** bloco adiciona dois registros à tabela Sales. SalesOrderHeader. Para esta tabela, SalesOrderID é uma coluna do IDENTITY. Portanto, o updategram não especifica o valor de SalesOrderID em cada um dos \<Sales.SalesOrderHeader> elementos.  
  
 A especificação de vários **\<sync>** blocos é útil porque, se o segundo **\<sync>** bloco (uma transação) falhar ao adicionar registros à tabela Sales. SalesOrderHeader, o primeiro **\<sync>** bloco ainda poderá atualizar o registro do cliente na tabela Sales. Customer.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
      <Sales.Customer CustomerID="1" SalesPersonID="280" />  
    </updg:before>  
    <updg:after>  
      <Sales.Customer CustomerID="1" SalesPersonID="283" />  
    </updg:after>  
  </updg:sync>  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
   <Sales.SalesOrderHeader   
             CustomerID="1"  
             RevisionNumber="1"  
             OrderDate="2004-07-01 00:00:00.000"  
             DueDate="2004-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="01010101-2222-3333-4444-556677889900"  
             ModifiedDate="2004-07-08 00:00:00.000" />  
   <Sales.SalesOrderHeader  
             CustomerID="1"  
             RevisionNumber="1"  
             OrderDate="2004-07-01 00:00:00.000"  
             DueDate="2004-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="1000.0000"  
             TaxAmt="0.0000"  
             Freight="0.0000"  
             rowguid="10101010-2222-3333-4444-556677889900"  
             ModifiedDate="2004-07-09 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Para testar o diagrama de atualização  
  
1.  Copie o modelo de diagrama de atualização acima e cole-o em um arquivo de texto. Salve o arquivo como UpdateMultipleSyncs.xml.  
  
2.  Crie e use o Script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o diagrama de atualização.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="e-using-a-mapping-schema"></a>E. Usando um esquema de mapeamento  
 Neste exemplo, o updategram especifica um esquema de mapeamento usando o atributo **Mapping-Schema** . (Não há um mapeamento padrão; isto é, o esquema de mapeamento fornece o mapeamento necessário de elementos e atributos no diagrama de atualização para as tabelas e colunas do banco de dados.)  
  
 Os elementos e atributos especificados no diagrama de atualização referem-se aos elementos e atributos no esquema de mapeamento.  
  
 O esquema de mapeamento XSD a seguir tem os **\<Customer>** **\<Order>** elementos, e **\<OD>** que são mapeados para as tabelas Sales. Customer, Sales. SalesOrderHeader e Sales. SalesOrderDetail no banco de dados.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustomerOrder"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
  
    <sql:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                     sql:relationship="CustomerOrder" >  
           <xsd:complexType>  
              <xsd:sequence>  
                <xsd:element name="OD"   
                             sql:relation="Sales.SalesOrderDetail"  
                             sql:relationship="OrderOD" >  
                 <xsd:complexType>  
                  <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                  <xsd:attribute name="ProductID" type="xsd:integer" />  
                  <xsd:attribute name="UnitPrice" type="xsd:decimal" />  
                  <xsd:attribute name="OrderQty" type="xsd:integer" />  
                  <xsd:attribute name="UnitPriceDiscount" type="xsd:decimal" />   
                 </xsd:complexType>  
                </xsd:element>  
              </xsd:sequence>  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="OrderDate" type="xsd:date" />  
           </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Este esquema de mapeamento (UpdategramMappingSchema.xml) é especificado no diagrama de atualização a seguir. O diagrama de atualização adiciona um item de detalhe de ordem na tabela Sales.SalesOrderDetail para uma ordem específica. O updategram inclui elementos aninhados: um **\<OD>** elemento aninhado dentro de um **\<Order>** elemento. A relação de chave primária/chave estrangeira entre estes dois elementos é especificada no esquema de mapeamento.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="UpdategramMappingSchema.xml" >  
    <updg:before>  
       <Order SalesOrderID="43659" />  
    </updg:before>  
    <updg:after>  
      <Order SalesOrderID="43659" >  
          <OD ProductID="776" UnitPrice="2329.0000"  
              OrderQty="2" UnitPriceDiscount="0.0" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Para testar o diagrama de atualização  
  
1.  Copie o esquema de mapeamento acima e cole-o em um arquivo de texto. Salve o arquivo como UpdategramMappingSchema.xml.  
  
2.  Copie o modelo de diagrama de atualização acima e cole-o em um arquivo de texto. Salve o arquivo como UpdateWithMappingSchema.xml na mesma pasta que foi usada para salvar o esquema de mapeamento (UpdategramMappingSchema.xml).  
  
3.  Crie e use o Script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o diagrama de atualização.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Para obter mais exemplos de Updategrams que usam esquemas de mapeamento, consulte [especificando um esquema de mapeamento anotado em um Updategram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
### <a name="f-using-a-mapping-schema-with-idrefs-attributes"></a>F. Usando um esquema de mapeamento com atributos IDREFS  
 Este exemplo ilustra como os diagramas de atualização usam os atributos IDREFS no esquema de mapeamento para atualizar registros em várias tabelas. Para obter este exemplo, assuma que o banco de dados consiste nas seguintes tabelas:  
  
-   Student(StudentID, LastName)  
  
-   Course(CourseID, CourseName)  
  
-   Enrollment(StudentID, CourseID)  
  
 Como um aluno pode se matricular em vários cursos e um curso pode ter muitos alunos, a terceira tabela, Enrollment, é necessária para representar esta relação M:N.  
  
 O esquema de mapeamento XSD a seguir fornece uma exibição XML das tabelas usando os **\<Student>** **\<Course>** elementos, e **\<Enrollment>** . Os atributos **IDREFS** no esquema de mapeamento especificam a relação entre esses elementos. O atributo **StudentIDList** no **\<Course>** elemento é um atributo de tipo **IDREFS** que se refere à coluna StudentId na tabela de registro. Da mesma forma, o atributo **Enrollment** no **\<Student>** elemento é um atributo de tipo **IDREFS** que se refere à coluna cursoid na tabela de registro.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="StudentEnrollment"  
          parent="Student"  
          parent-key="StudentID"  
          child="Enrollment"  
          child-key="StudentID" />  
  
    <sql:relationship name="CourseEnrollment"  
          parent="Course"  
          parent-key="CourseID"  
          child="Enrollment"  
          child-key="CourseID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Course" sql:relation="Course"   
                             sql:key-fields="CourseID" >  
    <xsd:complexType>  
    <xsd:attribute name="CourseID"  type="xsd:string" />   
    <xsd:attribute name="CourseName"   type="xsd:string" />   
    <xsd:attribute name="StudentIDList" sql:relation="Enrollment"  
                 sql:field="StudentID"  
                 sql:relationship="CourseEnrollment"   
                                     type="xsd:IDREFS" />  
  
    </xsd:complexType>  
  </xsd:element>  
  <xsd:element name="Student" sql:relation="Student" >  
    <xsd:complexType>  
    <xsd:attribute name="StudentID"  type="xsd:string" />   
    <xsd:attribute name="LastName"   type="xsd:string" />   
    <xsd:attribute name="EnrolledIn" sql:relation="Enrollment"  
                 sql:field="CourseID"  
                 sql:relationship="StudentEnrollment"   
                                     type="xsd:IDREFS" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Sempre que você especifica este esquema em um diagrama de atualização e insere um registro na tabela Course, o diagrama de atualização insere um novo registro de curso na tabela Course. Se você especificar um ou mais novos IDs de aluno para o atributo StudentIDList, o diagrama de atualização também inserirá um registro na tabela Enrollment para cada novo aluno. O diagrama de atualização garante que nenhuma duplicata seja adicionada à tabela Enrollment.  
  
##### <a name="to-test-the-updategram"></a>Para testar o diagrama de atualização  
  
1.  Crie estas tabelas no banco de dados que é especificado na raiz virtual:  
  
    ```  
    CREATE TABLE Student(StudentID varchar(10) primary key,   
                         LastName varchar(25))  
    CREATE TABLE Course(CourseID varchar(10) primary key,   
                        CourseName varchar(25))  
    CREATE TABLE Enrollment(StudentID varchar(10)   
                                      references Student(StudentID),  
                           CourseID varchar(10)   
                                      references Course(CourseID))  
    ```  
  
2.  Adicione estes dados de exemplo:  
  
    ```  
    INSERT INTO Student VALUES ('S1','Davoli')  
    INSERT INTO Student VALUES ('S2','Fuller')  
  
    INSERT INTO Course VALUES  ('CS101', 'C Programming')  
    INSERT INTO Course VALUES  ('CS102', 'Understanding XML')  
  
    INSERT INTO Enrollment VALUES ('S1', 'CS101')  
    INSERT INTO Enrollment VALUES ('S1', 'CS102')  
    ```  
  
3.  Copie o esquema de mapeamento acima e cole-o em um arquivo de texto. Salve o arquivo como SampleSchema.xml.  
  
4.  Salve o diagrama de atualização (SampleUpdategram) na mesma pasta usada para salvar o esquema de mapeamento na etapa anterior. (Esse diagrama de atualização descarta um aluno com StudentID = "1" do curso CS102.)  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101 CS102" />  
        </updg:before>  
        <updg:after >  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
5.  Crie e use o Script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o diagrama de atualização.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
6.  Salve e execute o diagrama de atualização a seguir como descrito nas etapas anteriores. O diagrama de atualização adiciona o aluno com StudentID = "1" novamente ao curso CS102 adicionando um registro na tabela Enrollment.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101" />  
        </updg:before>  
        <updg:after >  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101 CS102" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
7.  Salve e execute este próximo diagrama de atualização como descrito nas etapas anteriores. Esse diagrama de atualização insere três alunos novos e os matricula no curso CS101. Novamente, a relação de IDREFS insere registros na tabela Enrollment.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
           <Course updg:id="y" CourseID="CS101"   
                               CourseName="C Programming" />  
        </updg:before>  
        <updg:after >  
           <Student updg:id="x1" StudentID="S3" LastName="Leverling" />  
           <Student updg:id="x2" StudentID="S4" LastName="Pecock" />  
           <Student updg:id="x3" StudentID="S5" LastName="Buchanan" />  
           <Course updg:id="y" CourseID="CS101"  
                               CourseName="C Programming"  
                               StudentIDList="S3 S4 S5" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
 Este é o esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <ElementType name="Enrollment" sql:relation="Enrollment" sql:key-fields="StudentID CourseID">  
    <AttributeType name="StudentID" dt:type="id" />  
    <AttributeType name="CourseID" dt:type="id" />  
  
    <attribute type="StudentID" />  
    <attribute type="CourseID" />  
  </ElementType>  
  <ElementType name="Course" sql:relation="Course" sql:key-fields="CourseID">  
    <AttributeType name="CourseID" dt:type="id" />  
    <AttributeType name="CourseName" />  
  
    <attribute type="CourseID" />  
    <attribute type="CourseName" />  
  
    <AttributeType name="StudentIDList" dt:type="idrefs" />  
    <attribute type="StudentIDList" sql:relation="Enrollment" sql:field="StudentID" >  
        <sql:relationship  
                key-relation="Course"  
                key="CourseID"  
                foreign-relation="Enrollment"  
                foreign-key="CourseID" />  
    </attribute>  
  
  </ElementType>  
  <ElementType name="Student" sql:relation="Student">  
    <AttributeType name="StudentID" dt:type="id" />  
     <AttributeType name="LastName" />  
  
    <attribute type="StudentID" />  
    <attribute type="LastName" />  
  
    <AttributeType name="EnrolledIn" dt:type="idrefs" />  
    <attribute type="EnrolledIn" sql:relation="Enrollment" sql:field="CourseID" >  
        <sql:relationship  
                key-relation="Student"  
                key="StudentID"  
                foreign-relation="Enrollment"  
                foreign-key="StudentID" />  
    </attribute>  
  
    <element type="Enrollment" sql:relation="Enrollment" >  
        <sql:relationship key-relation="Student"  
                          key="StudentID"  
                          foreign-relation="Enrollment"  
                          foreign-key="StudentID" />  
    </element>  
  </ElementType>  
  
</Schema>  
```  
  
 Para obter mais exemplos de Updategrams que usam esquemas de mapeamento, consulte [especificando um esquema de mapeamento anotado em um Updategram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Considerações de segurança do updategram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
