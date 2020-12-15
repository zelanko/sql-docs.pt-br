---
title: Introdução aos Updategrams (SQLXML)
description: Saiba mais sobre os Updategrams do SQLXML 4,0 que podem ser usados para inserir, atualizar ou excluir dados em um banco de dado.
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- explicit schema mapping [SQLXML]
- updategrams [SQLXML], mapping schema specifying
- namespaces [SQLXML]
- updategrams [SQLXML], about updategrams
- attribute-centric mapping
- invalid characters [SQLXML]
- element-centric mapping [SQLXML]
- mapping schema [SQLXML], updategrams
- namespaces [SQLXML], updategrams
- executing updategrams [SQLXML]
- implicit schema mapping
ms.assetid: cfe24e82-a645-4f93-ab16-39c21f90cce6
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ce05847c88ca60e2635ca6d27f1558edafac04e0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97430336"
---
# <a name="introduction-to-updategrams-sqlxml-40"></a>Introdução aos diagramas de atualização (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Você pode modificar (inserir, atualizar ou excluir) um banco de dados [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do em um documento XML existente usando um updategram ou a [!INCLUDE[tsql](../../../includes/tsql-md.md)] função OPENXML.  
  
 A função OPENXML modifica um banco de dados fragmentando o documento XML existente e fornecendo um conjunto de linhas que pode ser passado para uma instrução INSERT, UPDATE ou DELETE. Com OPENXML, as operações são executadas diretamente nas tabelas de banco de dados. Portanto, OPENXML é especialmente apropriada nos casos em que provedores de conjuntos de linhas, como uma tabela, possam aparecer como uma origem.  
  
 Da mesma forma que a OPENXML, um diagrama de atualização permite inserir, atualizar ou excluir dados no banco de dados. Entretanto, ele trabalha nas exibições em XML fornecidas pelo esquema XSD (ou um XDR) anotado; por exemplo, as atualizações são aplicadas à exibição em XML fornecida pelo esquema de mapeamento. O esquema de mapeamento, por sua vez, tem as informações necessárias para mapear elementos e atributos XML para as tabelas e colunas de bancos de dados correspondentes. O diagrama de atualização usa estas informações de mapeamento para atualizar as tabelas e colunas de bancos de dados.  
  
> [!NOTE]  
>  Esta documentação parte do pressuposto de que você esteja familiarizado com suporte a modelos e ao esquema de mapeamento no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [introdução aos esquemas XSD anotados &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md). Para aplicativos herdados que usam XDR, consulte [esquemas XDR anotados &#40;preteridos no SQLXML 4,0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
## <a name="required-namespaces-in-the-updategram"></a>Namespaces necessários no diagrama de atualização  
 As palavras-chave em um updategram, como, **\<sync>** **\<before>** e **\<after>** , existem no namespace **urn: schemas-microsoft-com: xml-updategram** . O prefixo de namespace utilizado é arbitrário. Nesta documentação, o prefixo **updg** denota o namespace do **updategram** .  
  
## <a name="reviewing-syntax"></a>Revisando a sintaxe  
 Um updategram é um modelo com **\<sync>** , **\<before>** e **\<after>** blocos que formam a sintaxe do updategram. O seguinte código mostra esta sintaxe em sua forma mais simples:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema= "AnnotatedSchemaFile.xml"] >  
    <updg:before>  
        ...  
    </updg:before>  
    <updg:after>  
        ...  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 As seguintes definições descrevem a função de cada um destes blocos:  
  
 **\<before>**  
 Identifica o estado existente (também chamado de "o estado antes") da instância de registro.  
  
 **\<after>**  
 Identifica o estado novo para o qual dados devem ser alterados.  
  
 **\<sync>**  
 Contém os **\<before>** **\<after>** blocos e. Um **\<sync>** bloco pode conter mais de um conjunto de **\<before>** **\<after>** blocos e. Se houver mais de um conjunto de **\<before>** blocos e **\<after>** , esses blocos (mesmo se estiverem vazios) deverão ser especificados como pares. Além disso, um updategram pode ter mais de um **\<sync>** bloco. Cada **\<sync>** bloco é uma unidade de transação (o que significa que tudo no **\<sync>** bloco é feito ou nada é feito). Se você especificar vários **\<sync>** blocos em um updategram, a falha de um **\<sync>** bloco não afetará os outros **\<sync>** blocos.  
  
 Se um updategram exclui, insere ou atualiza uma instância de registro depende do conteúdo dos **\<before>** **\<after>** blocos e:  
  
