---
title: Comparar XML tipado com XML não tipado | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xml data type [SQL Server], variables
- parameters [XML in SQL Server]
- facets [XML in SQL Server]
- xml data type [SQL Server], columns
- untyped XML
- xml data type [SQL Server], typed xml
- XML [SQL Server], typed
- variables [XML in SQL Server], creating
- xml data type [SQL Server], untyped xml
- columns [XML in SQL Server], creating
- typed XML
- document mode processing [SQL Server]
- XML [SQL Server], untyped
- xml data type [SQL Server], parameters
ms.assetid: 4bc50af9-2f7d-49df-bb01-854d080c72c7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f1a8113ba4f9df20fcf11a7f4662abb1f2a24b5c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47841274"
---
# <a name="compare-typed-xml-to-untyped-xml"></a>Comparar XML digitado com XML não digitado
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  É possível criar variáveis, parâmetros e colunas do tipo **xml** . Opcionalmente, é possível associar uma coleção de esquemas XML a uma variável, parâmetro ou coluna de tipo **xml** . Nesse caso, a instância do tipo de dados **xml** é chamada *com tipo*. Caso contrário, a instância XML é chamada *sem-tipo*.  
  
## <a name="well-formed-xml-and-the-xml-data-type"></a>XML bem formado e o tipo de dados xml  
 O tipo de dados **xml** implementa o tipo de dados **xml** padrão ISO. Portanto ele pode armazenar documentos bem formados em XML versão 1.0 e também os chamados fragmentos de conteúdo XML com nós de texto e um número arbitrário de elementos de nível superior em uma coluna XML sem-tipo. Os sistema verifica se os dados estão bem formados, se não requerem que a coluna esteja associada a esquemas XML e rejeita dados que não são bem formados no sentido estendido. Isso também é verdadeiro para variáveis e parâmetros XML sem-tipo.  
  
## <a name="xml-schemas"></a>Esquemas XML  
 Um esquema XML fornece o seguinte:  
  
-   **Restrições de validação.** Sempre que uma instância xml com tipo é atribuída ou modificada, o SQL Server a valida.  
  
-   **Informações sobre tipos de dados.** Os esquemas fornecem informações sobre os tipos de atributos e elementos na instância de tipo de dados **xml** . As informações de tipo fornecem semântica operacional mais precisa aos valores contidos na instância do que é possível com **xml**sem tipo. Por exemplo, podem ser executadas operações aritméticas decimais em um valor decimal, mas não em um valor de cadeia de caracteres. Por causa disso, o armazenamento de XML com tipo pode ser feito de maneira significativamente mais compacta do que o XML sem-tipo.  
  
## <a name="choosing-typed-or-untyped-xml"></a>Escolhendo XML com tipo ou sem-tipo  
 Use o tipo de dados **xml** sem tipo nas seguintes situações:  
  
-   Você não tem um esquema para obter os dados XML.  
  
-   Você tem esquemas, mas não quer que o servidor valide os dados. Algumas vezes, esse é o caso quando um aplicativo executa validação do lado do cliente antes de armazenar os dados no servidor ou armazena temporariamente os dados XML que são inválidos de acordo com o esquema ou usa componentes de esquema que não têm suporte no servidor.  
  
 Use o tipo de dados **xml** com tipo nas seguintes situações:  
  
-   Você tem esquemas para os dados XML e quer que o servidor valide os dados XML de acordo com os esquemas XML.  
  
-   Você quer usufruir de otimizações de consulta e de armazenamento com base em informações de tipo.  
  
-   Você quer usufruir melhor de informações de tipo durante a compilação de suas consultas.  
  
 Colunas, parâmetros e variáveis de XML com tipo podem armazenar conteúdo ou documentos XML. No entanto é necessário especificar com um sinalizador se você está armazenando um documento ou conteúdo no momento da declaração. Além disso, você precisa fornecer a coleção de esquemas XML. Especifique DOCUMENT se cada instância XML tiver exatamente um elemento de nível superior. Caso contrário, use CONTENT. O compilador de consultas usa o sinalizador DOCUMENT em verificações de tipo durante a compilação de consultas para deduzir elementos singleton de nível superior.  
  
