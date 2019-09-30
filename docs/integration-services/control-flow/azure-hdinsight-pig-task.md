---
title: Tarefa do Pig do Azure HDInsight | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afppigtask.f1
- sql14.dts.designer.afppigtask.f1
ms.assetid: 26f34f64-f344-486e-9190-acf71aef29a8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 44d6fd9052b2f36381b95223222ec9008a8e4728
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298410"
---
# <a name="azure-hdinsight-pig-task"></a>Tarefa de Pig de HDInsight do Azure

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Use a **Tarefa de Pig do Azure HDInsight** para executar o script do Pig em um cluster Azure HDInsight.
     
Para adicionar uma **Tarefa do Pig do Azure HDInsight**, arraste e solte-a no Designer do SSIS e clique duas vezes ou com o botão direito do mouse e clique em **Editar** para ver a caixa de diálogo **Editor de Tarefa do Pig do Azure HDInsight** a seguir.  
  
A **Tarefa do Pig do Azure HDInsight** é um componente do [SSIS (SQL Server Integration Services) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
 A lista a seguir descreve os campos dessa caixa de diálogo.  
  
1.  Para o campo **HDInsightConnection**, selecione um Gerenciador de Conexões do Azure HDInsight existente ou crie um novo que se refere ao cluster do Azure HDInsight usado para executar o script.
  
2.  Para o campo **AzureStorageConnection**, selecione um Gerenciador de Conexões do Armazenamento do Azure existente ou crie um novo que se refere à Conta de Armazenamento do Azure associada ao cluster. Isso só é necessário se você deseja baixar os logs de erro e de saída de execução do script.
 
3.  Para o campo **BlobContainer**, especifique o nome do contêiner de armazenamento associado ao cluster. Isso só é necessário se você deseja baixar os logs de erro e de saída de execução do script.
  
4.  Para o campo **LocalLogFolder**, especifique a pasta para a qual os logs de erro e de saída de execução do script serão baixados. Isso só é necessário se você deseja baixar os logs de erro e de saída de execução do script.   
  
5.  Há duas maneiras de especificar o script do Pig a ser executado:
  
    1.  **Script embutido**: especifique o campo **Script**, digitando em linha o script a ser executado na caixa de diálogo **Inserir Script**.
  
    2.  **Arquivo de script**: carregue o arquivo de script para o Armazenamento de Blobs do Azure e especifique o campo **BlobName**. Se o blob não estiver na conta de armazenamento padrão ou no contêiner associado ao cluster HDInsight, os campos **ExternalStorageAccountName** e **ExternalBlobContainer** deverão ser especificados. Para um blob externo, verifique se ele está configurado como acessível ao público.  
  
     Se ambos estiverem especificados, o arquivo de script será usado e o script embutido será ignorado.
