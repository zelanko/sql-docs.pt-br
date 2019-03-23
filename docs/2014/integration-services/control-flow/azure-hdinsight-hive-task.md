---
title: Tarefa do Hive do Azure HDInsight | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afphivetask.f1
- sql11.dts.designer.afphivetask.f1
ms.assetid: e1896c73-128a-4128-9814-3e01f7dfe19b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f7b61bd02d44639cb3f5ad540d53ebeebcff4da0
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58391664"
---
# <a name="azure-hdinsight-hive-task"></a>Tarefa do Hive do Azure HDInsight
Use a **Tarefa do Hive do Azure HDInsight** para executar o script do Hive em um cluster Azure HDInsight.
     
Para adicionar uma **Tarefa do Hive do Azure HDInsight**, arraste e solte-a no Designer SSIS e clique duas vezes ou com o botão direito do mouse e clique em **Editar** para ver a caixa de diálogo **Editor de Tarefa do Hive do Azure HDInsight** a seguir.  
  
 A lista a seguir descreve os campos dessa caixa de diálogo.  
  
1.  Para o campo **HDInsightConnection**, selecione um Gerenciador de Conexões do Azure HDInsight existente ou crie um novo que se refere ao cluster do Azure HDInsight usado para executar o script.
  
2.  Para o campo **AzureStorageConnection**, selecione um Gerenciador de Conexões do Armazenamento do Azure existente ou crie um novo que se refere à Conta de Armazenamento do Azure associada ao cluster. Isso só é necessário se você deseja baixar os logs de erro e de saída de execução do script.
 
3.  Para o campo **BlobContainer**, especifique o nome do contêiner de armazenamento associado ao cluster. Isso só é necessário se você deseja baixar os logs de erro e de saída de execução do script.
  
4.  Para o campo **LocalLogFolder**, especifique a pasta para a qual os logs de erro e de saída de execução do script serão baixados. Isso só é necessário se você deseja baixar os logs de erro e de saída de execução do script.   
  
5.  Há duas maneiras de especificar o script do Hive a ser executado:
  
    1.  **Script em linha**: Especifique o **Script** campo digitando o script seja executado em embutido o **Inserir Script** caixa de diálogo.
  
    2.  **Arquivo de script**: Carregue o arquivo de script para o armazenamento de BLOBs do Azure e especifique o **BlobName** campo. Se o blob não estiver na conta de armazenamento padrão ou no contêiner associado ao cluster HDInsight, os campos **ExternalStorageAccountName** e **ExternalBlobContainer** deverão ser especificados. Para um blob externo, verifique se ele está configurado como acessível ao público.  
  
     Se ambos estiverem especificados, o arquivo de script será usado e o script embutido será ignorado.
