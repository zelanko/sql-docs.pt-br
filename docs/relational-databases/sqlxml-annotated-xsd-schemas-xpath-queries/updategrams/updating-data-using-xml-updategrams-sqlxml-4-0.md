---
title: Atualização de dados usando diagramas de atualização XML (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
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
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e9db70d57cca76574f5f3e5e1aa77decade35392
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38035733"
---
# <a name="updating-data-using-xml-updategrams-sqlxml-40"></a>Atualizando dados que usam diagramas de atualização XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Quando você atualiza os dados existentes, você deve especificar ambos os  **\<antes de >** e  **\<depois >** blocos. Os elementos especificados na  **\<antes de >** e  **\<depois >** blocos descrevem a alteração desejada. O diagrama usa o elemento (s) que é especificados na  **\<antes de >** bloco para identificar os registros existentes no banco de dados. O elemento (s) correspondente na  **\<depois >** bloco indicam como os registros devem aparecer depois de executar a operação de atualização. Com essas informações, o diagrama de atualização cria uma instrução SQL que corresponde a  **\<depois >** bloco. O diagrama de atualização usa esta instrução para atualizar o banco de dados.  
  
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
 Os elementos na  **\<antes de >** bloco identificam os registros existentes nas tabelas de banco de dados.  
  
 **\<updg:after>**  
 Os elementos na  **\<depois >** bloco descrevem como os registros especificados no  **\<antes >** bloco deve se parecer após as atualizações são aplicadas.  
  
 O **esquema de mapeamento** atributo identifica o esquema de mapeamento a ser usado pelo diagrama de atualização. Se o diagrama Especifica um esquema de mapeamento, os nomes de elementos e atributos especificados nos  **\<antes de >** e  **\<depois >** blocos devem corresponder aos nomes no esquema. O esquema de mapeamento mapeia esses nomes de elemento ou atributo para os nomes de tabela de banco de dados e de coluna.  
  
 Se um diagrama de atualização não especificar um esquema, o diagrama usará mapeamento padrão. No mapeamento padrão, o  **\<ElementName >** especificado no diagrama de atualização mapeará para a tabela de banco de dados e o mapa de elementos ou atributos filho para as colunas de banco de dados.  
  
 Um elemento de  **\<antes de >** bloco deve corresponder com apenas uma linha de tabela no banco de dados. Se o elemento corresponde a várias linhas da tabela ou não corresponde a nenhuma linha de tabela, o diagrama de atualização retornará um erro e cancelará todo o  **\<sincronização >** bloco.  
  
 Um diagrama de atualização pode incluir vários  **\<sincronização >** blocos. Cada  **\<sincronização >** bloco é tratado como uma transação. Cada  **\<sincronização >** bloco pode ter vários  **\<antes >** e  **\<depois >** blocos. Por exemplo, se você estiver atualizando dois dos registros existentes, você pode especificar dois  **\<antes de >** e  **\<depois >** pares, um para cada registro que está sendo atualizado.  
  
## <a name="using-the-updgid-attribute"></a>Usando o atributo updg:id  
 Quando forem especificados vários elementos na  **\<antes de >** e  **\<depois >** blocos, use o **updg: ID** atributo para marcar linhas no  **\<antes de >** e  **\<depois >** blocos. A lógica de processamento usa essas informações para determinar qual registro na  **\<antes de >** bloquear combina com qual registro no  **\<depois >** bloco.  
  
 O **updg: ID** atributo não é necessário (embora recomendado) se qualquer um dos seguintes existir:  
  
-   Os elementos no esquema de mapeamento especificado tiverem o **SQL: Key-campos** atributo definido neles.  
  
-   Há um ou mais valor específico fornecido para o campo chave no diagrama de atualização.  
  
 Se for o caso, tanto o diagrama usa as colunas de chave são especificadas na **SQL: Key-campos** para emparelhar os elementos a  **\<antes >** e  **\< Depois de >** blocos.  
  
 Se o esquema de mapeamento não identificar colunas de chave (usando **SQL: Key-campos**) ou se o diagrama de atualização estiver atualizando um valor de coluna de chave, você deve especificar **updg: ID**.  
  
 Os registros que são identificados na  **\<antes de >** e  **\<depois >** blocos é preciso estar na mesma ordem. O **updg: ID** atributo força a associação entre os elementos que são especificados na  **\<antes >** e  **\<depois >** blocos.  
  
 Se você especificar um elemento na  **\<antes de >** bloco e apenas um elemento correspondente no  **\<depois >** bloquear, usando **updg: ID** não é necessário. No entanto, é recomendável que você especifique **updg: ID** assim mesmo para evitar ambiguidade.  
  
## <a name="examples"></a>Exemplos  
 Antes de você usar os exemplos do diagrama de atualização, observe o seguinte:  
  
-   A maioria dos exemplos usa mapeamento padrão (ou seja, nenhum esquema de mapeamento é especificado no diagrama de atualização). Para obter mais exemplos de diagramas de atualização que usam esquemas de mapeamento, consulte [especificando um esquema de mapeamento anotado em um diagrama de atualização &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
-   A maioria dos exemplos usa o banco de dados de exemplo do AdventureWorks. Todas as atualizações são aplicadas às tabelas deste banco de dados. É possível restaurar o banco de dados AdventureWorks.  
  
### <a name="a-updating-a-record"></a>A. Atualizando um registro  
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
  
 O registro descrito na  **\<antes de >** bloco representa o registro atual no banco de dados. O diagrama usa todos os valores de coluna especificados na  **\<antes de >** bloco para procurar o registro. Este diagrama de atualização, o  **\<antes de >** block fornece apenas a coluna ContactID; portanto, o diagrama de atualização usa apenas o valor para procurar o registro. Se você fosse acrescentar o valor LastName a esse bloco, o diagrama de atualização usaria os valores ContactID e LastName para pesquisar.  
  
 Este diagrama de atualização, o  **\<depois >** block fornece apenas o valor da coluna LastName porque esse é o único valor que está sendo alterado.  
  
##### <a name="to-test-the-updategram"></a>Para testar o diagrama de atualização  
  
1.  Copie o modelo de diagrama de atualização acima e cole-o em um arquivo de texto. Salve o arquivo como UpdateLastName.xml.  
  
2.  Crie e use o Script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o diagrama de atualização.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="b-updating-multiple-records-by-using-the-updgid-attribute"></a>B. Atualizando vários registros usando o atributo updg:id  
 Neste exemplo, o diagrama de atualização executa duas atualizações na tabela HumanResources.Shift no banco de dados do AdventureWorks:  
  
-   Ele altera o nome do turno do dia original que inicia às 7h00 do "Dia" até a "Madrugada".  
  
-   Insere um novo turno denominado "Fim da Manhã" que inicia às 10h00.  
  
 No diagrama de atualização, o **updg: ID** atributo cria associações entre os elementos na  **\<antes >** e  **\<depois >** blocos.  
  
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
  
 Observe como o **updg: ID** atributo combina a primeira instância da \<HumanResources. SHIFT > elemento no  **\<antes de >** bloco com a segunda instância das \< HumanResources. SHIFT > elemento na  **\<depois >** bloco.  
  
##### <a name="to-test-the-updategram"></a>Para testar o diagrama de atualização  
  
1.  Copie o modelo de diagrama de atualização acima e cole-o em um arquivo de texto. Salve o arquivo como UpdateMultipleRecords.xml.  
  
2.  Crie e use o Script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o diagrama de atualização.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="c-specifying-multiple-before-and-after-blocks"></a>C. Especificando vários \<antes de > e \<depois > blocos  
 Para evitar ambiguidade, você pode escrever o diagrama de atualização do exemplo B por meio de várias  **\<antes de >** e  **\<depois >** pares de blocos. Especificando  **\<antes de >** e  **\<depois >** pares é uma maneira de especificar várias atualizações com um mínimo de confusão. Além disso, se cada do  **\<antes de >** e  **\<depois >** blocos especificam no máximo um elemento, você não precisa usar o **updg: ID** atributo .  
  
> [!NOTE]  
>  Para formar um par, o  **\<depois >** marca deve vir logo após correspondente  **\<antes >** marca.  
  
 No diagrama a seguir, a primeira  **\<antes de >** e  **\<depois >** par atualiza o nome do turno para o turno do dia. O segundo par insere um novo registro de turno.  
  
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
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="d-specifying-multiple-sync-blocks"></a>D. Especificando vários \<sincronização > blocos  
 Você pode especificar vários  **\<sincronização >** blocos em um diagrama de atualização. Cada  **\<sincronização >** bloco especificado é uma transação independente.  
  
 No diagrama a seguir, a primeira  **\<sincronização >** bloco atualiza um registro na tabela Sales. Customer. Por causa da simplicidade, o diagrama de atualização especifica só os valores de coluna exigidos; o valor de identidade (CustomerID) e o valor que está sendo atualizado (SalesPersonID).  
  
 A segunda  **\<sincronização >** bloco adiciona dois registros à tabela Sales. SalesOrderHeader. Para esta tabela, SalesOrderID é uma coluna do IDENTITY. Portanto, o diagrama de atualização não especifica o valor de SalesOrderID em cada uma da \<Sales. SalesOrderHeader > elementos.  
  
 Especificando vários  **\<sincronização >** blocos é útil porque se a segunda  **\<sincronização >** bloco (uma transação) não adicionar registros à tabela Sales. SalesOrderHeader, o primeira  **\<sincronização >** bloco ainda poderá atualizar o registro do cliente na tabela Sales. Customer.  
  
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
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="e-using-a-mapping-schema"></a>E. Usando um esquema de mapeamento  
 Neste exemplo, o diagrama Especifica um esquema de mapeamento usando o **esquema de mapeamento** atributo. (Não há um mapeamento padrão; isto é, o esquema de mapeamento fornece o mapeamento necessário de elementos e atributos no diagrama de atualização para as tabelas e colunas do banco de dados.)  
  
 Os elementos e atributos especificados no diagrama de atualização referem-se aos elementos e atributos no esquema de mapeamento.  
  
 Tem o seguinte esquema de mapeamento XSD  **\<cliente >**,  **\<Order >**, e  **\<OD >** elementos que mapeiam para o Tabelas Sales. Customer, Sales. SalesOrderHeader e SalesOrderDetail no banco de dados.  
  
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
  
 Este esquema de mapeamento (UpdategramMappingSchema.xml) é especificado no diagrama de atualização a seguir. O diagrama de atualização adiciona um item de detalhe de ordem na tabela Sales.SalesOrderDetail para uma ordem específica. O diagrama de atualização inclui elementos aninhados: uma  **\<OD >** elemento aninhado dentro de uma  **\<Order >** elemento. A relação de chave primária/chave estrangeira entre estes dois elementos é especificada no esquema de mapeamento.  
  
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
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Para obter mais exemplos de diagramas de atualização que usam esquemas de mapeamento, consulte [especificando um esquema de mapeamento anotado em um diagrama de atualização &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
### <a name="f-using-a-mapping-schema-with-idrefs-attributes"></a>F. Usando um esquema de mapeamento com atributos IDREFS  
 Este exemplo ilustra como os diagramas de atualização usam os atributos IDREFS no esquema de mapeamento para atualizar registros em várias tabelas. Para obter este exemplo, assuma que o banco de dados consiste nas seguintes tabelas:  
  
-   Student(StudentID, LastName)  
  
-   Course(CourseID, CourseName)  
  
-   Enrollment(StudentID, CourseID)  
  
 Como um aluno pode se matricular em vários cursos e um curso pode ter muitos alunos, a terceira tabela, Enrollment, é necessária para representar esta relação M:N.  
  
 O esquema de mapeamento XSD a seguir fornece uma exibição XML das tabelas usando o  **\<Student >**,  **\<curso >**, e  **\<registro >** elementos. O **IDREFS** atributos no esquema de mapeamento especificam a relação entre esses elementos. O **StudentIDList** atributo as  **\<curso >** elemento é um **IDREFS** atributo de tipo que se refere à coluna StudentID na tabela Enrollment. Da mesma forma, o **EnrolledIn** atributo as  **\<aluno >** elemento é um **IDREFS** atributo de tipo que se refere à coluna CourseID na inscrição tabela.  
  
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
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
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
  
 Para obter mais exemplos de diagramas de atualização que usam esquemas de mapeamento, consulte [especificando um esquema de mapeamento anotado em um diagrama de atualização &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Consulte também  
 [Considerações de segurança do diagrama de atualização &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
