---
title: Suporte ao tipo de dados xml no SQLXML 4.0
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, xml data type support
- xml data type [SQL Server], SQLXML
ms.assetid: 9a6f5ad8-4a8f-4de7-ac17-81d5ccf78459
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4c56efd6c79b7ce7d74af621963f4b12e734d5f9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75252167"
---
# <a name="xml-data-type-support-in-sqlxml-40"></a>Suporte ao tipo de dados xml no SQLXML 4.0
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]partir do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o oferece suporte a dados tipados XML usando o tipo de dados **XML** . Este tópico fornece informações sobre como o SQLXML 4,0 reconhece instâncias do tipo de dados **XML** e implementa o suporte para eles.  
  
## <a name="working-with-xml-data-types"></a>Trabalhando com tipos de dados xml  
 Para entender mais sobre como trabalhar com tabelas SQL que implementam colunas de tipo de dados **XML** , os exemplos a seguir são fornecidos:  
  
|Tarefa|Exemplo|Tópico|  
|----------|-------------|-----------|  
|Como mapear e incluir uma coluna **XML** em uma exibição XML|"Mapeando um elemento XML para uma coluna de tipo de dados XML"|[Mapeamento padrão de elementos e atributos XSD para tabelas e colunas &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)|  
|Como inserir dados em uma coluna **XML** com Updategrams|"Inserindo dados em uma coluna de tipo de dados XML"|[Inserindo dados usando Updategrams XML &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)|  
|Carregamento em massa de dados XML em uma coluna **XML**|"Carregamento em massa em colunas de tipo de dados xml"|[Exemplos de carregamento em massa de XML &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)|  
  
## <a name="guidelines-and-limitations"></a>Diretrizes e limitações  
  
-   xsd: qualquer>não pode ser mapeada para uma coluna, incluindo um tipo de dados **XML** . ** \<** O suporte no SQLXML para esse cenário é fornecido por meio da anotação **SQL: overflow-field** . Outra solução alternativa é mapear um campo de tipo de dados **XML** como um elemento de **xsd: anyType**. Essa solução alternativa é demonstrada no exemplo "Mapeando um elemento XML para uma coluna de tipo de dados XML" mencionado na tabela acima.  
  
-   Não há suporte para a consulta XPath no conteúdo das colunas de tipo de dados **XML** .  
  
-   O uso de uma coluna de tipo de dados **XML** em anotações em que não há suporte (como **SQL: relationship** e **SQL: key-fields**) ou allowed [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resultará em erros que não serão interceptados por componentes da camada intermediária que implementam o SQLXML 4,0. Isto ocorre porque o SQLXML não exige informações do tipo SQL. Isto é semelhante ao comportamento do SQLXML para outros tipos de dados, como o BLOB e tipos binários.  
  
-   O mapeamento de colunas **XML** tem suporte apenas para esquemas XSD. Os esquemas XDR não dão suporte ao mapeamento de colunas **XML** .  
  
-   O SQLXML 4.0 conta com o suporte de análise de XML fornecido no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Uma coluna **XML** pode ser MAPEADA como XML digitado ou XML não tipado. Em qualquer um desses casos, o SQLXML 4.0 não valida o XML de entrada.  Se o XML de entrada não for válido nem bem formado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o informará para o SQLXML e propagará todas as informações de erro relevantes retornadas pelo servidor para o usuário.  
  
-   O SQLXML 4.0 conta com o suporte limitado para DTDs fornecido no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]permite um DTD interno em dados de tipo de dados **XML** , que podem ser usados para fornecer valores padrão e para substituir referências de entidade com seu conteúdo expandido. SQLXML transmite os dados de XML "como estão" (incluindo o DTD interno) para o servidor. É possível converter documentos DTDs em Esquema XML (XSD) usando ferramentas de terceiros e carregar os dados com esquemas XSD embutidos no banco de dados.  
  
-   O SQLXML 4,0 não preserva as instruções de processamento de declaração XML (por exemplo,) com base [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]no comportamento de. Em vez disso, a declaração XML é tratada como uma diretiva [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o analisador XML, e seus atributos (versão, codificação e autônomo) são perdidos depois que os dados são convertidos no tipo de dados **XML** . Os dados XML são armazenados internamente como UCS-2. Todas as outras instruções de processamento na instância XML são preservadas; Elas são permitidas na coluna **XML** e podem ser suportadas pelo SQLXML.  
  
## <a name="see-also"></a>Consulte Também  
 [Dados XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
