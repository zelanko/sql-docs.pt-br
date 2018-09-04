---
title: Origem de Blobs do Azure | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpblobsrc.f1
- sql14.dts.designer.afpblobsrc.f1
ms.assetid: 80645c5c-88c8-4fb0-8607-de1bb7bffcbb
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5404b7bc7e7543f85890816973fdbd0c1e39022f
ms.sourcegitcommit: 61212c06b56953ce2e2627d35f7bd69cda786540
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2018
ms.locfileid: "40410956"
---
# <a name="azure-blob-source"></a>Fonte de Blobs do Azure
  O componente de **Fonte de Blobs do Azure** permite que um pacote SSIS leia dados de um blob do Azure. Os formatos de arquivo com suporte são: CSV e AVRO.
  
  Para ver o editor da Fonte de Blobs do Azure, arraste e solte **Fonte de Blobs do Azure** no designer de fluxo de dados e clique duas vezes nele para abrir o editor.  
  
 A **Origem de Blobs do Azure** é um componente do [SSIS (SQL Server Integration Services) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  
  
1.  Para o campo **Gerenciador de conexões do armazenamento do Azure** , especifique um Gerenciador de Conexões do Armazenamento do Azure existente ou crie um novo referindo-se a uma Conta de Armazenamento do Azure.  
  
2.  Para o campo **Nome do contêiner de blobs** , especifique o nome do contêiner de blobs que contém os arquivos de origem.  
  
3.  Para o campo **Nome do Blob** , especifique o caminho para o blob.  
  
4.  Para o campo **Formato de arquivo de blob**, selecione o formato de blob que você deseja usar, **Texto** ou **Avro**.  
  
5.  Se o formato de arquivo for **Texto**, você deverá especificar o valor do **Caractere delimitador de coluna**. (O uso de múltiplos caracteres delimitadores não é compatível.)

    Além disso, selecione **Nomes de coluna na primeira linha de dados** se a primeira linha no arquivo contiver nomes de coluna.

6.  Se o arquivo estiver compactado, selecione **Descompactar o arquivo**.

7.  Se o arquivo estiver compactado, selecione o **Tipo de compactação**: **GZIP**, **DEFLATE** ou **BZIP2**. Observe que não há suporte para o formato Zip.
  
8.  Depois de especificar as informações de conexão, alterne para a página **Colunas** para mapear colunas de origem para colunas de destino para o fluxo de dados do SSIS.  
  
  
