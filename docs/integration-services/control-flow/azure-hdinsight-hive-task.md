---
title: Tarefa do Hive do Azure HDInsight | Microsoft Docs
ms.custom: 
ms.date: 02/28/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afphivetask.f1
- sql14.dts.designer.afphivetask.f1
ms.assetid: e1896c73-128a-4128-9814-3e01f7dfe19b
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f9e67e91b5cd38482ab1151d5942c9c55c04136c
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-hive-task"></a>Tarefa do Hive do Azure HDInsight
Use a **Tarefa do Hive do Azure HDInsight** para executar o script do Hive em um cluster Azure HDInsight.
     
Para adicionar uma **Tarefa do Hive do Azure HDInsight**, arraste e solte-a no Designer SSIS e clique duas vezes ou com o botão direito do mouse e clique em **Editar** para ver a caixa de diálogo **Editor de Tarefa do Hive do Azure HDInsight** a seguir.  
  
O **tarefa Hive** é um componente do [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
 A lista a seguir descreve os campos dessa caixa de diálogo.  
  
1.  Para o **HDInsightConnection** campo, selecione um Gerenciador de Conexão de HDInsight do Azure existente ou crie um novo que se refere ao cluster HDInsight do Azure usada para executar o script.
  
2.  Para o **AzureStorageConnection** campo, selecione um Gerenciador de Conexão de armazenamento do Azure existente ou crie um novo que se refere à conta de armazenamento do Azure associada ao cluster. Isso só é necessário se você deseja baixar os logs de saída e o erro de execução do script.
 
3.  Para o **BlobContainer** , especifique o nome do contêiner de armazenamento associado ao cluster. Isso só é necessário se você deseja baixar os logs de saída e o erro de execução do script.
  
4.  Para o **LocalLogFolder** campo, especifique a pasta à qual os logs de saída e o erro de execução do script serão baixados no. Isso só é necessário se você deseja baixar os logs de saída e o erro de execução do script.   
  
5.  Há duas maneiras de especificar o script de Hive:
  
    1.  **Script em linha**: especifique o **Script** campo digitando o script seja executado no embutido a **Inserir Script** caixa de diálogo.
  
    2.  **Arquivo de script**: Carregue o arquivo de script para o armazenamento de Blob do Azure e especifique o **BlobName** campo. Se o blob não estiver na conta de armazenamento padrão ou no contêiner associado ao cluster HDInsight, o **ExternalStorageAccountName** e **ExternalBlobContainer** campos devem ser especificados. Para um blob externo, verifique se ele está configurado como publicamente acessível.  
  
     Se ambos forem especificados, o arquivo de script será usado e o script em linha será ignorado.

