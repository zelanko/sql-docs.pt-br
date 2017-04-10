---
title: "Fonte de Blobs do Azure | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "07/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.afpblobsrc.f1"
  - "sql14.dts.designer.afpblobsrc.f1"
ms.assetid: 80645c5c-88c8-4fb0-8607-de1bb7bffcbb
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Fonte de Blobs do Azure
  O componente de **Fonte de Blobs do Azure** permite que um pacote SSIS leia dados de um blob do Azure. Os formatos de arquivo com suporte são: CSV e AVRO.
  
>   [!NOTE] Para garantir que o Gerenciador de Conexões do Armazenamento do Azure e os componentes que o utilizam (isto é, a Fonte, Destino, Tarefa de Upload e Tarefa de Download do Blob) possam se conectar tanto a contas de armazenamento de uso geral quanto a contas de armazenamento de blobs, verifique se você baixou a versão mais recente do Azure Feature Pack [aqui](https://www.microsoft.com/download/details.aspx?id=49492). Para obter mais informações sobre esses dois tipos de contas de armazenamento, consulte [Introdução ao Armazenamento do Microsoft Azure](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts).
  
  Para ver o editor da Fonte de Blobs do Azure, arraste e solte **Fonte de Blobs do Azure** no designer de fluxo de dados e clique duas vezes nele para abrir o editor.  
  
 A **Fonte de Blobs** do Azure é um componente do SSIS (SQL Server Integration Services) Feature Pack para Azure do SQL Server 2016. Baixe o Feature Pack [daqui](http://go.microsoft.com/fwlink/?LinkID=626967).  
  
1.  Para o campo **Gerenciador de conexões do armazenamento do Azure** , especifique um Gerenciador de Conexões do Armazenamento do Azure existente ou crie um novo referindo-se a uma Conta de Armazenamento do Azure.  
  
2.  Para o campo **Nome do contêiner de blobs** , especifique o nome do contêiner de blobs que contém os arquivos de origem.  
  
3.  Para o campo **Nome do Blob** , especifique o caminho para o blob.  
  
4.  Para o campo **Formato de arquivo de blob** , especifique o formato de blob que você deseja usar.  
  
5.  Se o formato de arquivo for CSV, você deverá especificar o valor de **Caractere delimitador de coluna** . Além disso, selecione **Nomes de coluna na primeira linha de dados** se a primeira linha no arquivo contiver nomes de coluna.  
  
6.  Depois de especificar as informações de conexão, alterne para a página **Colunas** para mapear colunas de origem para colunas de destino para o fluxo de dados do SSIS.  
  
  