---
title: Diretrizes e limitações de carregamento em massa de XML (SQLXML)
description: Saiba mais sobre as diretrizes e limitações do uso do carregamento em massa de XML no SQLXML 4,0.
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
ms.assetid: c5885d14-c7c1-47b3-a389-455e99a7ece1
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 846ba2d77f399192d3e2c2e6ea00f704f0b1fa4d
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84882976"
---
# <a name="guidelines-and-limitations-of-xml-bulk-load-sqlxml-40"></a>Diretrizes e limitações de Carregamento em Massa de XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Ao usar o Carregamento em Massa de XML, você deve estar familiarizado com as diretrizes e limitações a seguir:  
  
-   Não há suporte a esquemas embutidos.  
  
     Se houver um esquema embutido no documento XML de origem, o Carregamento em Massa de XML ignorará esse esquema. Você especifica o esquema de mapeamento para o Carregamento em Massa de XML que é externo aos dados XML. Você não pode especificar o esquema de mapeamento em um nó usando o atributo **xmlns = "x:Schema"** .  
  
-   Um documento XML é verificado para que esteja bem formado, mas ele não é validado.  
  
     O carregamento em massa de XML verifica o documento XML para determinar se ele está bem formado, ou seja, para garantir que o XML esteja em conformidade com os requisitos de sintaxe da recomendação XML 1,0 do World Wide Web Consortium. Se o documento não estiver bem formado, o Carregamento em Massa de XML cancelará o processamento e retornará um erro. A única exceção é quando o documento é um fragmento (por exemplo, o documento não tem nenhum elemento raiz), caso em que o Carregamento em Massa de XML carregará o documento.  
  
     O Carregamento em Massa de XML não valida o documento com relação a qualquer esquema DTD ou de Dados XML definido ou referenciado no arquivo de dados XML. Além disso, o Carregamento em Massa de XML não valida o arquivo de dados XML com base no esquema de mapeamento fornecido.  
  
-   Quaisquer informações de prólogo XML são ignoradas.  
  
     O carregamento em massa de XML ignora todas as informações antes e depois do \<root> elemento no documento XML. Por exemplo, o Carregamento em Massa de XML ignora qualquer declaração XML, definições de DTD internas, referências de DTD externas, comentários e assim por diante.  
  
-   Se você tiver um esquema de mapeamento que define um relacionamento de chave primária/chave estrangeira entre duas tabelas (como entre Customer e CustOrder), a tabela com a chave primária deverá ser descrita primeiro no esquema. A tabela com a coluna de chave estrangeira deve aparecer depois no esquema. O motivo disso é que a ordem na qual as tabelas são identificadas no esquema é a ordem usada para carregá-las no banco de dados. Por exemplo, o esquema XDR a seguir produzirá um erro quando ele for usado no carregamento em massa de XML, pois o **\<Order>** elemento é descrito antes do **\<Customer>** elemento. A coluna CustomerID em CustOrder é uma coluna de chave estrangeira que se refere à coluna de chave primária CustomerID na tabela Cust.  
  
    ```  
    <?xml version="1.0" ?>  
    <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
            xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
            xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
        <ElementType name="Order" sql:relation="CustOrder" >  
          <AttributeType name="OrderID" />  
          <AttributeType name="CustomerID" />  
          <attribute type="OrderID" />  
          <attribute type="CustomerID" />  
        </ElementType>  
  
       <ElementType name="CustomerID" dt:type="int" />  
       <ElementType name="CompanyName" dt:type="string" />  
       <ElementType name="City" dt:type="string" />  
  
       <ElementType name="root" sql:is-constant="1">  
          <element type="Customers" />  
       </ElementType>  
       <ElementType name="Customers" sql:relation="Cust"   
                         sql:overflow-field="OverflowColumn"  >  
          <element type="CustomerID" sql:field="CustomerID" />  
          <element type="CompanyName" sql:field="CompanyName" />  
          <element type="City" sql:field="City" />  
          <element type="Order" >   
               <sql:relationship  
                   key-relation="Cust"  
                    key="CustomerID"  
                    foreign-key="CustomerID"  
                    foreign-relation="CustOrder" />  
          </element>  
       </ElementType>  
    </Schema>  
    ```  
  
-   Se o esquema não especificar colunas de estouro usando a anotação **SQL: overflow-field** , o carregamento em massa XML ignorará todos os dados presentes no documento XML, mas não será descrito no esquema de mapeamento.  
  
     O Carregamento em Massa de XML aplica o esquema de mapeamento que você especifica sempre que encontra marcas conhecidas no fluxo de dados XML. Ele ignora dados presentes no documento XML mas não descritos no esquema. Por exemplo, suponha que você tenha um esquema de mapeamento que descreve um **\<Customer>** elemento. O arquivo de dados XML tem uma **\<AllCustomers>** marca de raiz (que não está descrita no esquema) que inclui todos os **\<Customer>** elementos:  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
      <Customer>...</Customer>  
       ...  
    </AllCustomers>  
    ```  
  
     Nesse caso, o carregamento em massa de XML ignora o **\<AllCustomers>** elemento e começa o mapeamento no **\<Customer>** elemento. O Carregamento em Massa de XML ignora os elementos não descritos no esquema mas presentes no documento XML.  
  
     Considere outro arquivo de dados de origem XML que contenha **\<Order>** elementos. Esses elementos não são descritos no esquema de mapeamento:  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
        <Order> ... </Order>  
        <Order> ... </Order>  
         ...  
      <Customer>...</Customer>  
        <Order> ... </Order>  
        <Order> ... </Order>  
         ...  
      ...  
    </AllCustomers>  
    ```  
  
     O carregamento em massa de XML ignora esses **\<Order>** elementos. Mas se você usar a anotação **SQL: overflow-field**no esquema para identificar uma coluna como uma coluna de estouro, a carga em massa XML armazenará todos os dados não consumidos nesta coluna.  
  
