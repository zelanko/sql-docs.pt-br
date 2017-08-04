---
title: "Transformação pesquisa de termos | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.termlookuptrans.f1
helpviewer_keywords:
- extracting data [Integration Services]
- match extracted terms [Integration Services]
- text extraction [Integration Services]
- term extractions [Integration Services]
- lookups [Integration Services]
- counting extracted items
- Term Lookup transformation
ms.assetid: 3c0fa2f8-cb6a-4371-b184-7447be001de1
caps.latest.revision: 56
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3eefbab1c6f9b3cd5e51faa9e875a44218c33b3f
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="term-lookup-transformation"></a>transformação Pesquisa de Termos
  A transformação Pesquisa de Termo corresponde termos extraídos de texto em uma coluna de entrada de transformação com termos em uma tabela de referência. Ela conta o número de vezes em que um termo na tabela de pesquisa ocorre no conjunto de dados de entrada e grava a contagem junto com o termo da tabela de referência nas colunas na saída de transformação. Essa transformação é útil para criar uma lista de palavras personalizada com base no texto de entrada, completa com estatísticas de frequência de palavras.  
  
 Antes de a transformação pesquisa de termos executar uma pesquisa, ela extrai palavras do texto em uma coluna de entrada usando o mesmo método da transformação extração de termos:  
  
-   O texto é dividido em sentenças.  
  
-   As sentenças são divididas em palavras.  
  
-   As palavras são normalizadas.  
  
 Para personalizar ainda mais quais os termos a corresponder, a transformação pesquisa de termos pode ser configurada para executar uma correspondência com diferenciação de maiúsculas e minúsculas.  
  
## <a name="matches"></a>Correspondências  
 A pesquisa de termos executa uma pesquisa e retorna um valor usando as regras a seguir:  
  
-   Se a transformação estiver configurada para executar correspondências com diferenciação de maiúsculas e minúsculas, as correspondências que apresentarem falha na comparação com diferenciação de maiúsculas e minúsculas serão descartadas. Por exemplo, *estudante* e *ESTUDANTE* serão tratadas como palavras diferentes.  
  
    > [!NOTE]  
    >  Uma palavra sem inicial em maiúscula pode corresponder a uma palavra que tenha a inicial em maiúscula por estar no início de uma sentença. Por exemplo, a correspondência entre *estudante* e *Estudante* obterá êxito quando *Estudante* for a primeira palavra em um sentença.  
  
-   Se uma forma plural do substantivo ou locução nominal existir na tabela de referência, a pesquisa corresponderá apenas à forma plural do substantivo ou locução nominal. Por exemplo, todas as ocorrências de *estudantes* seriam contadas separadamente das ocorrências de *estudante*.  
  
-   Se apenas a forma singular da palavra for achada na tabela de referência, tanto a forma singular quanto a plural da palavra ou locução corresponderão à forma singular. Por exemplo, se a tabela de pesquisa contiver *estudante*e a transformação achar as palavras *estudante* e *estudantes*, ambas as palavras seriam contadas como correspondentes ao termo de pesquisa *estudante*.  
  
-   Se o texto na coluna de entrada for uma locução nominal lematizada, só a última palavra na locução nominal será afetada pela normalização. Por exemplo, a versão lematizada de *consultas de médicos* é *consulta de médicos*.  
  
 Quando um item de pesquisa contém termos que se sobrepõem no conjunto de referência, isto é, um subtermo é achado em mais de um registro de referência, a transformação pesquisa de termos só retorna um resultado de pesquisa. O exemplo a seguir mostra o resultado quando um item de pesquisa contém um subtermo sobreposto. O subtermo sobreposto nesse caso é *Windows*, que é achado dentro de dois termos de referência. Porém, a transformação não retorna dois resultados, mas apenas um único termo de referência: *Windows*. O segundo termo de referência, *Windows 7 Professional*não é retornado.  
  
