---
title: Destino de Blob do Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpblobdest.f1
- sql11.dts.designer.afpblobdest.f1
ms.assetid: 820a1e7a-7182-4c7b-ab56-5b4097a7e042
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6f114f39d76a5ec764e9bab814123a668a522dbe
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756858"
---
# <a name="azure-blob-destination"></a>Destino de Blob do Azure
  O componente **Destino de Blob do Azure** permite que um pacote SSIS grave dados de um blob do Azure. Os formatos de arquivo com suporte são: CSV e AVRO. Arraste e solte **destino de Blob do Azure** ao designer de fluxo de dados e clique duas vezes nele para ver o editor).  
  
1.  Para o campo **Gerenciador de conexões do armazenamento do Azure** , especifique um Gerenciador de Conexões do Armazenamento do Azure existente ou crie um novo referindo-se a uma Conta de Armazenamento do Azure.  
  
2.  Para o campo **Nome do contêiner de blobs** , especifique o nome do contêiner de blobs que contém os arquivos de origem.  
  
3.  Para o campo **Nome do Blob** , especifique o caminho para o blob.  
  
4.  Para o campo **Formato de arquivo de blob** , especifique o formato de blob que você deseja usar.  
  
5.  Se o formato de arquivo for CSV, você deverá especificar o valor do **Caractere delimitador de coluna** . Além disso, escolha **Nomes de coluna na primeira linha de dados** se a primeira linha no arquivo contiver nomes de coluna.  
  
6.  Depois de especificar as informações de conexão, alterne para a página **Colunas** para mapear colunas de origem para colunas de destino para o fluxo de dados do SSIS.  
  
  
