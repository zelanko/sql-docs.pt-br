---
title: Destino de Blob do Azure | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpblobdest.f1
- sql14.dts.designer.afpblobdest.f1
ms.assetid: 820a1e7a-7182-4c7b-ab56-5b4097a7e042
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 3194e2dbb6563b5260fcc390e84e73a17e09542c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045463"
---
# <a name="azure-blob-destination"></a>Destino de Blob do Azure

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


 O componente **Destino de Blob do Azure** permite que um pacote SSIS grave dados de um blob do Azure. Os formatos de arquivo compatíveis são: CSV e AVRO. 
   
 Arraste e solte **Destino de Blob do Azure** para o designer de fluxo de dados e clique duas vezes nele para ver o editor).  
  
 O **Destino de Blob de Azure** é um componente do [Feature Pack do SSIS (SQL Server Integration Services) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  
  
1.  Para o campo **Gerenciador de conexões do armazenamento do Azure** , especifique um Gerenciador de Conexões do Armazenamento do Azure existente ou crie um novo referindo-se a uma Conta de Armazenamento do Azure.  
  
2.  Para o campo **Nome do contêiner de blobs** , especifique o nome do contêiner de blobs que contém os arquivos de origem.  
  
3.  Para o campo **Nome do Blob** , especifique o caminho para o blob.  
  
4.  Para o campo **Formato de arquivo de blob** , especifique o formato de blob que você deseja usar.  
  
5.  Se o formato de arquivo for CSV, você deverá especificar o valor do **Caractere delimitador de coluna** . Além disso, escolha **Nomes de coluna na primeira linha de dados** se a primeira linha no arquivo contiver nomes de coluna.  
  
6.  Depois de especificar as informações de conexão, alterne para a página **Colunas** para mapear colunas de origem para colunas de destino para o fluxo de dados do SSIS.  
  
  
