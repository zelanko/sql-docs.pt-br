---
title: "Requisitos e limitações de uso de coleções de esquema XML no servidor | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- identifiers [XML schema collections]
- XML schema collections [SQL Server], limitations
- substitution groups [XML in SQL Server]
- XML schema collections [SQL Server], guidelines
- lax validation
- enumeration facets [XML in SQL Server]
- decimal precision [XML in SQL Server]
- repeated XML schema collection values
- schema collections [SQL Server], limitations
- time zones [XML in SQL Server]
- precision decimals [XML in SQL Server]
- schema collections [SQL Server], guidelines
- lexical representation
ms.assetid: c2314fd5-4c6d-40cb-a128-07e532b40946
caps.latest.revision: 84
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f1cf19211d774242d0f4b88bc089fb8ece06b511
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="requirements-and-limitations-for-xml-schema-collections-on-the-server"></a>Requisitos e limitações de uso de coleções de esquema XML no servidor
  A validação da linguagem de definição de esquema XML (XSD) apresenta algumas limitações em relação a colunas SQL que usam o tipo de dados **xml** . A tabela a seguir fornece detalhes sobre essas limitações e diretrizes para modificação de seu esquema XSD para que ele possa funcionar com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os tópicos nesta seção fornecem informações adicionais sobre limitações específicas e diretrizes para trabalhar com elas.  
  
