---
title: "Tarefa do Hive do Azure HDInsight | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "02/28/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.afphivetask.f1"
  - "sql14.dts.designer.afphivetask.f1"
ms.assetid: e1896c73-128a-4128-9814-3e01f7dfe19b
caps.latest.revision: 13
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Tarefa do Hive do Azure HDInsight
  Use a **Tarefa do Hive do Azure HDInsight** para executar o script do Hive em um cluster Azure HDInsight.
     
Para adicionar uma **Tarefa do Hive do Azure HDInsight**, arraste e solte-a no Designer SSIS e clique duas vezes ou com o botão direito do mouse e clique em **Editar** para ver a caixa de diálogo **Editor de Tarefa do Hive do Azure HDInsight** a seguir.  
  
 A **Tarefa do Hive do Azure HDInsight** é um componente do SSIS (SQL Server Integration Services) Feature Pack para Azure do SQL Server 2016. Baixe o Feature Pack [daqui](http://go.microsoft.com/fwlink/?LinkID=626967).  
  
 A lista a seguir descreve os campos dessa caixa de diálogo.  
  
1.  Para o campo **AzureSubscriptionConnection** , selecione um Gerenciador de conexão de assinatura do Azure existente ou crie um novo que se refere a uma assinatura do Azure que hospeda o cluster do HDInsight.  
  
2.  Para o **HDInsightClusterName** , escolha o nome do cluster HDInsight no qual você deseja executar o script do Hive.  
  
3.  Para o **LocalLogFolder**, clique em **... (reticências)** e escolha a pasta na qual você deseja baixar os logs de processamento do Hive do cluster HDInsight.  
  
4.  Há duas maneiras de especificar o script do Hive:  
  
    1.  **Script em linha**: clique em **... (reticências)** ao lado do campo **Script** e digite o script em linha na caixa de diálogo **Inserir Script**.  
  
    2.  **Arquivo de script**: carregue o arquivo de script para um local de blob e especifique seu **BlobName**. Se o blob não estiver no repositório padrão ou no contêiner do cluster HDInsight, **ExternalStorageAccountName** e **ExternalBlobContainer** deverão ser especificados. Para o blob externo, verifique se ele está configurado como acessível ao público.  
  
     Se ambos forem especificados, o arquivo de script será usado e o script em linha será ignorado.  
  
  