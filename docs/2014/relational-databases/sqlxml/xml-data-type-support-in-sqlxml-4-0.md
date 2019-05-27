---
title: XML Data Type Support in SQLXML 4.0 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, xml data type support
- xml data type [SQL Server], SQLXML
ms.assetid: 9a6f5ad8-4a8f-4de7-ac17-81d5ccf78459
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0288e88e10433a3c74487b1fd1418b14a58094b
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66012173"
---
# <a name="xml-data-type-support-in-sqlxml-40"></a>Suporte ao tipo de dados xml no SQLXML 4.0
  Começando com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a XML digitado dados usando o `xml` tipo de dados. Este tópico fornece informações sobre como o SQLXML 4.0 reconhece instâncias do tipo de dados `xml` e implementa o suporte para elas.  
  
## <a name="working-with-xml-data-types"></a>Trabalhando com tipos de dados xml  
 Para compreender melhor como trabalhar com tabelas SQL que implementam colunas de tipo de dados `xml`, os seguintes exemplos são fornecidos:  
  
|Tarefa|Exemplo|Tópico|  
|----------|-------------|-----------|  
|Como mapear e incluir uma coluna `xml` em uma exibição XML|"Mapeando um elemento XML para uma coluna de tipo de dados XML"|[Mapeamento padrão dos atributos e elementos XSD para tabelas e colunas &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)|  
|Como inserir dados em uma coluna `xml` com diagramas de atualização|"Inserindo dados em uma coluna de tipo de dados XML"|[Inserindo dados usando diagramas de atualização XML &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)|  
|Carregando em massa dados XML em uma coluna `xml`|"Carregamento em massa em colunas de tipo de dados xml"|[Exemplos de carregamento em massa XML &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)|  
  
## <a name="guidelines-and-limitations"></a>Diretrizes e limitações  
  
-   **\<XSD: qualquer >** não pode ser mapeado para uma coluna, incluindo um `xml` tipo de dados. O suporte no SQLXML para este cenário é fornecido pela anotação `sql:overflow-field`. Outra solução alternativa é mapear um campo de tipo de dados `xml` como um elemento de `xsd:anyType`. Essa solução alternativa é demonstrada no exemplo "Mapeando um elemento XML para uma coluna de tipo de dados XML" mencionado na tabela acima.  
  
-   Não há suporte para a consulta XPath no conteúdo das colunas de tipo de dados `xml`.  
  
-   O uso de uma coluna de tipo de dados `xml` em anotações em que ela não seja aceita (como `sql:relationship` e `sql:key-fields`) ou permitida resultará em erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não serão capturados por componentes de camada intermediária que implementam o SQLXML 4.0. Isto ocorre porque o SQLXML não exige informações do tipo SQL. Isto é semelhante ao comportamento do SQLXML para outros tipos de dados, como o BLOB e tipos binários.  
  
-   O mapeamento de colunas `xml` é aceito apenas para esquemas XSD. Os esquemas XDR não têm suporte para o mapeamento de colunas `xml`.  
  
-   O SQLXML 4.0 conta com o suporte de análise de XML fornecido no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Uma coluna `xml` pode ser mapeada como XML digitado ou não digitado. Em qualquer um desses casos, o SQLXML 4.0 não valida o XML de entrada.  Se o XML de entrada não for válido nem bem formado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o informará para o SQLXML e propagará todas as informações de erro relevantes retornadas pelo servidor para o usuário.  
  
-   O SQLXML 4.0 conta com o suporte limitado para DTDs fornecido no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite um DTD interno nos dados do tipo de dados `xml`, os quais podem ser usados para fornecer valores padrão e para substituir referências de entidades pelo conteúdo expandido correspondente. SQLXML transmite os dados de XML "como estão" (incluindo o DTD interno) para o servidor. É possível converter documentos DTDs em Esquema XML (XSD) usando ferramentas de terceiros e carregar os dados com esquemas XSD embutidos no banco de dados.  
  
-   O SQLXML 4.0 não preserva instruções de processamento de declaração XML (por exemplo), com base no comportamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Em vez disso, a declaração XML é tratada como uma diretiva para o analisador XML do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e seus atributos (version, encoding e standalone) são perdidos depois que os dados são convertidos no tipo de dados `xml`. Os dados XML são armazenados internamente como UCS-2. Todas as outras instruções de processamento na instância de XML são preservadas; elas são permitidas na coluna `xml` e podem ser aceitas por SQLXML.  
  
## <a name="see-also"></a>Consulte também  
 [Dados XML &#40;SQL Server&#41;](../xml/xml-data-sql-server.md)  
  
  
