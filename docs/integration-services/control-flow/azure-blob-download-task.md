---
title: "Tarefa de Download do Blob do Azure | Microsoft Docs"
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
  - "sql13.dts.designer.afpblobdltask.f1"
  - "sql14.dts.designer.afpblobdltask.f1"
ms.assetid: 8a63bf44-71be-456d-9a5c-be7c31aff065
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 12
---
# Tarefa de Download do Blob do Azure
  A Tarefa de Download do Blob do Azure permite que um pacote SSIS baixe arquivos de um armazenamento de blob do Azure.

>   [!NOTE] Para garantir que o Gerenciador de Conexões do Armazenamento do Azure e os componentes que o utilizam (isto é, a Fonte, Destino, Tarefa de Upload e Tarefa de Download do Blob) possam se conectar tanto a contas de armazenamento de uso geral quanto a contas de armazenamento de blobs, verifique se você baixou a versão mais recente do Azure Feature Pack [aqui](https://www.microsoft.com/download/details.aspx?id=49492). Para obter mais informações sobre esses dois tipos de contas de armazenamento, consulte [Introdução ao Armazenamento do Microsoft Azure](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts).
   
Para adicionar uma **Tarefa de Download de Blobs do Azure**, arraste-a e solte-a no Designer SSIS, e clique duas vezes ou com o botão direito do mouse em **Editar** para ver a caixa de diálogo **Editor da Tarefa de Download de Blobs do Azure**.  
  
 A **Tarefa de Download de Blobs do Azure** é um componente do SSIS (SQL Server Integration Services) Feature Pack para Azure do SQL Server 2016. Baixe o Feature Pack [daqui](http://go.microsoft.com/fwlink/?LinkID=626967).  
  
 A tabela a seguir fornece uma descrição para os campos nessa caixa de diálogo.  
  
|||  
|-|-|  
|**Campo**|**Description**|  
|AzureStorageConnection|Especifique um Gerenciador de Conexão de Armazenamento do Azure existente ou crie um novo referindo-se a uma Conta de Armazenamento do Azure, que aponta para onde os arquivos de blob estão hospedados.|  
|BlobContainer|Especifica o nome do contêiner de Blob que contém os arquivos de Blob a serem baixados.|  
|BlobDirectory|Especifica o diretório de Blob que contém os arquivos de Blob a serem baixados. O diretório de Blob é uma estrutura hierárquica virtual.|  
|LocalDirectory|Especifica o diretório local onde serão armazenados os arquivos de blob baixados.|  
|FileName|Especifica um filtro de nome para selecionar arquivos com o padrão de nome especificado. Por ex.: MySheet*.xls\* inclui arquivos como MySheet001.xls e MySheetABC.xlsx.|  
|TimeRangeFrom/TimeRangeTo|Especifica um filtro de intervalo de tempo. Arquivos modificados após **TimeRangeFrom** e antes de **TimeRangeTo** serão incluídos.|  
  
  