|Item|Value|  
|----------|-----------|  
|Termo de entrada|Windows 7 Professional|  
|Termos de referência|Windows, Windows 7 Professional|  
|Saída|Windows|  
  
 A transformação pesquisa de termos pode corresponder substantivos e locuções nominais que contenham caracteres especiais e os dados na tabela de referência podem incluir esses caracteres. Os caracteres especiais são da seguinte maneira: %, @, &, $, #, \*,:,,., **,** ,!,?, \<, >, +, =, ^, ~, |, \\, /, (,), [,], {,}, ", e '.  
  
## <a name="data-types"></a>Tipos de dados  
 A transformação pesquisa de termos só pode usar uma coluna que tenha tipo de dados DT_WSTR ou DT_NTEXT. Se uma coluna contiver texto, mas não tiver um desses tipos de dados, a transformação Conversão de Dados poderá adicionar uma coluna com tipo de dados DT_WSTR ou DT_NTEXT para o fluxo de dados e copiar os valores da coluna para a coluna nova. A saída da transformação Conversão de Dados pode ser usada, então, como entrada para a transformação pesquisa de termos. Para obter mais informações, consulte [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md).  
  
## <a name="configuration-the-term-lookup-transformation"></a>Configuração da transformação Pesquisa de Termo  
 As colunas de entrada da transformação Pesquisa de Termo incluem a propriedade InputColumnType, que indica o uso da coluna. InputColumnType pode conter os valores a seguir:  
  
-   O valor 0 indica que a coluna só é transmitida para a saída e não é usada na pesquisa.  
  
-   O valor 1 indica que a coluna só é usada na pesquisa.  
  
-   O valor 2 indica que a coluna é transmitida para a saída e também é usada na pesquisa.  
  
 As colunas de saída da transformação cuja propriedade InputColumnType é definida como 0 ou 2 incluem a propriedade CustomLineageID para uma coluna, que contém o identificador de linhagem atribuído à coluna por um componente de fluxo de dados upstream.  
  
 A transformação Pesquisa de Termos adiciona duas colunas à saída da transformação; por padrão elas são nomeadas como **Term** e **Frequency**. A coluna**Term** contém um termo da tabela de pesquisa e a **Frequency** contém o número de vezes que o termo na tabela de referência ocorre no conjunto de dados de entrada. Essas colunas não incluem a propriedade CustomLineageID.  
  
 A tabela de pesquisa deve ser uma tabela em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou do Access. Se a saída da transformação extração de termos for salva em uma tabela, esta tabela poderá ser usada como tabela de referência, mas outras tabelas também poderão ser usadas. Texto em arquivos simples, pastas de trabalho do Excel ou outras fontes precisam ser importadas em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou em um banco de dados do Access antes de você poder usar a transformação pesquisa de termos.  
  
 A transformação pesquisa de termos usa uma conexão OLE DB separada para conectar-se à tabela de referência. Para obter mais informações, consulte [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 A transformação pesquisa de termos funciona em um modo totalmente pré-armazenado em cache. No tempo de execução, a transformação pesquisa de termos lê os termos da tabela de referência e os armazena em sua memória privada antes de processar qualquer linha de entrada de transformação.  
  
 Como os termos em uma linha de coluna de entrada podem se repetir, a saída da transformação pesquisa de termos geralmente tem mais linhas que a entrada da transformação.  
  
 A transformação tem uma entrada e uma saída. Ela não oferece suporte a saídas de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação Pesquisa de Termos** , clique em um dos seguintes tópicos:  
  
-   [Editor de Transformação Pesquisa de Termos &#40;Guia Tabela de Referência&#41;](../../../integration-services/data-flow/transformations/term-lookup-transformation-editor-reference-table-tab.md)  
  
-   [Editor de Transformação Pesquisa de Termos &#40;Guia Pesquisa de Termos&#41;](../../../integration-services/data-flow/transformations/term-lookup-transformation-editor-term-lookup-tab.md)  
  
-   [Editor de Transformação Pesquisa de Termos &#40;Guia Avançado&#41;](../../../integration-services/data-flow/transformations/term-lookup-transformation-editor-advanced-tab.md)  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
  
