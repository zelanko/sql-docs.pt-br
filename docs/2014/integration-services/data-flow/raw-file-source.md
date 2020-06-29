---
title: Origem do arquivo bruto | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rawfilesource.f1
helpviewer_keywords:
- sources [Integration Services], Raw File
- raw data [Integration Services]
- Raw File source
ms.assetid: 5b4daea5-7f76-4674-aa77-0a79f9f97f7d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 53b9b4a38e82fe37f0f1f114969f2f71fb4848a8
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85431533"
---
# <a name="raw-file-source"></a>Origem do arquivo bruto
  A fonte Arquivo Bruto lê dados brutos de um arquivo. Como a representação dos dados é nativa à fonte, os dados não necessitam de conversão e praticamente nenhuma análise. Isso significa que a fonte de arquivo bruto pode ler dados mais rapidamente do que outras fontes, como o arquivo simples e as fontes OLE DB.  
  
 A fonte de arquivo bruto é usada para recuperar dados brutos que foram escritos previamente pelo destino de arquivo bruto. Você também pode apontar a origem Arquivo Bruto para um arquivo bruto vazio que contenha somente as colunas (arquivo somente de metadados). Use o destino Arquivo Bruto para gerar o arquivo de somente metadados sem precisar executar o pacote. Para obter mais informações, consulte [Raw File Destination](raw-file-destination.md).  
  
 O formato de arquivo bruto contém informações de classificação. O destino Arquivo Bruto salva todas as informações de classificação incluindo os sinalizadores de comparação para as colunas de cadeia de caracteres. A fonte Arquivo Bruto lê e segue as informações de classificação. Você tem a opção de configurar fonte Arquivo Bruto para ignorar os sinalizadores de classificação no arquivo, usando o Editor Avançado. Para obter mais informações sobre os sinalizadores de comparação, consulte [Comparando dados de cadeia de caracteres](comparing-string-data.md).  
  
 Você configura o arquivo bruto especificando o nome do arquivo que a fonte de arquivo bruto lê.  
  
> [!NOTE]  
>  Essa fonte não utiliza um gerenciador de conexões.  
  
 Essa fonte tem uma saída. Não dá suporte a uma saída de erro.  
  
## <a name="configuration-of-the-raw-file-source"></a>Configuração da Fonte Arquivo Bruto  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../common-properties.md)  
  
-   [Propriedades personalizadas de arquivo bruto](raw-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter informações sobre como definir as propriedades do componente, consulte [Definir as propriedades de um componente de fluxo de dados](set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Entrada de blog, [Raw Files Are Awesome](https://www.sqlservercentral.com/blogs/31-days-of-ssis-%e2%80%93-raw-files-are-awesome-131), em sqlservercentral.com  
  
## <a name="see-also"></a>Consulte Também  
 [Destino do arquivo bruto](raw-file-destination.md)   
 [Fluxo de Dados](data-flow.md)  
  
  