## <a name="creating-typed-xml"></a>Criando XML com tipo  
 Antes de criar variáveis, parâmetros ou colunas **xml** com tipo, você deve primeiro registrar a coleção de esquema XML usando [CREATE XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md). Em seguida, você pode associar a coleção de esquema XML a variáveis, parâmetros ou colunas do tipo de dados **xml**.  
  
 Nos exemplos a seguir, uma convenção de nomenclatura de duas partes é usada para especificar o nome da coleção de esquema XML. A primeira parte é o nome do esquema e a segunda parte é o nome da coleção de esquema XML.  
  
### <a name="example-associating-a-schema-collection-with-an-xml-type-variable"></a>Exemplo: Associando uma coleção de esquema com uma variável de tipo xml  
 O exemplo a seguir cria uma variável de tipo **xml** e associa uma coleção de esquema a ela. A coleção de esquema especificada no exemplo já está importada no banco de dados **AdventureWorks** .  
  
```  
DECLARE @x xml (Production.ProductDescriptionSchemaCollection);   
```  
  
### <a name="example-specifying-a-schema-for-an-xml-type-column"></a>Exemplo: Especificando um esquema para uma coluna de tipo xml  
 O exemplo a seguir cria uma tabela com uma coluna de tipo **xml** e especifica um esquema para a coluna:  
  
```  
CREATE TABLE T1(  
 Col1 int,   
 Col2 xml (Production.ProductDescriptionSchemaCollection)) ;  
```  
  
### <a name="example-passing-an-xml-type-parameter-to-a-stored-procedure"></a>Exemplo: Passando um parâmetro de tipo xml para um procedimento armazenado  
 O exemplo a seguir passa um parâmetro de tipo **xml** para um procedimento armazenado e especifica um esquema para a variável:  
  
```  
CREATE PROCEDURE SampleProc   
  @ProdDescription xml (Production.ProductDescriptionSchemaCollection)   
AS   
...  
```  
  
 Observe o seguinte sobre a coleção de esquema XML:  
  
-   Uma coleção de esquema XML está disponível apenas no banco de dados no qual ela foi registrada usando [Criando uma coleção de esquema XML](../../t-sql/statements/create-xml-schema-collection-transact-sql.md).  
  
-   Se você converter de um tipo de dados de cadeia de caracteres em **xml** com tipo, a análise também executará validação e classificação de tipo com base nos namespaces do esquema XML na coleção especificada.  
  
-   Você pode converter de um tipo de dados **xml** com tipo em um tipo de dados **xml** sem tipo e vice-versa.  
  
 Para obter mais informações sobre outras maneiras de gerar XML no SQL Server, consulte [Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md). Depois que o XML é gerado, ele pode ser atribuído a uma variável de tipo de dados **xml** ou armazenado em colunas de tipo **xml** para processamento adicional.  
  
 Na hierarquia de tipo de dados, o tipo de dados **xml** aparece abaixo dos tipos de dados **sql_variant** e definidos pelo usuário, mas acima de qualquer tipo interno.  
  
### <a name="example-specifying-facets-to-constrain-a-typed-xml-column"></a>Exemplo: Especificando facetas para restringir uma coluna xml com tipo  
 Para colunas **xml** com tipo, é possível restringir a coluna para permitir que apenas elementos únicos de nível superior de cada instância sejam armazenados nela. Isso é feito especificando a faceta opcional `DOCUMENT` ao criar uma tabela, conforme mostrado no exemplo a seguir:  
  
```  
CREATE TABLE T(Col1 xml   
   (DOCUMENT Production.ProductDescriptionSchemaCollection));  
GO  
DROP TABLE T;  
GO  
```  
  
 Por padrão, instâncias armazenadas na coluna **xml** com tipo são armazenadas como conteúdo XML e não como documentos XML. Isto permite o seguinte:  
  
