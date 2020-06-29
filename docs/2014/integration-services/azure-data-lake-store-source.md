---
title: Origem do Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSSRC.F1
- SQL11.DTS.DESIGNER.AFPADLSSRC.F1
ms.assetid: 7d9e8457-62aa-4aea-98ee-7d1121dfae4f
author: yualan
ms.author: chugu
ms.openlocfilehash: e5bce25e303b055d734da6a00c73851f4eb0d7ec
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439383"
---
# <a name="azure-data-lake-store-source"></a>Fonte do Azure Data Lake Store
  O componente de **Fonte do Azure Data Lake Store** permite que um pacote SSIS leia dados de um Azure Data Lake Store. Os formatos de arquivo com suporte são texto e Avro.
  
## <a name="configure-the-azure-data-lake-store-source"></a>Configure a Fonte do Azure Data Lake Store 
  
1.  Para ver o editor da Fonte do Azure Data Lake Store, arraste e solte **Fonte do Azure Data Lake Store** no designer de fluxo de dados e clique duas vezes nela para abrir o editor.  
  
2.  Para o campo **Gerenciador de conexões do Azure Data Lake Store** , especifique um Gerenciador de conexões do Azure Data Lake Store existente ou crie um novo referindo-se a um serviço do Azure Data Lake Store.  
  
    1.  Para o campo **caminho do arquivo** especifique o caminho do arquivo do arquivo de origem no armazenamento do Azure Data Lake Store.   
  
    2.  Para o campo **formato de arquivo** especifique o formato de arquivo do arquivo de origem.  
  
        Se o formato de arquivo for texto, você deverá especificar o valor do **Caractere delimitador de coluna** . Além disso, selecione **Nomes de coluna na primeira linha de dados** se a primeira linha no arquivo contiver nomes de coluna.  
  
3.  Depois de especificar as informações de conexão, alterne para a página **Colunas** para mapear colunas de origem para colunas de destino para o fluxo de dados do SSIS.  
