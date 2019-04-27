---
title: Destino do Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSDEST.F1
- SQL11.DTS.DESIGNER.AFPADLSDEST.F1
ms.assetid: d0e86032-2a6b-48b2-898f-e94328474fde
author: yualan
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2f10f78f59a6ec1dd5d5119a89624295935d6ff9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62771892"
---
# <a name="azure-data-lake-store-destination"></a>Destino do Azure Data Lake Store
  O componente **Destino do Azure Data Lake Store** permite que um pacote SSIS grave dados em um Azure Data Lake Store. Os formatos de arquivo compatíveis são: Texto, Avro e ORC. 
  
## <a name="configure-the-azure-data-lake-store-destination"></a>Configure o Destino do Azure Data Lake Store 

1. Arraste e solte **Destino do Azure Data Lake Store** para o designer de fluxo de dados e clique duas vezes nele para ver o editor.  

2.  Para o campo **Gerenciador de conexões do Azure Data Lake Store** , especifique um Gerenciador de conexões do Azure Data Lake Store existente ou crie um novo referindo-se a um serviço do Azure Data Lake Store.  
  
    1.  Para o **caminho do arquivo** especifique o nome do arquivo em que você deseja gravar dados. Se esse arquivo já existir, seu conteúdo será substituído.  
  
    2.  Para o campo **Formato de arquivo** , especifique o formato de arquivo que você deseja usar.  
  
        Se o formato de arquivo for texto, você deverá especificar o valor do **Caractere delimitador de coluna** . Além disso, selecione **Nomes de coluna na primeira linha de dados** se a primeira linha no arquivo contiver nomes de coluna.  

        Se o formato de arquivo for ORC, você precisa instalar o JRE da plataforma correspondente. 
  
3.  Depois de especificar as informações de conexão, alterne para a página **Colunas** para mapear colunas de origem para colunas de destino para o fluxo de dados do SSIS.  