-   Zero ou muitos elementos de nível superior  
  
-   Nós de texto em elementos de nível superior  
  
 Você também pode especificar explicitamente esse comportamento adicionando a faceta `CONTENT` , conforme mostrado no exemplo a seguir:  
  
```  
CREATE TABLE T(Col1 xml(CONTENT Production.ProductDescriptionSchemaCollection));  
GO -- Default  
```  
  
 Observe que você pode especificar as facetas opcionais DOCUMENT/CONTENT em qualquer lugar que definir o tipo **xml** (xml com tipo). Quando você cria uma variável **xml** com tipo, pode adicionar a faceta DOCUMENT/CONTENT, conforme mostrado no exemplo a seguir:  
  
```  
declare @x xml (DOCUMENT Production.ProductDescriptionSchemaCollection);  
```  
  
## <a name="document-type-definition-dtd"></a>DTD (Definição de Tipo de Documento)  
 As colunas, variáveis e parâmetros de tipo de dados **xml** podem ter o tipo definido usando esquema XML, mas não usando DTD. No entanto DTD embutido pode ser usado para XML com tipo e sem-tipo para fornecer valores padrão e para substituir referências a entidades com seus formulários expandidos.  
  
 É possível converter documentos de esquema DTD em XML usando ferramentas de terceiros e carregar os esquemas XML no banco de dados.  
  
## <a name="upgrading-typed-xml-from-sql-server-2005"></a>Atualizando XML com tipo a partir do SQL Server 2005  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] fez várias extensões ao suporte do Esquema XML, incluindo suporte para validação incerta, manipulação melhorada de dados das instâncias **xs:date**, **xs:time** e **xs:dateTime** e suporte adicionado para tipos de lista e de união. Na maior parte dos casos, as alterações não afetam a experiência de atualização. No entanto, se você usou uma coleção de Esquemas XML no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] que permitiu valores do tipo **xs:date**, **xs:time**ou **xs:dateTime** (ou qualquer subtipo), as seguintes etapas de atualização ocorrerão quando você anexar o banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a uma versão posterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
1.  Para cada coluna XML que recebe tipo com uma Coleção de Esquema XML que contém elementos ou atributos que recebem o tipo de **xs:anyType**, **xs:anySimpleType**, **xs:date** ou qualquer um de seus subtipos, **xs:time** ou qualquer um de seus subtipos, ou **xs:dateTime** ou qualquer um de seus subtipos, ou são de tipo de união ou de lista contendo qualquer um desses tipos, ocorre o seguinte:  
  
    1.  Todos os índices XML da coluna serão desabilitados.  
  
    2.  Todos os valores do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] continuarão a ser representados no fuso horário Z, pois foram normalizados para o fuso horário Z.  
  
    3.  Quaisquer valores de **xs:date** ou **xs:dateTime** menores que 1º de janeiro do ano 1 resultarão em um erro em tempo de execução quando o índice for reconstruído ou uma instrução XQuery ou XML-DML for executada em relação ao tipo de dados XML que contém esse valor.  
  
2.  Quaisquer anos negativos nas facetas **xs:date** ou **xs:dateTime** ou valores padrão em uma coleção de esquema XML serão atualizados automaticamente para o menor valor permitido pelo tipo **xs:date** ou **xs:dateTime** (por exemplo, 0001-01-01T00:00:00.0000000Z para **xs:dateTime**).  
  
 Observe que você ainda pode usar uma instrução select SQL simples para recuperar o tipo de dados XML inteiro, mesmo que ele contenha anos negativos. É recomendável substituir anos negativos por um ano dentro do intervalo com suporte recente ou alterar o tipo do elemento ou atributo para **xs:string**.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [Métodos de tipos de dados xml](../../t-sql/xml/xml-data-type-methods.md)   
 [Linguagem de modificação de dados XML &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)   
 [Dados XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