|Item|Limitação|  
|----------|----------------|  
|**minOccurs** e **maxOccurs**|Os valores dos atributos **minOccurs** e **maxOccurs** devem ser ajustados em inteiros de 4 bytes. Os esquemas que não estiverem de acordo serão rejeitados pelo servidor.|  
|**\<xsd:choice>**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rejeita os esquemas que têm uma partícula **\<xsd:choice>** sem filhos, a menos que a partícula seja definida com um atributo **minOccurs** com valor zero.|  
|**\<xsd:include>**|Atualmente, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte a esse elemento. Os esquemas XML que incluem esse elemento são rejeitados pelo servidor.<br /><br /> Como uma solução, os esquemas XML que incluem a diretiva **\<xsd:include>** podem ser pré-processados para copiar e mesclar o conteúdo de qualquer esquema incluído em um único esquema para o upload no servidor. Para obter mais informações, veja [Pré-processar um esquema para mesclar esquemas incluídos](../../relational-databases/xml/preprocess-a-schema-to-merge-included-schemas.md).|  
|**\<xsd:key>**, **\<xsd:keyref>** e **\<xsd:unique>**|Atualmente, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte a essas restrições baseadas em XSD para impor exclusividade ou estabelecer chaves e referências a chaves. Os esquemas XML que contêm esses elementos não podem ser registrados.|  
|**\<xsd:redefine>**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte a esse elemento. Para obter informações sobre outra maneira de atualizar esquemas, veja [O elemento &#60;xsd:redefine&#62; Element](../../relational-databases/xml/the-xsd-redefine-element.md).|  
|Valores **\<xsd:simpleType>**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte apenas à precisão de milissegundos para tipos simples que têm componentes de segundos diferentes de **xs:time** e **xs:dateTime**e à precisão de 100 nanossegundos para **xs:time** e **xs:dateTime**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] impõe limitações em todas as enumerações de tipo simples XSD reconhecidas.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não dá suporte ao uso do valor “NaN” nas declarações **\<xsd:simpleType>**.<br /><br /> Para obter mais informações, veja[Valores para declarações &#60;xsd:simpleType&#62;](../../relational-databases/xml/values-for-xsd-simpletype-declarations.md).|  
|**xsi:schemaLocation** e **xsi:noNamespaceSchemaLocation**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ignorará esses atributos se eles estiverem presentes nos dados da instância XML inseridos em uma coluna ou variável de tipo de dados **xml** .|  
|**xs:QName**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte a tipos derivados de **xs:QName** que usam um elemento de restrição de Esquema XML.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte a tipos de união com **xs:QName** como um elemento membro.<br /><br /> Para obter mais informações, consulte [The xs:QName Type](../../relational-databases/xml/the-xs-qname-type.md).|  
|Adicionando membros a um grupo de substituição existente|Não é possível adicionar membros a um grupo de substituições existente em uma coleção de esquema XML. Um grupo de substituição em um esquema XML é restrito no sentido de que o elemento principal e todos os seus elementos membros devem ser definidos na mesma instrução {CREATE &#124; ALTER} XML SCHEMA COLLECTION.|  
|Formas canônicas e restrições de padrões|A representação canônica de um valor não pode violar a restrição de padrão de seu tipo. Para obter mais informações, consulte [Canonical Forms and Pattern Restrictions](../../relational-databases/xml/canonical-forms-and-pattern-restrictions.md).|  
|Aspectos de enumeração|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte a esquemas XML com tipos que têm aspectos padrão ou enumerações que violam essas facetas.|  
|Comprimento do aspecto|Os aspectos **length**, **minLength**e **maxLength** são armazenados como um tipo **long** . Esse é um tipo de 32 bits. Portanto, o intervalo de valores aceitos para esses valores é 2^31.|  
|Atributo ID|Cada componente de esquema XML pode ter um atributo de ID. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] impõe exclusividade para as declarações **\<xsd:attribute>** do tipo **ID**, mas não armazena esses valores. O escopo para imposição de exclusividade é a instrução {CREATE &#124; ALTER} XML SCHEMA COLLECTION.|  
|Tipo ID|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte a elementos de tipo **xs:ID**, **xs:IDREF**ou **xs:IDREFS**. Um esquema pode não declarar elementos desse tipo ou elementos derivados pela restrição ou extensão desse tipo.|  
|Namespace local|O namespace local precisa ser especificado explicitamente para o elemento **\<xsd:any>**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rejeita esquemas que usam uma cadeia de caracteres vazia ("") como um valor para o atributo de namespace. Em vez disso, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exige o uso explícito de "##local" para indicar um elemento ou atributo não qualificado, como a instância do caractere curinga.|  
|Tipo misto e conteúdo simples|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte à restrição de tipo misto a conteúdo simples. Para obter mais informações, consulte [Mixed Type and Simple Content](../../relational-databases/xml/mixed-type-and-simple-content.md).|  
|Tipo NOTATION|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte ao tipo NOTATION.|  
|Condições de memória insuficiente|Ao trabalhar com grandes coleções de esquema XML, pode ocorrer uma condição de memória insuficiente. Para obter soluções para esse problema, veja [Coleções de esquemas XML grandes e condições de memória insuficiente](../../relational-databases/xml/large-xml-schema-collections-and-out-of-memory-conditions.md).|  
|Valores repetidos|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rejeita esquemas nos quais o bloco ou o atributo final repetiu valores como "restriction restriction" e "extension extension".|  
|Identificadores de componente de esquema|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] limita identificadores de componentes de esquema a um comprimento máximo de 1000 caracteres Unicode. Além disso, não há suporte para pares de caracteres substitutos dentro de identificadores.|  
|Informações de fuso horário|No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores, há suporte completo a informações de fuso horário para valores **xs:date**, **xs:time**e **xs:dateTime** para validação de Esquema XML. Com o modo de compatibilidade com versões anteriores do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , as informações de fuso horário sempre são normalizadas para o Tempo Universal Coordenado (Hora de Greenwich). Para elementos de tipo **dateTime** , o servidor converte a hora fornecida para GMT usando o valor de deslocamento (“-05:00”) e retornando a hora GMT correspondente.|  
|Tipos de união|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte a restrições de tipos de união.|  
|Decimais de precisão variáveis|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte a decimais de precisão variáveis. O tipo **xs:decimal** representa números decimais de precisão arbitrária. Processadores XML com conformidade mínima devem oferecer suporte a números decimais com um mínimo de `totalDigits=18`. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a `totalDigits=38,` , mas limita os dígitos fracionários a 10. Todos os valores **xs:decimal** de instância são representados internamente pelo servidor usando o tipo numérico SQL (38, 10).|  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Canonical Forms and Pattern Restrictions](../../relational-databases/xml/canonical-forms-and-pattern-restrictions.md)|Explica formas canônicas e restrições de padrões.|  
|[Componentes curinga e validação de conteúdo](../../relational-databases/xml/wildcard-components-and-content-validation.md)|Descreve as limitações da utilização de caracteres curingas, a validação incerta e quaisquer Elementos anyType com coleções de esquema XML.|  
|[O elemento &#60;xsd:redefine&#62; Element](../../relational-databases/xml/the-xsd-redefine-element.md)|Explica a limitação da utilização do elemento \<xsd:redefine> e descreve uma solução alternativa.|  
|[The xs:QName Type](../../relational-databases/xml/the-xs-qname-type.md)|Descreve a limitação relativa ao tipo xs:QName.|  
|[Valores para declarações &#60;xsd:simpleType&#62;](../../relational-databases/xml/values-for-xsd-simpletype-declarations.md)|Descreve as restrições aplicadas a declarações \<xsd:simpleType>.|  
|[Enumeration Facets](../../relational-databases/xml/enumeration-facets.md)|Descreve a limitação relativa a aspectos de enumeração.|  
|[Mixed Type and Simple Content](../../relational-databases/xml/mixed-type-and-simple-content.md)|Descreve a limitação de restringir um tipo misto a um conteúdo simples.|  
|[Coleções de esquemas XML grandes e condições de memória insuficiente](../../relational-databases/xml/large-xml-schema-collections-and-out-of-memory-conditions.md)|Fornece soluções para a condição de memória insuficiente que às vezes acontece com grandes coleções de esquema.|  
|[Modelos de conteúdo não determinístico](../../relational-databases/xml/non-deterministic-content-models.md)|Descreve as limitações relativas a modelos de conteúdo não determinístico.|  
  
## <a name="see-also"></a>Consulte também  
 [Dados XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)   
 [Comparar XML digitado com XML não digitado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Conceder permissões em uma coleção de esquemas XML](../../relational-databases/xml/grant-permissions-on-an-xml-schema-collection.md)   
 [Restrição de atribuição de partícula exclusiva](../../relational-databases/xml/unique-particle-attribution-constraint.md)   
 [Coleções de esquemas XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
