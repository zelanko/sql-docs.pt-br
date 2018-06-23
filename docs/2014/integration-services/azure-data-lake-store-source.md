---
title: Origem do Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSSRC.F1
- SQL11.DTS.DESIGNER.AFPADLSSRC.F1
ms.assetid: 7d9e8457-62aa-4aea-98ee-7d1121dfae4f
caps.latest.revision: 6
author: yualan
ms.author: yual
manager: jhubbard
ms.openlocfilehash: e7bd327dc2657123daf94390785bda11a17e2040
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007980"
---
# <a name="azure-data-lake-store-source"></a>Fonte do Azure Data Lake Store
  O componente de **Fonte do Azure Data Lake Store** permite que um pacote SSIS leia dados de um Azure Data Lake Store. Os formatos de arquivo com suporte são texto e Avro.
  
## <a name="configure-the-azure-data-lake-store-source"></a>Configure o Fonte do Azure Data Lake Store 
  
1.  Para ver o editor doFonte do Azure Data Lake Store, arraste e solte **Fonte do Azure Data Lake Store** no designer de fluxo de dados e clique duas vezes nele para abrir o editor.  
  
2.  Para o campo **Gerenciador de conexões do Azure Data Lake Store** , especifique um Gerenciador de conexões do Azure Data Lake Store existente ou crie um novo referindo-se a um serviço do Azure Data Lake Store.  
  
    1.  Para o campo **caminho do arquivo** especifique o caminho do arquivo do arquivo de origem no armazenamento do Azure Data Lake Store.   
  
    2.  Para o campo **formato de arquivo** especifique o formato de arquivo do arquivo de origem.  
  
        Se o formato de arquivo for texto, você deverá especificar o valor do **Caractere delimitador de coluna** . Além disso, selecione **Nomes de coluna na primeira linha de dados** se a primeira linha no arquivo contiver nomes de coluna.  
  
3.  Depois de especificar as informações de conexão, alterne para a página **Colunas** para mapear colunas de origem para colunas de destino para o fluxo de dados do SSIS.  