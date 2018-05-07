---
title: Registrar processo de geração (SQLXML 4.0) | Microsoft Docs
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
- XML Bulk Load [SQLXML], record generation process
- node scopes [SQLXML]
- record subsets [SQLXML]
- scope [SQLXML]
- key ordering rules [SQLXML]
- record generation process for bulk loads [SQLXML]
- entering node scope [SQLXML]
- bulk load [SQLXML], record generation process
- leaving node scope [SQLXML]
- schema mapping [SQLXML]
ms.assetid: d8885bbe-6f15-4fb9-9684-ca7883cfe9ac
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 59ec68c1c2c321f45940eace9ef1f6a3dc9be9c8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="record-generation-process-sqlxml-40"></a>Registrar processo de geração (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  O Carregamento em massa XML processa os dados de entrada XML e prepara os registros para as tabelas apropriadas no Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A lógica no Carregamento em massa XML determina quando gerar um novo registro, quais valores de elemento filho ou de atributo copiar nos campos do registro e quando o registro está completo e pronto para ser enviado ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para inserção.  
  
 O Carregamento em massa XML não carrega todos os dados XML de entrada na memória e não produz conjuntos de registros completos antes de enviar dados ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Isto é porque os dados de entrada XML podem ser um documento grande e carregar o documento inteiro na memória pode ser caro. Em vez disso, o Carregamento em massa XML faz o seguinte:  
  
1.  Analisa o esquema de mapeamento e prepara o plano de execução necessário.  
  
2.  Aplica o plano de execução aos dados no fluxo de entrada.  
  
 Esse processamento sequencial torna importante o fornecimento de dados de entrada XML de um modo específico. Você deve entender como o Carregamento em massa XML analisa o esquema de mapeamento e como o processo de geração de registro ocorre. Ao compreender isso, você pode fornecer um esquema de mapeamento ao Carregamento em massa XML que gera os resultados desejados.  
  
 O Carregamento em massa XML trata as anotações do esquema de mapeamento comum, incluindo mapeamentos de coluna e tabela (especificados explicitamente, usando anotações, ou implicitamente, através do mapeamento padrão), e relacionamentos de junção.  
  
> [!NOTE]  
>  Parte-se do pressuposto que você está familiarizado com esquemas de mapeamento anotados XSD ou XDR. Para obter mais informações sobre esquemas, consulte [Introdução a esquemas de XSD anotado &#40;SQLXML 4.0&#41; ](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md) ou [os esquemas XDR anotados &#40;substituídos no SQLXML 4.0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
 Compreender a geração de registros requer o conhecimento dos seguintes conceitos:  
  
-   Escopo de um nó  
  
-   Regra de geração de registro  
  
-   Subconjunto de registro e regra de ordenação de chaves  
  
-   Exceções à regra de geração de registros  
  
## <a name="scope-of-a-node"></a>Escopo de um nó  
 Um nó (um elemento ou um atributo) em um documento XML entra *no escopo* quando carregamento em massa XML o encontra no fluxo de dados de entrada XML. Para um nó de elemento, a marca inicial do elemento coloca o elemento no escopo. Para um nó de atributo, o nome do atributo coloca o atributo no escopo.  
  
 Um nó sai do escopo quando não há mais dados para ele: seja na marca final (no caso de um nó de elemento) ou no final do valor de um atributo (no caso de um nó de atributo).  
  
## <a name="record-generation-rule"></a>Regra de geração de registro  
 Quando um nó (elemento ou atributo) entra no escopo, existe uma possibilidade de geração de um registro a partir desse nó. O registro dura enquanto o nó associado estiver no escopo. Quando o nó sair do escopo, o Carregamento em massa XML considera o registro gerado completo (com dados) e o envia ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para inserção.  
  
 Por exemplo, considere o seguinte fragmento de esquema XSD:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Customer" sql:relation="Customers" >  
   <xsd:complexType>  
     <xsd:attribute name="CustomerID" type="xsd:string" />  
     <xsd:attribute name="CompanyName" type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 O esquema especifica um  **\<cliente >** elemento com **CustomerID** e **CompanyName** atributos. O **SQL: Relation** anotação mapeia o  **\<cliente >** elemento para a tabela Customers.  
  
 Considere este fragmento de um documento XML:  
  
```  
<Customer CustomerID="1" CompanyName="xyz" />  
<Customer CustomerID="2" CompanyName="abc" />  
...  
```  
  
 Quando um Carregamento em massa XML é fornecido com o esquema descrito nos parágrafos anteriores e os dados XML são fornecidos como entrada, ele processa os nós (elementos e atributos) nos dados de origem, conforme indicado a seguir:  
  
-   A marca de início do primeiro  **\<cliente >** elemento coloca esse elemento no escopo. Este nó é mapeado para a tabela Customers. Portanto, o Carregamento em massa XML gera um registro para a tabela Customers.  
  
-   No esquema, todos os atributos do  **\<cliente >** são mapeados para colunas da tabela Customers. À medida que esses atributos entram no escopo, o Carregamento em massa XML copia seus valores para o registro do cliente que já foi gerado pelo escopo pai.  
  
-   Quando o XML Bulk Load atingir a marca de fim de  **\<cliente >** elemento, o elemento sai do escopo. Isto faz o Carregamento em massa XML considerar o registro completo e enviá-lo ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Carregamento em massa XML segue esse processo para cada subsequentes  **\<cliente >** elemento.  
  
> [!IMPORTANT]  
>  Nesse modelo, como um registro é inserido quando uma marca final é atingida (ou o nó fica fora do escopo), você deve definir todos os dados que estão associados ao registro dentro do escopo do nó.  
  
## <a name="record-subset-and-the-key-ordering-rule"></a>Subconjunto de registro e a chave de ordenação de regra  
 Quando você especificar um esquema de mapeamento que usa  **\<SQL: Relationship >**, o termo subconjunto refere-se ao conjunto de registros que é gerado no lado externo da relação. No exemplo a seguir, os registros CustOrder estão no lado externo,  **\<SQL: Relationship >**.  
  
 Por exemplo, suponha que um banco de dados contenha as seguintes tabelas:  
  
-   Cust (CustomerID, CompanyName, City)  
  
-   CustOrder (CustomerID, OrderID)  
  
 O CustomerID na tabela CustOrder é uma chave estrangeira que faz referência à chave primária CustomerID na tabela Cust.  
  
 Agora, considere a exibição XML conforme especificado no seguinte esquema XSD anotado. Esse esquema usa  **\<SQL: Relationship >** para especificar a relação entre as tabelas Cust e CustOrder.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customers" sql:relation="Cust" >  
   <xsd:complexType>  
     <xsd:sequence>  
       <xsd:element name="CustomerID"  type="xsd:integer" />  
       <xsd:element name="CompanyName" type="xsd:string" />  
       <xsd:element name="City"        type="xsd:string" />  
       <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
         <xsd:complexType>  
          <xsd:attribute name="OrderID" type="xsd:integer" />  
         </xsd:complexType>  
       </xsd:element>  
     </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Os dados XML de exemplo e as etapas para criar um exemplo de funcionamento são dados a seguir.  
  
-   Quando um  **\<cliente >** nó de elemento no arquivo de dados XML entra no escopo, o XML Bulk Load gera um registro para a tabela Cust. Carregamento em massa XML, em seguida, copia os valores de colunas necessárias (CustomerID, CompanyName e City) do  **\<CustomerID >**,  **\<CompanyName >** e o  **\<Cidade >** elementos filho como esses elementos entrarem no escopo.  
  
-   Quando um  **\<ordem >** nó de elemento entra no escopo, o XML Bulk Load gera um registro para a tabela CustOrder. Carregamento em massa XML copia o valor de **OrderID** atributo para este registro. O valor necessário para a coluna CustomerID é obtida a partir de  **\<CustomerID >** elemento filho do  **\<cliente >** elemento. O XML Bulk Load usa as informações que são especificadas no  **\<SQL: Relationship >** para obter o valor da chave estrangeiro CustomerID para este registro, a menos que o **CustomerID** foi de atributo especificado no  **\<ordem >** elemento. A regra geral é que, se o elemento filho especifica explicitamente um valor para o atributo de chave estrangeiro, o XML Bulk Load usa esse valor e não obtém o valor do elemento pai usando especificado **\<SQL: Relationship >**. Como isso  **\<ordem >** nó de elemento sai do escopo, o carregamento em massa XML envia o registro de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e, em seguida, processa todos os próximos  **\<ordem >** nós de elemento da mesma maneira.  
  
-   Por fim, o  **\<cliente >** nó de elemento sai do escopo. Nesse instante, o Carregamento em massa XML envia o registro do cliente ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O Carregamento em massa XML segue este processo para todos os clientes subsequentes no fluxo de dados XML.  
  
 Existem duas observações sobre o esquema de mapeamento:  
  
-   Quando o esquema obedece a regra de "contenção" (por exemplo, todos os dados que está associados com o cliente e a ordem é definido dentro do escopo de associado  **\<cliente >** e  **\<Ordem >** nós de elemento), o carregamento em massa for bem-sucedida.  
  
-   Descrever o  **\<cliente >** elemento, seu filho, os elementos são especificados na ordem apropriada. Nesse caso, o  **\<CustomerID >** elemento filho é especificada antes do  **\<ordem >** elemento filho. Isso significa que, no arquivo de dados XML entrado, o  **\<CustomerID >** o valor do elemento está disponível como a chave estrangeira quando a  **\<ordem >** elemento entra no escopo. Os atributos de chave são especificados primeiro; esta é a “regra de ordenação de chaves".  
  
     Se você especificar o  **\<CustomerID >** elemento filho após o  **\<ordem >** elemento filho, o valor não está disponível quando o  **\< Ordem >** elemento entra no escopo. Quando o  **\</Order >** marca final é lida, então o registro para a tabela CustOrder é considerado concluído e é inserido na tabela CustOrder com um valor nulo para a coluna CustomerID, que não é o resultado desejado.  
  
#### <a name="to-create-a-working-sample"></a>Para criar um exemplo de funcionamento  
  
1.  Salve o esquema fornecido neste exemplo como SampleSchema.xml.  
  
2.  Crie estas tabelas:  
  
    ```  
    CREATE TABLE Cust (  
                  CustomerID     int         PRIMARY KEY,  
                  CompanyName    varchar(20) NOT NULL,  
                  City           varchar(20) DEFAULT 'Seattle')  
    GO  
    CREATE TABLE CustOrder (  
                 OrderID        int         PRIMARY KEY,  
                 CustomerID     int         FOREIGN KEY REFERENCES                                          Cust(CustomerID))  
    GO  
    ```  
  
3.  Salve os dados de entrada XML de exemplo a seguir como SampleXMLData.xml:  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City>NY</City>   
        <Order OrderID="1" />  
        <Order OrderID="2" />  
      </Customers>  
  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Toms Spezialitten</CompanyName>  
        <City>LA</City>  
        <Order OrderID="3" />  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
    </Customers>  
    </ROOT>  
    ```  
  
4.  Para executar o Carregamento em massa XML, salve e execute o seguinte exemplo do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript) (BulkLoad.vbs):  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
## <a name="exceptions-to-the-record-generation-rule"></a>Exceções à regra de geração de registros  
 O Carregamento em massa XML não gera um registro para um nó quando ele entra no escopo, se esse nó for do tipo IDREF ou IDREFS. Você deve ter certeza de que há uma descrição completa do registro em algum lugar do esquema. O **dt: type = "nmtokens"** anotações são ignoradas, assim como o tipo IDREFS é ignorado.  
  
 Por exemplo, considere o seguinte esquema XSD que descreve  **\<cliente >** e  **\<ordem >** elementos. O  **\<cliente >** elemento inclui um **OrderList** atributo do tipo IDREFS. O  **\<SQL: Relationship >** marca Especifica a relação um-para-muitos entre o cliente e a lista de pedidos.  
  
 Este é o esquema:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
                 parent="Cust"  
                 parent-key="CustomerID"  
                 child="CustOrder"  
                 child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customers" sql:relation="Cust" >  
   <xsd:complexType>  
    <xsd:attribute name="CustomerID" type="xsd:integer" />  
    <xsd:attribute name="CompanyName" type="xsd:string" />  
    <xsd:attribute name="City" type="xsd:string" />  
    <xsd:attribute name="OrderList"   
                       type="xsd:IDREFS"   
                       sql:relation="CustOrder"   
                       sql:field="OrderID"  
                       sql:relationship="CustCustOrder" >  
    </xsd:attribute>  
  </xsd:complexType>  
 </xsd:element>  
  
  <xsd:element name="Order" sql:relation="CustOrder" >  
   <xsd:complexType>  
    <xsd:attribute name="OrderID" type="xsd:string" />  
    <xsd:attribute name="CustomerID" type="xsd:integer" />  
    <xsd:attribute name="OrderDate" type="xsd:date" />  
  </xsd:complexType>  
 </xsd:element>  
</xsd:schema>  
```  
  
 Como o carregamento em massa ignora os nós do tipo IDREFS, não há nenhuma geração de registro quando o **OrderList** nó de atributo entra no escopo. Portanto, se você quiser que os registros de ordem sejam adicionados à tabela Orders, deve descrever esses pedidos ordens em algum lugar no esquema. Nesse esquema, especificando o  **\<ordem >** elemento garante que o XML Bulk Load adiciona os registros de pedido à tabela Orders. O  **\<ordem >** elemento descreve todos os atributos necessários para preencher o registro para a tabela CustOrder.  
  
 Você deve garantir que o **CustomerID** e **OrderID** valores no  **\<cliente >** elemento correspondam aos valores de  **\<Ordem >** elemento. Você é responsável por manter a integridade referencial.  
  
#### <a name="to-test-a-working-sample"></a>Para testar um exemplo de funcionamento  
  
1.  Crie estas tabelas:  
  
    ```  
    CREATE TABLE Cust (  
                  CustomerID     int          PRIMARY KEY,  
                  CompanyName    varchar(20)  NOT NULL,  
                  City           varchar(20)  DEFAULT 'Seattle')  
    GO  
    CREATE TABLE CustOrder (  
                  OrderID        varchar(10) PRIMARY KEY,  
                  CustomerID     int         FOREIGN KEY REFERENCES                                          Cust(CustomerID),  
                  OrderDate      datetime DEFAULT '2000-01-01')  
    GO  
    ```  
  
2.  Salve o esquema de mapeamento fornecido neste exemplo como SampleSchema.xml.  
  
3.  Salve os dados XML de exemplo a seguir como SampleXMLData.xml:  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1111" CompanyName="Sean Chai" City="NY"  
                 OrderList="Ord1 Ord2" />  
      <Customers CustomerID="1112" CompanyName="Dont Know" City="LA"  
                 OrderList="Ord3 Ord4" />  
      <Order OrderID="Ord1" CustomerID="1111" OrderDate="1999-01-01" />  
      <Order OrderID="Ord2" CustomerID="1111" OrderDate="1999-02-01" />  
      <Order OrderID="Ord3" CustomerID="1112" OrderDate="1999-03-01" />  
      <Order OrderID="Ord4" CustomerID="1112" OrderDate="1999-04-01" />  
    </ROOT>  
    ```  
  
4.  Para executar o Carregamento em massa XML, salve e execute esse exemplo de VBScript (SampleVB.vbs):  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints=True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
  
