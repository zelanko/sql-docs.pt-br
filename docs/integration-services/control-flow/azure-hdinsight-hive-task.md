---
description: Tarefa do Hive do Azure HDInsight
title: Tarefa do Hive do Azure HDInsight | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afphivetask.f1
- sql14.dts.designer.afphivetask.f1
ms.assetid: e1896c73-128a-4128-9814-3e01f7dfe19b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0c327451deeb763605dc9e66862fe275046cddb9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88496014"
---
# <a name="azure-hdinsight-hive-task"></a>Tarefa do Hive do Azure HDInsight

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


Use a **Tarefa do Hive do Azure HDInsight** para executar o script do Hive em um cluster Azure HDInsight.
     
Para adicionar uma **Tarefa do Hive do Azure HDInsight**, arraste e solte-a no Designer SSIS e clique duas vezes ou com o botão direito do mouse e clique em **Editar** para ver a caixa de diálogo **Editor de Tarefa do Hive do Azure HDInsight** a seguir.  
  
A **Tarefa do Hive do Azure HDInsight** é um componente do [SSIS (SQL Server Integration Services) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
 A lista a seguir descreve os campos dessa caixa de diálogo.  
  
1.  Para o campo **HDInsightConnection**, selecione um Gerenciador de Conexões do Azure HDInsight existente ou crie um novo que se refere ao cluster do Azure HDInsight usado para executar o script.
  
2.  Para o campo **AzureStorageConnection**, selecione um Gerenciador de Conexões do Armazenamento do Azure existente ou crie um novo que se refere à Conta de Armazenamento do Azure associada ao cluster. Isso só é necessário se você deseja baixar os logs de erro e de saída de execução do script.
 
3.  Para o campo **BlobContainer**, especifique o nome do contêiner de armazenamento associado ao cluster. Isso só é necessário se você deseja baixar os logs de erro e de saída de execução do script.
  
4.  Para o campo **LocalLogFolder**, especifique a pasta para a qual os logs de erro e de saída de execução do script serão baixados. Isso só é necessário se você deseja baixar os logs de erro e de saída de execução do script.   
  
5.  Há duas maneiras de especificar o script do Hive a ser executado:
  
    1.  **Script em linha**: especifique o campo **Script** digitando em linha o script a ser executado na caixa de diálogo **Inserir Script**.
  
    2.  **Arquivo de script**: carregue o arquivo de script para o Armazenamento de Blobs do Azure e especifique o campo **BlobName**. Se o blob não estiver na conta de armazenamento padrão ou no contêiner associado ao cluster HDInsight, os campos **ExternalStorageAccountName** e **ExternalBlobContainer** deverão ser especificados. Para um blob externo, verifique se ele está configurado como acessível ao público.  
  
     Se ambos estiverem especificados, o arquivo de script será usado e o script embutido será ignorado.
