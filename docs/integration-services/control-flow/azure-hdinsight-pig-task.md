---
title: Tarefa de Pig de HDInsight do Azure | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 02/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afppigtask.f1
- sql14.dts.designer.afppigtask.f1
ms.assetid: 26f34f64-f344-486e-9190-acf71aef29a8
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9874b119b634966b146f8fa9d22c016bcd91617b
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-pig-task"></a>Tarefa de Pig de HDInsight do Azure
Use a **Tarefa de Pig do Azure HDInsight** para executar o script do Pig em um cluster Azure HDInsight.
     
Para adicionar uma **Tarefa do Pig do Azure HDInsight**, arraste e solte-a no Designer do SSIS e clique duas vezes ou com o botão direito do mouse e clique em **Editar** para ver a caixa de diálogo **Editor de Tarefa do Pig do Azure HDInsight** a seguir.  
  
O **tarefa de Pig de HDInsight do Azure** é um componente do [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
 A lista a seguir descreve os campos dessa caixa de diálogo.  
  
1.  Para o **HDInsightConnection** campo, selecione um Gerenciador de Conexão de HDInsight do Azure existente ou crie um novo que se refere ao cluster HDInsight do Azure usada para executar o script.
  
2.  Para o **AzureStorageConnection** campo, selecione um Gerenciador de Conexão de armazenamento do Azure existente ou crie um novo que se refere à conta de armazenamento do Azure associada ao cluster. Isso só é necessário se você deseja baixar os logs de saída e o erro de execução do script.
 
3.  Para o **BlobContainer** , especifique o nome do contêiner de armazenamento associado ao cluster. Isso só é necessário se você deseja baixar os logs de saída e o erro de execução do script.
  
4.  Para o **LocalLogFolder** campo, especifique a pasta à qual os logs de saída e o erro de execução do script serão baixados no. Isso só é necessário se você deseja baixar os logs de saída e o erro de execução do script.   
  
5.  Há duas maneiras de especificar o script de Pig:
  
    1.  **Script em linha**: especifique o **Script** campo digitando o script seja executado no embutido a **Inserir Script** caixa de diálogo.
  
    2.  **Arquivo de script**: Carregue o arquivo de script para o armazenamento de Blob do Azure e especifique o **BlobName** campo. Se o blob não estiver na conta de armazenamento padrão ou no contêiner associado ao cluster HDInsight, o **ExternalStorageAccountName** e **ExternalBlobContainer** campos devem ser especificados. Para um blob externo, verifique se ele está configurado como publicamente acessível.  
  
     Se ambos forem especificados, o arquivo de script será usado e o script em linha será ignorado.

