---
title: Origem do arquivo bruto | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.rawfilesource.f1
- sql13.dts.designer.rawfilesourceconnectionmanager.f1
- sql13.dts.designer.rawfilesourcecolumns.f1
helpviewer_keywords:
- sources [Integration Services], Raw File
- raw data [Integration Services]
- Raw File source
ms.assetid: 5b4daea5-7f76-4674-aa77-0a79f9f97f7d
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bed2d974f66be781c9fc11ea93c06be8ccf5fc5f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="raw-file-source"></a>Origem do arquivo bruto
  A fonte Arquivo Bruto lê dados brutos de um arquivo. Como a representação dos dados é nativa à fonte, os dados não necessitam de conversão e praticamente nenhuma análise. Isso significa que a fonte de arquivo bruto pode ler dados mais rapidamente do que outras fontes, como o arquivo simples e as fontes OLE DB.  
  
 A fonte de arquivo bruto é usada para recuperar dados brutos que foram escritos previamente pelo destino de arquivo bruto. Você também pode apontar a origem Arquivo Bruto para um arquivo bruto vazio que contenha somente as colunas (arquivo somente de metadados). Use o destino Arquivo Bruto para gerar o arquivo de somente metadados sem precisar executar o pacote. Para obter mais informações, consulte [Raw File Destination](../../integration-services/data-flow/raw-file-destination.md).  
  
 O formato de arquivo bruto contém informações de classificação. O destino Arquivo Bruto salva todas as informações de classificação incluindo os sinalizadores de comparação para as colunas de cadeia de caracteres. A fonte Arquivo Bruto lê e segue as informações de classificação. Você tem a opção de configurar fonte Arquivo Bruto para ignorar os sinalizadores de classificação no arquivo, usando o Editor Avançado. Para obter mais informações sobre os sinalizadores de comparação, consulte [Comparando dados de cadeia de caracteres](../../integration-services/data-flow/comparing-string-data.md).  
  
 Você configura o arquivo bruto especificando o nome do arquivo que a fonte de arquivo bruto lê.  
  
> [!NOTE]  
>  Essa fonte não utiliza um gerenciador de conexões.  
  
 Essa fonte tem uma saída. Não dá suporte a uma saída de erro.  
  
## <a name="configuration-of-the-raw-file-source"></a>Configuração da Fonte Arquivo Bruto  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas de arquivo bruto](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter informações sobre como definir as propriedades do componente, consulte [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Entrada de blog, [Raw Files Are Awesome](http://www.sqlservercentral.com/blogs/stratesql/archive/2011/1/1/31-days-of-ssis-_1320_-raw-files-are-awesome-_2800_1_2F00_31_2900_.aspx), em sqlservercentral.com  
  
## <a name="raw-file-source-editor-connection-manager-page"></a>Editor de Fonte Arquivo Bruto (página Gerenciador de Conexões)
  A fonte Arquivo Bruto lê dados brutos de um arquivo. Como a representação dos dados é nativa à fonte, os dados não necessitam de conversão e praticamente nenhuma análise.   
## <a name="raw-file-source-editor-columns-page"></a>Editor de fonte Arquivo Bruto (página Colunas)
  A fonte Arquivo Bruto lê dados brutos de um arquivo. Como a representação dos dados é nativa à fonte, os dados não necessitam de conversão e praticamente nenhuma análise.   
## <a name="see-also"></a>Consulte Também  
 [Raw File Destination](../../integration-services/data-flow/raw-file-destination.md)   
 [Fluxo de Dados](../../integration-services/data-flow/data-flow.md)  
  
  