-   Se uma instância de registro aparecer apenas no **\<before>** bloco sem nenhuma instância correspondente no **\<after>** bloco, o updategram executará uma operação de exclusão.  
  
-   Se uma instância de registro aparecer apenas no **\<after>** bloco sem nenhuma instância correspondente no **\<before>** bloco, será uma operação de inserção.  
  
-   Se uma instância de registro aparecer no **\<before>** bloco e tiver uma instância correspondente no **\<after>** bloco, será uma operação de atualização. Nesse caso, o updategram atualiza a instância do registro para os valores especificados no **\<after>** bloco.  
  
## <a name="specifying-a-mapping-schema-in-the-updategram"></a>Especificando um esquema de mapeamento no diagrama de atualização  
 Em um diagrama de atualização, a abstração XML que é fornecida por um esquema de mapeamento (é dado suporte a esquemas XSD e também XDR) pode ser implícita ou explícita (ou seja, um diagrama de atualização pode funcionar com ou sem um esquema de mapeamento especificado). Se você não especificar um esquema de mapeamento, o updategram assumirá um mapeamento implícito (o mapeamento padrão), em que cada elemento no **\<before>** bloco ou **\<after>** bloco é mapeado para uma tabela e o elemento ou atributo filho de cada elemento é mapeado para uma coluna no banco de dados. Se você especificar explicitamente um esquema de mapeamento, os elementos e atributos no diagrama de atualização deverão corresponder aos elementos e atributos no esquema de mapeamento.  
  
### <a name="implicit-default-mapping"></a>Mapeamento implícito (padrão)  
 Na maioria dos casos, um diagrama de atualização que executa atualizações simples pode não precisar de um esquema de mapeamento. Neste caso, o diagrama de atualização se baseia no esquema de mapeamento padrão.  
  
 O seguinte diagrama de atualização demonstra o mapeamento implícito. Neste exemplo, o diagrama de atualização insere um novo cliente na tabela Sales.Customer. Como esse updategram usa o mapeamento implícito, o \<Sales.Customer> elemento é mapeado para a tabela Sales. Customer e os atributos CustomerID e vendedorid são mapeados para as colunas correspondentes na tabela Sales. Customer.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
