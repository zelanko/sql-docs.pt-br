---
title: Origem do Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 08/16/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSSRC.F1
- sql14.dts.designer.afpadlssrc.f1
ms.assetid: f9c3311f-7316-48d6-bf10-d810e70b4304
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 7b3bda4e977d5a3f7b6c3029d5151bca8af267ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045431"
---
# <a name="azure-data-lake-store-source"></a>Fonte do Azure Data Lake Store

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  O componente de **Fonte do Azure Data Lake Store** permite que um pacote SSIS leia dados de um Azure Data Lake Store. Os formatos de arquivo compatíveis são: Texto e Avro.
  
 A **Origem do Azure Data Lake Store** é um componente do [SSIS (SQL Server Integration Services) Feature Pack para o Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  
  
> [!NOTE]
> Para garantir que o Gerenciador de conexões do Azure Data Lake Store e os componentes que o utilizam, isto é, a Fonte do Azure Data Lake Store e o Destino do Azure Data Lake Store, possam se conectar aos serviços, verifique se você baixou a versão mais recente do Azure Feature Pack [aqui](https://www.microsoft.com/download/details.aspx?id=49492). 
  
## <a name="configure-the-azure-data-lake-store-source"></a>Configure o Fonte do Azure Data Lake Store
 1. Para ver o editor doFonte do Azure Data Lake Store, arraste e solte **Fonte do Azure Data Lake Store** no designer de fluxo de dados e clique duas vezes nele para abrir o editor.  
  
2.  Para o campo **Gerenciador de conexões do Azure Data Lake Store** , especifique um Gerenciador de conexões do Azure Data Lake Store existente ou crie um novo referindo-se a um serviço do Azure Data Lake Store.  
  
    1.  Para o campo **caminho do arquivo** especifique o caminho do arquivo do arquivo de origem no armazenamento do Azure Data Lake Store.   
  
    2.  Para o campo **formato de arquivo** especifique o formato de arquivo do arquivo de origem.  
  
        Se o formato de arquivo for texto, você deverá especificar o valor do **Caractere delimitador de coluna** . Além disso, selecione **Nomes de coluna na primeira linha de dados** se a primeira linha no arquivo contiver nomes de coluna.  
  
3.  Depois de especificar as informações de conexão, alterne para a página **Colunas** para mapear colunas de origem para colunas de destino para o fluxo de dados do SSIS.   

## <a name="text-qualifier"></a>Qualificador de texto

A **Fonte do Azure Data Lake Store** não dá suporte a um qualificador de texto. Se você tiver que especificar um qualificador de texto para processar os arquivos corretamente, considere a possibilidade de baixar os arquivos em seu computador local e processá-los com a **Fonte de Arquivo Simples**. A Fonte de Arquivo Simples permite especificar um qualificador de texto. Para obter mais informações, confira [Fonte de Arquivo Simples](flat-file-source.md).
