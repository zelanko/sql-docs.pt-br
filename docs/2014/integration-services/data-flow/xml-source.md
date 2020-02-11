---
title: Origem XML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmlsource.f1
helpviewer_keywords:
- sources [Integration Services], XML
- XML source [Integration Services]
- XML Source Editor
ms.assetid: 68c27ea5-e93d-4e26-bfb2-d967ca0a5282
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 28e7a7395c02e44e52469992f3738f0d873e227f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62899939"
---
# <a name="xml-source"></a>Origem XML
  A origem XML lê um arquivo de dados XML e preenche as colunas na saída de origem com os dados.  
  
 Os dados de arquivos XML frequentemente incluem relações hierárquicas. Por exemplo, um arquivo de dados XML pode representar catálogos e itens em catálogos. Antes de os dados serem inseridos no fluxo de dados, é necessário determinar a relação dos elementos no arquivo de dados XML e gerar uma saída para cada elemento do arquivo.  
  
## <a name="schemas"></a>Esquemas  
 A origem XML usa um esquema para interpretar os dados XML. A origem XML dá suporte ao uso de um arquivo XSD (XML Schema Definition) ou de esquemas embutidos para conversão dos dados XML em um formato tabular. Se a origem XML for configurada com a caixa de diálogo **Editor de Origem XML** , a interface de usuário poderá gerar um XSD a partir do arquivo de dados XML especificado.  
  
> [!NOTE]  
>  DTDs não são suportados.  
  
 Os esquemas só podem dar suporte a um único namespace; eles não dão suporte a coleções de esquema.  
  
> [!NOTE]  
>  A origem XML não valida os dados no arquivo de XML em relação ao XSD.  
  
## <a name="xml-source-editor"></a>Editor de Origem XML  
 Os dados dos arquivos XML frequentemente incluem relações hierárquicas. A caixa de diálogo **Editor de Origem XML** usa o esquema especificado para gerar as saídas de origem XML. É possível especificar um arquivo XSD, usar um esquema embutido ou gerar um XSD a partir do arquivo de dados XML especificado. O esquema deve estar disponível em tempo de design.  
  
 A origem XML gera estruturas tabulares a partir dos dados XML criando uma saída para cada elemento que contém outros elementos dos arquivos XML. Por exemplo, se os dados XML representarem catálogos e itens em catálogos, a origem XML criará uma saída para os catálogos e uma saída para cada tipo de item contido nos catálogos. A saída de cada item conterá colunas de saída para os atributos do item em questão.  
  
 Para fornecer informações sobre a relação hierárquica dos dados nas saídas, a origem XML adiciona uma coluna às saídas que identifica o elemento pai de cada elemento filho. Usando o exemplo de catálogos com tipos de itens diferentes, cada item teria um valor de coluna para identificar o catálogo ao qual pertence.  
  
 A origem XML cria uma saída para cada elemento, mas não é necessário usar todas as saídas. Você pode excluir todas as saídas que não deseja usar ou apenas não se conectar a um componente downstream.  
  
 A origem XML também gera os nomes de saída para assegurar que os nomes são sejam ambíguos. Esses nomes podem ser longos e talvez não identifiquem as saídas de uma maneira útil. Você pode renomear as saídas, contanto que seus nomes permaneçam exclusivos. Você também pode modificar o tipo de dados e o comprimento de colunas de saída.  
  
 A cada saída, a origem XML adiciona uma saída de erro. Por padrão, as colunas das saídas de erro têm um tipo de dados de cadeia de caracteres Unicode (DT_WSTR) com 255 caracteres, mas é possível configurar as colunas das saídas de erro modificando o tipo e o comprimento dos dados.  
  
 Se o arquivo de dados XML tiver elementos que não estão no XSD, esses elementos serão ignorados e nenhuma saída será gerada para eles. Por outro lado, se o arquivo de dados XML tiver elementos ausentes que estão representados no XSD, a saída vai conter colunas com valores nulos.  
  
 Quando os dados são extraídos do arquivo de dados XML, eles são convertidos em um tipo de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . No entanto, a origem XML não pode converter os dados XML para os tipos de dados DT_TIME2 ou DT_DBTIMESTAMP2 porque ela não tem suporte a esses tipos de dados. Para obter mais informações, consulte [Integration Services tipos de dados](integration-services-data-types.md).  
  
 O XSD ou o esquema embutido pode especificar o tipo de dados para os elementos, mas, se não fizerem isso, a caixa de diálogo **Editor de Origem XML** atribuirá o tipo de dados String Unicode (DT_WSTR) à coluna na saída que contém o elemento e definirá o comprimento da coluna como 255 caracteres.  
  
 Se o esquema especificar o comprimento máximo de um elemento, o comprimento da coluna de saída será definido para esse valor. Se o comprimento máximo for maior do que o comprimento suportado pelo tipo de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no qual o elemento foi convertido, os dados serão truncados no comprimento máximo do tipo de dados. Por exemplo, se o comprimento de uma cadeia de caracteres for 5000, ela será truncada em 4000 caracteres porque o comprimento máximo do tipo de dados DT_WSTR é 4000 caracteres; do mesmo modo, os dados de byte são truncados em 8000 caracteres, que é o comprimento máximo do tipo de dados DT_BYTES. Se o esquema não especificar nenhum comprimento máximo, o comprimento padrão das colunas com qualquer tipo de dados será definido como 255. O truncamento dos dados na origem XML é tratada do mesmo modo que seria em outros componentes de fluxo de dados. Para obter mais informações, consulte [Tratamento de erros em dados](error-handling-in-data.md).  
  
 Você pode modificar o tipo de dados e o comprimento da coluna. Para obter mais informações, consulte [Integration Services tipos de dados](integration-services-data-types.md).  
  
## <a name="configuration-of-the-xml-source"></a>Configuração da origem XML  
 A origem XML dá suporte a três modos diferentes de acesso aos dados. Você pode especificar o local do arquivo de dados XML, a variável que contém o local do arquivo ou a variável que contém os dados XML.  
  
 A origem XML inclui as propriedades personalizadas `XMLData` e `XMLSchemaDefinition` que podem ser atualizadas por expressões de propriedade quando o pacote é carregado. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md), [Usar expressões de propriedade em pacotes](../expressions/use-property-expressions-in-packages.md) e [Propriedades personalizadas de origem XML](xml-source-custom-properties.md).  
  
 A origem XML dá suporte a várias saídas regulares e saídas de erro.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui a caixa de diálogo **XML Source edito**r para configurar a origem XML. Esta caixa de diálogo está disponível no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Origem XML** , clique em um dos seguintes tópicos:  
  
-   [Editor de origem XML &#40;página do Gerenciador de conexões&#41;](../xml-source-editor-connection-manager-page.md)  
  
-   [Editor de origem XML &#40;página colunas&#41;](../xml-source-editor-columns-page.md)  
  
-   [Editor de origem XML &#40;página saída de erro&#41;](../xml-source-editor-error-output-page.md)  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../common-properties.md)  
  
-   [Propriedades personalizadas da origem XML](xml-source-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, clique em um dos tópicos a seguir:  
  
-   [Definir as propriedades de um componente de fluxo de dados](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [Extrair dados por meio da origem XML](xml-source.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Artigo técnico, [usando um arquivo XML para configurar um pacote do SSIS](https://www.sqlshack.com/using-xml-file-configure-ssis-package/).  
  
  