</updg:before>  
<updg:after>  
    <Sales.Customer CustomerID="1" SalesPersonID="277" />  
    </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="explicit-mapping"></a>Mapeamento explícito  
 Se você especificar um esquema de mapeamento (XSD ou XDR), o diagrama de atualização usará o esquema para determinar as tabelas e colunas do banco de dados que deverão ser atualizados.  
  
 Se o updategram executar uma atualização complexa (por exemplo, inserir registros em várias tabelas com base na relação pai-filho especificada no esquema de mapeamento), você deverá fornecer explicitamente o esquema de mapeamento usando o atributo **Mapping-Schema** no qual o updategram é executado.  
  
 Como um diagrama de atualização é um modelo, o caminho especificado para o esquema de mapeamento no diagrama de atualização é relativo ao local do arquivo do modelo (relativo ao local onde o diagrama de atualização está armazenado). Para obter mais informações, consulte [especificando um esquema de mapeamento anotado em um Updategram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="element-centric-and-attribute-centric-mapping-in-updategrams"></a>Mapeamento centrado em elemento e mapeamento centrado em atributo em diagramas de atualização  
 Com o mapeamento padrão (quando o esquema de mapeamento não for especificado no diagrama de atualização), os elementos do diagrama de atualização são mapeados para tabelas e os elementos-filho (no caso do mapeamento centrado em elementos) e os atributos (no caso do mapeamento centrado em atributos) são mapeados para colunas.  
  
### <a name="element-centric-mapping"></a>Mapeamento centrado em elemento  
 Em um diagrama de atualização centrado em elemento, um elemento contém elementos filhos que denotam as propriedades do elemento. Como um exemplo, consulte o seguinte diagrama de atualização. O **\<Person.Contact>** elemento contém os **\<FirstName>** **\<LastName>** elementos filho e. Esses elementos filho são propriedades do **\<Person.Contact>** elemento.  
  
 Como esse updategram não especifica um esquema de mapeamento, o updategram usa o mapeamento implícito, em que o **\<Person.Contact>** elemento é mapeado para a tabela Person. Contact e seus elementos filho são mapeados para as colunas FirstName e LastName.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:after>  
    <Person.Contact>  
       <FirstName>Catherine</FirstName>  
       <LastName>Abel</LastName>  
    </Person.Contact>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="attribute-centric-mapping"></a>mapeamento centrado em atributo  
 Em um mapeamento centrado em atributo, os elementos têm atributos. O seguinte diagrama de atualização usa mapeamento centrado em atributo. Neste exemplo, o **\<Person.Contact>** elemento consiste nos atributos **FirstName** e **LastName** . Esses atributos são as propriedades do **\<Person.Contact>** elemento. Como no exemplo anterior, este updategram não especifica nenhum esquema de mapeamento, portanto, ele se baseia no mapeamento implícito para mapear o **\<Person.Contact>** elemento para a tabela Person. Contact e os atributos do elemento para as respectivas colunas na tabela.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
    <Person.Contact FirstName="Catherine" LastName="Abel" />  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="using-both-element-centric-and-attribute-centric-mapping"></a>Usando o mapeamento centrado em elemento e centrado em atributo  
 Você pode especificar uma mistura de mapeamento centrado em elemento e mapeamento centrado em atributo, conforme mostrado no seguinte diagrama de atualização. Observe que o **\<Person.Contact>** elemento contém um atributo e um elemento filho. Além disso, este diagrama de atualização se baseia em mapeamento implícito. Assim, o atributo **FirstName** e o **\<LastName>** elemento filho são mapeados para as colunas correspondentes na tabela Person. Contact.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
    <Person.Contact FirstName="Catherine" >  
       <LastName>Abel</LastName>  
    </Person.Contact>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="working-with-characters-valid-in-sql-server-but-not-valid-in-xml"></a>Trabalhando com caracteres válidos no SQL Server, mas não válidos em XML  
 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], os nomes de tabela podem incluir um espaço. Porém, este tipo de nome de tabela não é válido em XML.  
  
 Para codificar caracteres que são [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] identificadores válidos, mas não são identificadores XML válidos, use ' __xHHHH \_ \_ ' como o valor de codificação, em que HHHH significa o código UCS-2 hexadecimal de quatro dígitos para o caractere na ordem de bits mais significativa. Usando esse esquema de codificação, um caractere de espaço é substituído por x0020 (o código hexadecimal de quatro dígitos para um caractere de espaço); Portanto, o nome da tabela [Order Details] in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se torna _x005B_Order_x0020_Details_x005D \_ em XML.  
  
 Da mesma forma, talvez seja necessário especificar nomes de elementos de três partes, como \<[database].[owner].[table]> . Como os caracteres de colchetes ([e]) não são válidos em XML, você deve especificar isso como \<_x005B_database_x005D\_._x005B_owner_x005D\_._x005B_table_x005D\_> , em que _x005B \_ é a codificação para o colchete esquerdo ([) e _x005D \_ é a codificação para o colchete direito (]).  
  
## <a name="executing-updategrams"></a>Executando diagramas de atualização  
 Como um diagrama de atualização é um modelo, todos os mecanismos de processamento de um modelo se aplicam ao diagrama de atualização. Para SQLXML 4.0, você pode executar um diagrama de atualização em qualquer um dos seguintes modos:  
  
-   Enviando-o em um comando ADO.  
  
-   Enviando-o como um comando OLE DB.  
  
## <a name="see-also"></a>Consulte Também  
 [Considerações de segurança do updategram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
