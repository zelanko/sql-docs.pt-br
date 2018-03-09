---
title: "Introdução aos diagramas de atualização (SQLXML 4.0) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2dc3ce73bfe3da97e6567c1819eea34a8bc1dfaa
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="introduction-to-updategrams-sqlxml-40"></a>Introdução aos diagramas de atualização (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Você pode modificar (Inserir, atualizar ou excluir) um banco de dados [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de um existente documento XML usando um diagrama de atualização ou o OPENXML [!INCLUDE[tsql](../../../includes/tsql-md.md)] função.  
  
 A função OPENXML modifica um banco de dados fragmentando o documento XML existente e fornecendo um conjunto de linhas que pode ser passado para uma instrução INSERT, UPDATE ou DELETE. Com OPENXML, as operações são executadas diretamente nas tabelas de banco de dados. Portanto, OPENXML é especialmente apropriada nos casos em que provedores de conjuntos de linhas, como uma tabela, possam aparecer como uma origem.  
  
 Da mesma forma que a OPENXML, um diagrama de atualização permite inserir, atualizar ou excluir dados no banco de dados. Entretanto, ele trabalha nas exibições em XML fornecidas pelo esquema XSD (ou um XDR) anotado; por exemplo, as atualizações são aplicadas à exibição em XML fornecida pelo esquema de mapeamento. O esquema de mapeamento, por sua vez, tem as informações necessárias para mapear elementos e atributos XML para as tabelas e colunas de bancos de dados correspondentes. O diagrama de atualização usa estas informações de mapeamento para atualizar as tabelas e colunas de bancos de dados.  
  
> [!NOTE]  
>  Esta documentação parte do pressuposto de que você esteja familiarizado com suporte a modelos e ao esquema de mapeamento no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Introdução a esquemas de XSD anotado &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md). Para aplicativos herdados que usam XDR, consulte [os esquemas XDR anotados &#40; preteridos no SQLXML 4.0 &#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
## <a name="required-namespaces-in-the-updategram"></a>Namespaces necessários no diagrama de atualização  
 As palavras-chave em um diagrama de atualização, como  **\<sincronização >**,  **\<antes >**, e  **\<depois >**, existem no **urn: schemas-microsoft-com: XML-diagrama de atualização** namespace. O prefixo de namespace utilizado é arbitrário. Nesta documentação, o **updg** prefixo indica o **updategram** namespace.  
  
## <a name="reviewing-syntax"></a>Revisando a sintaxe  
 Um diagrama de atualização é um modelo com  **\<sincronização >**,  **\<antes >**, e  **\<depois >** blocos que formam a sintaxe das diagrama de atualização. O seguinte código mostra esta sintaxe em sua forma mais simples:  
  
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
 Contém o  **\<antes >** e  **\<depois >** blocos. Um  **\<sincronização >** bloco pode conter mais de um conjunto de  **\<antes >** e  **\<depois >** blocos. Se houver mais de um conjunto de  **\<antes >** e  **\<depois >** blocos, esses blocos (mesmo se elas estiverem vazias) devem ser especificados como pares. Além disso, um diagrama de atualização pode ter mais de um  **\<sincronização >** bloco. Cada  **\<sincronização >** bloco é uma unidade de transação (o que significa que tudo no  **\<sincronização >** bloco ou nada é feito). Se você especificar vários  **\<sincronização >** blocos em um diagrama de atualização, a falha de um  **\<sincronização >** bloco não afetará os outros  **\<sincronização >** blocos.  
  
 Se um diagrama de atualização exclui, insere ou atualiza uma instância de registro depende do conteúdo do  **\<antes >** e  **\<depois >** blocos:  
  
-   Se uma instância de registro aparecer somente no  **\<antes >** bloco com uma instância correspondente no  **\<depois >** bloco, o diagrama de atualização executa uma operação de exclusão.  
  
-   Se uma instância de registro aparecer somente no  **\<depois >** bloco com uma instância correspondente no  **\<antes >** bloco, é uma operação de inserção.  
  
-   Se uma instância de registro aparece no  **\<antes >** bloquear e tem uma instância correspondente  **\<depois >** bloco, é uma operação de atualização. Nesse caso, o diagrama de atualização atualiza a instância de registro para os valores que são especificados no  **\<depois >** bloco.  
  
## <a name="specifying-a-mapping-schema-in-the-updategram"></a>Especificando um esquema de mapeamento no diagrama de atualização  
 Em um diagrama de atualização, a abstração XML que é fornecida por um esquema de mapeamento (é dado suporte a esquemas XSD e também XDR) pode ser implícita ou explícita (ou seja, um diagrama de atualização pode funcionar com ou sem um esquema de mapeamento especificado). Se você não especificar um esquema de mapeamento, o diagrama de atualização assumirá um mapeamento implícito (o mapeamento padrão), onde cada elemento o  **\<antes >** bloco ou  **\<depois >** bloco é mapeado para uma tabela e cada elemento filho ou atributo mapeado para uma coluna no banco de dados. Se você especificar explicitamente um esquema de mapeamento, os elementos e atributos no diagrama de atualização deverão corresponder aos elementos e atributos no esquema de mapeamento.  
  
### <a name="implicit-default-mapping"></a>Mapeamento implícito (padrão)  
 Na maioria dos casos, um diagrama de atualização que executa atualizações simples pode não precisar de um esquema de mapeamento. Neste caso, o diagrama de atualização se baseia no esquema de mapeamento padrão.  
  
 O seguinte diagrama de atualização demonstra o mapeamento implícito. Neste exemplo, o diagrama de atualização insere um novo cliente na tabela Sales.Customer. Como este diagrama de atualização usa mapeamento implícito, o \<Sales. Customer > elemento é mapeado para a tabela Sales. Customer e os atributos CustomerID e SalesPersonID são mapeados para as colunas correspondentes na tabela Sales. Customer.  
  
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
  
 Se o diagrama de atualização realizar uma atualização complexa (por exemplo, inserindo registros em várias tabelas base a relação pai-filho que é especificado no esquema de mapeamento), você deve fornecer explicitamente o esquema de mapeamento usando o  **esquema de mapeamento** atributo em relação a qual o diagrama de atualização é executado.  
  
 Como um diagrama de atualização é um modelo, o caminho especificado para o esquema de mapeamento no diagrama de atualização é relativo ao local do arquivo do modelo (relativo ao local onde o diagrama de atualização está armazenado). Para obter mais informações, consulte [especificando um esquema de mapeamento anotado em um diagrama de atualização &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="element-centric-and-attribute-centric-mapping-in-updategrams"></a>Mapeamento centrado em elemento e mapeamento centrado em atributo em diagramas de atualização  
 Com o mapeamento padrão (quando o esquema de mapeamento não for especificado no diagrama de atualização), os elementos do diagrama de atualização são mapeados para tabelas e os elementos-filho (no caso do mapeamento centrado em elementos) e os atributos (no caso do mapeamento centrado em atributos) são mapeados para colunas.  
  
### <a name="element-centric-mapping"></a>Mapeamento centrado em elemento  
 Em um diagrama de atualização centrado em elemento, um elemento contém elementos filhos que denotam as propriedades do elemento. Como um exemplo, consulte o seguinte diagrama de atualização. O  **\<Person. Contact >** elemento contém o  **\<FirstName >**e  **\<LastName >** elementos filho. Esses elementos filho são propriedades do  **\<Person. Contact >** elemento.  
  
 Como este diagrama de atualização não especifica um esquema de mapeamento, o diagrama usa o mapeamento implícito, em que o  **\<Person. Contact >** elemento é mapeado para a tabela Person. Contact e seus elementos filho são mapeados para o nome e Colunas de sobrenome.  
  
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
 Em um mapeamento centrado em atributo, os elementos têm atributos. O seguinte diagrama de atualização usa mapeamento centrado em atributo. Neste exemplo, o  **\<Person. Contact >** elemento consiste de **FirstName** e **LastName** atributos. Esses atributos são as propriedades do  **\<Person. Contact >** elemento. Como no exemplo anterior, este diagrama de atualização não especifica nenhum esquema de mapeamento, então ele se baseia em mapeamento implícito para mapear o  **\<Person. Contact >** elemento para a tabela Person. Contact e atributos do elemento para o respectivas colunas na tabela.  
  
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
 Você pode especificar uma mistura de mapeamento centrado em elemento e mapeamento centrado em atributo, conforme mostrado no seguinte diagrama de atualização. Observe que o  **\<Person. Contact >** elemento contém um atributo e um elemento filho. Além disso, este diagrama de atualização se baseia em mapeamento implícito. Portanto, o **FirstName** atributo e o  **\<LastName >** são mapeados para as colunas correspondentes na tabela Person. Contact.  
  
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
  
 Para codificar caracteres que são válidos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] identificadores mas não são identificadores válidos em XML, use ' __xHHHH\_\_' como valor de codificação, onde HHHH representa para o código UCS-2 hexadecimal de quatro dígitos do caractere na mais ordem do primeiro bit significativo. Usando esse esquema de codificação, um caractere de espaço é substituído por x0020 (o quatro dígitos hexadecimal código para um caractere de espaço); Portanto, o nome da tabela [Order Details] no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se torna _x005B_Order_x0020_Details_x005D\_ em XML.  
  
 Da mesma forma, talvez seja necessário especificar nomes de elemento de três partes, como \<[banco de dados]. [ proprietário]. [tabela] >. Como os caracteres de colchetes ([e]) não são válidos em XML, você deve especificar como \<_x005B_database_x005D\_._x005B_owner_x005D\_._x005B_table_x005D\_>, onde _x005B\_ é o codificação para o colchete esquerdo ([) e _x005D\_ é a codificação para o colchete direito (]).  
  
## <a name="executing-updategrams"></a>Executando diagramas de atualização  
 Como um diagrama de atualização é um modelo, todos os mecanismos de processamento de um modelo se aplicam ao diagrama de atualização. Para SQLXML 4.0, você pode executar um diagrama de atualização em qualquer um dos seguintes modos:  
  
-   Enviando-o em um comando ADO.  
  
-   Enviando-o como um comando OLE DB.  
  
## <a name="see-also"></a>Consulte também  
 [Considerações de segurança do diagrama &#40; SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
