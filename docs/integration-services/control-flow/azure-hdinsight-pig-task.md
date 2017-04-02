---
title: "Tarefa de Pig de HDInsight do Azure | Microsoft Docs"
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
  - "sql13.dts.designer.afppigtask.f1"
  - "sql14.dts.designer.afppigtask.f1"
ms.assetid: 26f34f64-f344-486e-9190-acf71aef29a8
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# Tarefa de Pig de HDInsight do Azure
  Use a **Tarefa de Pig do Azure HDInsight** para executar o script do Pig em um cluster Azure HDInsight. 
    
Para adicionar uma **Tarefa do Pig do Azure HDInsight**, arraste e solte-a no Designer do SSIS e clique duas vezes ou com o botão direito do mouse e clique em **Editar** para ver a caixa de diálogo **Editor de Tarefa do Pig do Azure HDInsight** a seguir.  
  
 A **Tarefa do Pig do Azure HDInsight** é um componente do SSIS (SQL Server Integration Services) Feature Pack para Azure do SQL Server 2016. Baixe o Feature Pack [daqui](http://go.microsoft.com/fwlink/?LinkID=626967).  
  
1.  No campo **AzureSubscriptionConnection** , selecione um Gerenciador de conexão de assinatura do Azure existente ou crie um novo que se refere a uma assinatura do Azure que hospeda o cluster do HDInsight.  
  
2.  No campo **HDInsightClusterName** , selecione o nome do cluster HDInsight no qual você deseja executar o script do Pig.  
  
3.  No campo **LocalLogFolder**, clique em **... (reticências)** e selecione a pasta na qual você quer baixar os logs de processamento do Pig do cluster HDInsight.  
  
4.  Há duas maneiras de especificar o script do Pig:  
  
    1.  **Script em linha**: clique em **... (reticências)** ao lado do campo **Script** e digite o script em linha na caixa de diálogo **Inserir Script**.  
  
    2.  **Arquivo de script**: carregue o arquivo de script para um local de blob e especifique seu **BlobName**. Se o blob não estiver no repositório padrão ou no contêiner do cluster HDInsight, **ExternalStorageAccountName** e **ExternalBlobContainer** deverão ser especificados. Para o blob externo, verifique se ele está configurado como acessível ao público.  
  
     Se ambos forem especificados, o arquivo de script será usado e o script em linha será ignorado.  
  
  