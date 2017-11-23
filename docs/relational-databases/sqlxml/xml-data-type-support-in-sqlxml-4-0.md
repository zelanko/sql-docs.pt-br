---
title: XML Data Type Support in SQLXML 4.0 | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQLXML, xml data type support
- xml data type [SQL Server], SQLXML
ms.assetid: 9a6f5ad8-4a8f-4de7-ac17-81d5ccf78459
caps.latest.revision: "17"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 581472d13c4bb9e11d52a8a71965f9b8f64bf0c4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="xml-data-type-support-in-sqlxml-40"></a>Suporte ao tipo de dados xml no SQLXML 4.0
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Começando com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a XML digitado dados usando o **xml** tipo de dados. Este tópico fornece informações sobre como o SQLXML 4.0 reconhece instâncias do **xml** tipo de dados e implementa o suporte para eles.  
  
## <a name="working-with-xml-data-types"></a>Trabalhando com tipos de dados xml  
 Para saber mais sobre como trabalhar com tabelas SQL que implementam **xml** colunas de tipo de dados são fornecidos os exemplos a seguir:  
  
|Tarefa|Exemplo|Tópico|  
|----------|-------------|-----------|  
|Como mapear e incluir um **xml** coluna em uma exibição XML|"Mapeando um elemento XML para uma coluna de tipo de dados XML"|[Mapeamento padrão de atributos e elementos XSD para tabelas e colunas &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)|  
|Como inserir dados em um **xml** coluna com diagramas de atualização|"Inserindo dados em uma coluna de tipo de dados XML"|[Inserindo dados usando diagramas de atualização XML &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)|  
|Carregar dados XML em massa um **xml** coluna|"Carregamento em massa em colunas de tipo de dados xml"|[Exemplos de carregamento em massa XML &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)|  
  
## <a name="guidelines-and-limitations"></a>Diretrizes e limitações  
  
-   **\<XSD: qualquer >** não pode ser mapeado para uma coluna, incluindo um **xml** tipo de dados. Suporte no SQLXML para este cenário é fornecido por meio de **SQL: overflow-campo** anotação. Outra solução alternativa é mapear um **xml** campo de tipo de dados como um elemento de **anyType**. Essa solução alternativa é demonstrada no exemplo "Mapeando um elemento XML para uma coluna de tipo de dados XML" mencionado na tabela acima.  
  
-   A consulta XPath no conteúdo das **xml** não há suporte para colunas do tipo de dados.  
  
-   Usando um **xml** coluna de tipo de dados em anotações em que não há suporte (como **SQL: Relationship** e **SQL: Key-campos**) ou permitida resultará em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erros que não serão capturados por componentes de camada intermediária que implementam o SQLXML 4.0. Isto ocorre porque o SQLXML não exige informações do tipo SQL. Isto é semelhante ao comportamento do SQLXML para outros tipos de dados, como o BLOB e tipos binários.  
  
-   Mapeamento de **xml** colunas só tem suporte para esquemas XSD. Esquemas XDR não oferecem suporte a mapeamento **xml** colunas.  
  
-   O SQLXML 4.0 conta com o suporte de análise de XML fornecido no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um **xml** coluna pode ser mapeada como XML tipado ou de XML não digitado. Em qualquer um desses casos, o SQLXML 4.0 não valida o XML de entrada.  Se o XML de entrada não for válido nem bem formado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o informará para o SQLXML e propagará todas as informações de erro relevantes retornadas pelo servidor para o usuário.  
  
-   O SQLXML 4.0 conta com o suporte limitado para DTDs fornecido no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]permite um DTD interno nos **xml** tipo de dados, que pode ser usado para fornecer valores padrão e para substituir referências a entidades pelo conteúdo expandido correspondente. SQLXML transmite os dados de XML "como estão" (incluindo o DTD interno) para o servidor. É possível converter documentos DTDs em Esquema XML (XSD) usando ferramentas de terceiros e carregar os dados com esquemas XSD embutidos no banco de dados.  
  
-   O SQLXML 4.0 não preserva instruções de processamento de declaração XML (por exemplo), com base no comportamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Em vez disso, a declaração XML é tratada como uma diretiva para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] analisador XML e seus atributos (versão, a codificação e autônoma) são perdidos após a conversão de dados para o **xml** tipo de dados. Os dados XML são armazenados internamente como UCS-2. Todas as outras instruções de processamento na instância XML são preservadas; elas são permitidas no **xml** coluna e podem ser aceitas por SQLXML.  
  
## <a name="see-also"></a>Consulte também  
 [Dados XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