-   As referências de entidade e seções CDATA são traduzidas para os respectivos equivalentes de cadeia de caracteres antes de serem armazenadas no banco de dados.  
  
     Neste exemplo, uma seção CDATA encapsula o valor do **\<City>** elemento. O carregamento em massa de XML extrai o valor da cadeia de caracteres ("NY") antes de inserir o **\<City>** elemento no banco de dados.  
  
    ```  
    <City><![CDATA[NY]]> </City>  
    ```  
  
     O Carregamento em Massa de XML não preserva as referências de entidade.  
  
-   Se o esquema de mapeamento especificar o valor padrão de um atributo e os dados de origem XML não contiverem esse atributo, o Carregamento em Massa de XML usará o valor padrão.  
  
     O seguinte esquema XDR de exemplo atribui um valor padrão ao atributo **HireDate** :  
  
    ```  
    <?xml version="1.0" ?>  
    <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
            xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
            xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
       <ElementType name="root" sql:is-constant="1">  
          <element type="Customers" />  
       </ElementType>  
  
       <ElementType name="Customers" sql:relation="Cust3" >  
          <AttributeType name="CustomerID" dt:type="int"  />  
          <AttributeType name="HireDate"  default="2000-01-01" />  
          <AttributeType name="Salary"   />  
  
          <attribute type="CustomerID" sql:field="CustomerID" />  
          <attribute type="HireDate"   sql:field="HireDate"  />  
          <attribute type="Salary"     sql:field="Salary"    />  
       </ElementType>  
    </Schema>  
    ```  
  
     Nesses dados XML, o atributo **HireDate** está faltando no segundo **\<Customers>** elemento. Quando o carregamento em massa de XML insere o segundo **\<Customers>** elemento no banco de dados, ele usa o valor padrão especificado no esquema.  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1" HireDate="1999-01-01" Salary="10000" />  
      <Customers CustomerID="2" Salary="10000" />  
    </ROOT>  
    ```  
  
-   Não há suporte para a anotação **SQL: url-encode** :  
  
     Você não pode especificar uma URL na entrada de dados XML e esperar que o Carregamento em Massa leia os dados desse local.  
  
     São criadas as tabelas identificadas no esquema de mapeamento (o banco de dados precisa existir). Se uma ou mais das tabelas já existir no banco de dados, a propriedade SGDropTables determinará se essas tabelas preexistentes devem ser descartadas e recriadas.  
  
-   Se você especificar a propriedade SchemaGen (por exemplo, SchemaGen = true), as tabelas identificadas no esquema de mapeamento serão criadas. Mas o SchemaGen não cria nenhuma restrição (como as restrições PRIMARY KEY/FOREIGN KEY) nessas tabelas com uma exceção: se os nós XML que constituem a chave primária em uma relação forem definidos como tendo um tipo XML de ID (ou seja, **Type = "xsd: ID"** para xsd) e a propriedade SGUseID for definida como true para SchemaGen, não somente as chaves primárias serão criadas a partir dos nós de ID digitados, mas as relações de chave primária/chave estrangeira serão criadas a partir do mapeamento de relações  
  
-   SchemaGen não usa facetas e extensões de esquema XSD para gerar o esquema relacional [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Se você especificar a propriedade SchemaGen (por exemplo, SchemaGen = true) no carregamento em massa, somente as tabelas (e não as exibições do nome compartilhado) especificadas serão atualizadas.  
  
-   O SchemaGen fornece apenas a funcionalidade básica para gerar o esquema relacional do XSD anotado. O usuário deve modificar as tabelas geradas manualmente, se necessário.  
  
-   Onde existe mais de uma relação entre as tabelas, SchemaGen tenta criar uma única relação que inclui todas as chaves envolvidas entre as duas tabelas. Essa limitação pode causar um erro [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
-   Quando você está carregando em massa os dados XML em um banco de dados, é necessário haver pelo menos um atributo ou elemento filho no esquema de mapeamento que esteja mapeado para uma coluna de banco de dados.  
  
-   Se você estiver inserindo valores de data usando o XML Bulk Load, eles deverão ser especificados no formato (-)CCYY-MM-DD((+-)TZ). Esse é o formato de XSD padrão para a data.  
  
-   Alguns sinalizadores de propriedade não são compatíveis com outros. Por exemplo, o carregamento em massa não dá suporte a **IgnoreDuplicateKeys = true** junto com **KEEPIDENTITY = false**. Quando **KEEPIDENTITY = false**, o carregamento em massa espera que o servidor gere os valores de chave. As tabelas devem ter uma restrição de **identidade** na chave. O servidor não gerará chaves duplicadas, o que significa que não há necessidade de **IgnoreDuplicateKeys** ser definida como **true**. **IgnoreDuplicateKeys** deve ser definido como **true** somente ao carregar valores de chave primária dos dados de entrada em uma tabela que tem linhas e há um potencial para conflito de valores de chave primária.  
  
  
