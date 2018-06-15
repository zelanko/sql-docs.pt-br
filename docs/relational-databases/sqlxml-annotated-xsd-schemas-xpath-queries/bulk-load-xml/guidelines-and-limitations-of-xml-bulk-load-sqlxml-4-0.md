---
title: Diretrizes e limitações de XML em massa Load (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
ms.assetid: c5885d14-c7c1-47b3-a389-455e99a7ece1
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4b0796f498bd70f5b16ceb50b82843cc891652bf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32972471"
---
# <a name="guidelines-and-limitations-of-xml-bulk-load-sqlxml-40"></a>Diretrizes e limitações de Carregamento em Massa de XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Ao usar o Carregamento em Massa de XML, você deve estar familiarizado com as diretrizes e limitações a seguir:  
  
-   Não há suporte a esquemas embutidos.  
  
     Se houver um esquema embutido no documento XML de origem, o Carregamento em Massa de XML ignorará esse esquema. Você especifica o esquema de mapeamento para o Carregamento em Massa de XML que é externo aos dados XML. Você não pode especificar o esquema de mapeamento em um nó usando o **xmlns = "x:Schema"** atributo.  
  
-   Um documento XML é verificado para que esteja bem formado, mas ele não é validado.  
  
     O Carregamento em Massa de XML verifica o documento XML para determinar se ele está bem formado – ou seja, para garantir que o XML se conforme com os requisitos de sintaxe da recomendação feita pelo World Wide Web Consortium para o XML 1.0. Se o documento não estiver bem formado, o Carregamento em Massa de XML cancelará o processamento e retornará um erro. A única exceção é quando o documento é um fragmento (por exemplo, o documento não tem nenhum elemento raiz), caso em que o Carregamento em Massa de XML carregará o documento.  
  
     O Carregamento em Massa de XML não valida o documento com relação a qualquer esquema DTD ou de Dados XML definido ou referenciado no arquivo de dados XML. Além disso, o Carregamento em Massa de XML não valida o arquivo de dados XML com base no esquema de mapeamento fornecido.  
  
-   Quaisquer informações de prólogo XML são ignoradas.  
  
     Carregamento em massa de XML ignora todas as informações antes e depois o \<raiz > elemento no documento XML. Por exemplo, o Carregamento em Massa de XML ignora qualquer declaração XML, definições de DTD internas, referências de DTD externas, comentários e assim por diante.  
  
-   Se você tiver um esquema de mapeamento que define um relacionamento de chave primária/chave estrangeira entre duas tabelas (como entre Customer e CustOrder), a tabela com a chave primária deverá ser descrita primeiro no esquema. A tabela com a coluna de chave estrangeira deve aparecer depois no esquema. A razão para isso é que a ordem na qual as tabelas são identificadas no esquema é a ordem em que é usada para carregá-los no banco de dados. Por exemplo, o esquema XDR a seguir produzirá um erro quando ele é usado no carregamento em massa de XML porque a  **\<ordem >** elemento é descrito antes do  **\<cliente >** elemento. A coluna CustomerID em CustOrder é uma coluna de chave estrangeira que se refere à coluna de chave primária CustomerID na tabela Cust.  
  
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
  
-   Se o esquema não especificar colunas de estouro usando o **SQL: overflow-campo** anotação, carregamento em massa de XML ignora todos os dados que está presente no documento XML, mas não descritos no esquema de mapeamento.  
  
     O Carregamento em Massa de XML aplica o esquema de mapeamento que você especifica sempre que encontra marcas conhecidas no fluxo de dados XML. Ele ignora dados presentes no documento XML mas não descritos no esquema. Por exemplo, suponha que você tem um esquema de mapeamento que descreve um  **\<cliente >** elemento. O arquivo de dados XML tem uma  **\<AllCustomers >** raiz marca (que não é descrita no esquema) que inclui todos os  **\<cliente >** elementos:  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
      <Customer>...</Customer>  
       ...  
    </AllCustomers>  
    ```  
  
     Nesse caso, o XML Bulk Load ignora o  **\<AllCustomers >** elemento e começa o mapeamento no  **\<cliente >** elemento. O Carregamento em Massa de XML ignora os elementos não descritos no esquema mas presentes no documento XML.  
  
     Considere outro arquivo XML de dados de origem que contém  **\<ordem >** elementos. Esses elementos não são descritos no esquema de mapeamento:  
  
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
  
     Carregamento em massa de XML ignora esses  **\<ordem >** elementos. Porém, se você usar o **SQL: overflow-campo**anotação no esquema para identificar uma coluna como uma coluna de estouro, o XML Bulk Load armazena todos os dados não consumidos nessa coluna.  
  
-   As referências de entidade e seções CDATA são traduzidas para os respectivos equivalentes de cadeia de caracteres antes de serem armazenadas no banco de dados.  
  
     Neste exemplo, uma seção CDATA envolve o valor para o  **\<cidade >** elemento. Carregamento em massa de XML extrai o valor de cadeia de caracteres ("NY") antes de ele insere o  **\<cidade >** elemento no banco de dados.  
  
    ```  
    <City><![CDATA[NY]]> </City>  
    ```  
  
     O Carregamento em Massa de XML não preserva as referências de entidade.  
  
-   Se o esquema de mapeamento especificar o valor padrão de um atributo e os dados de origem XML não contiverem esse atributo, o Carregamento em Massa de XML usará o valor padrão.  
  
     O esquema XDR de exemplo a seguir atribui um valor padrão para o **HireDate** atributo:  
  
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
  
     Em dados XML, o **HireDate** atributo está ausente na segunda  **\<clientes >** elemento. Quando o XML Bulk Load insere o segundo  **\<clientes >** elemento no banco de dados, ele usa o valor padrão especificado no esquema.  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1" HireDate="1999-01-01" Salary="10000" />  
      <Customers CustomerID="2" Salary="10000" />  
    </ROOT>  
    ```  
  
-   O **SQL: url-encode** anotação não é suportada:  
  
     Você não pode especificar uma URL na entrada de dados XML e esperar que o Carregamento em Massa leia os dados desse local.  
  
     São criadas as tabelas identificadas no esquema de mapeamento (o banco de dados precisa existir). Se já existir um ou mais das tabelas no banco de dados, a propriedade SGDropTables determina se essas tabelas preexistentes devem ser descartadas e recriadas.  
  
-   Se você especificar a propriedade SchemaGen (por exemplo, SchemaGen = true), são criadas as tabelas são identificadas no esquema de mapeamento. Mas SchemaGen não cria restrições (como as restrições PRIMARY KEY/FOREIGN KEY) nessas tabelas com uma exceção: se os nós XML que constituem a chave primária em uma relação são definidos como tendo um tipo XML de ID (ou seja, **tipo = "xsd: ID"** para XSD) e a propriedade SGUseID está definida como True para SchemaGen, não apenas as chaves primárias criadas a partir de nós de digitado a ID, mas primárias/chave relações de chave estrangeira são criadas a partir de relacionamentos de esquema de mapeamento.  
  
-   SchemaGen não usa facetas de esquema XSD e extensões para gerar o relacional [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esquema.  
  
-   Se você especificar a propriedade SchemaGen (por exemplo, SchemaGen = true) em carregamento em massa, somente tabelas (e não as exibições do nome compartilhado) especificadas são atualizados.  
  
-   SchemaGen só oferece funcionalidade básica para gerar o esquema relacional do XSD anotado. O usuário deve modificar as tabelas geradas manualmente, se necessário.  
  
-   Quando mais de uma relação existe entre tabelas, SchemaGen tenta criar um único relacionamento que inclui todas as chaves envolvidas entre as duas tabelas. Essa limitação pode causar um erro [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
-   Quando você está carregando em massa os dados XML em um banco de dados, é necessário haver pelo menos um atributo ou elemento filho no esquema de mapeamento que esteja mapeado para uma coluna de banco de dados.  
  
-   Se você estiver inserindo valores de data usando o XML Bulk Load, eles deverão ser especificados no formato (-)CCYY-MM-DD((+-)TZ). Esse é o formato de XSD padrão para a data.  
  
-   Alguns sinalizadores de propriedade não são compatíveis com outros. Por exemplo, o carregamento em massa não suporta **Ignoreduplicatekeys = true** junto com **Keepidentity = false**. Quando **Keepidentity = false**, carregamento em massa espera o servidor para gerar os valores de chave. Tabelas devem ter um **identidade** restrição de chave. O servidor não irá gerar chaves duplicadas, que significa que não é necessário para **Ignoreduplicatekeys** seja definida como **true**. **IgnoreDuplicateKeys** deve ser definido como **true** somente ao carregar valores de chave primária dos dados de entrada em uma tabela que tem linhas e houver um possível conflito dos valores de chave primária.  
  
  
