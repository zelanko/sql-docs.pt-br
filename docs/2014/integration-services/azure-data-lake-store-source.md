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
ms.author: janinez
manager: craigg
ms.openlocfilehash: 07ca2a75fa3f7e6329443bb4f71a23f52662f0f8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66061346"
---
# <a name="azure-data-lake-store-source"></a>Fonte do Azure Data Lake Store
  O componente de **Fonte do Azure Data Lake Store** permite que um pacote SSIS leia dados de um Azure Data Lake Store. Os formatos de arquivo com suporte são texto e Avro.
  
## <a name="configure-the-azure-data-lake-store-source"></a>Configure a Fonte do Azure Data Lake Store 
  
1.  Para ver o editor da Fonte do Azure Data Lake Store, arraste e solte **Fonte do Azure Data Lake Store** no designer de fluxo de dados e clique duas vezes nela para abrir o editor.  
  
2.  Para o campo **Gerenciador de conexões do Azure Data Lake Store** , especifique um Gerenciador de conexões do Azure Data Lake Store existente ou crie um novo referindo-se a um serviço do Azure Data Lake Store.  
  
    1.  Para o campo **caminho do arquivo** especifique o caminho do arquivo do arquivo de origem no armazenamento do Azure Data Lake Store.   
  
    2.  Para o campo **formato de arquivo** especifique o formato de arquivo do arquivo de origem.  
  
        Se o formato de arquivo for texto, você deverá especificar o valor do **caractere delimitador de coluna** . Além disso, selecione **nomes de coluna na primeira linha de dados** se a primeira linha no arquivo contiver nomes de coluna.  
  
3.  Depois de especificar as informações de conexão, alterne para a página **Colunas** para mapear colunas de origem para colunas de destino para o fluxo de dados do SSIS.  
