---
title: Azure tarefa excluir Cluster HDInsight | Microsoft Docs
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
- sql13.dts.designer.afpdelcltask.f1
- sql14.dts.designer.afpdelcltask.f1
ms.assetid: e298776e-d18a-4393-a8e6-65ee3d555749
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f98b69e8bd3b2e78f6dd20a19ca17a83a834c3b3
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-delete-cluster-task"></a>Tarefa Excluir Cluster do Azure HDInsight
O **Azure tarefa excluir Cluster HDInsight** permite que um pacote do SSIS exclua um cluster HDInsight do Azure ao grupo de recursos e assinatura do Azure especificado.
  
O **Azure tarefa excluir Cluster HDInsight** é um componente do [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
> [!NOTE]
> Excluir um cluster HDInsight pode levar 10 ~ 20 minutos.  
  
Para adicionar uma **Tarefa Excluir Cluster do Azure HDInsight**, arraste e solte-a no Designer SSIS e clique duas vezes ou com o botão direito do mouse e clique em **Editar** para ver a caixa de diálogo **Editor de Tarefa Excluir Cluster do Azure HDInsight** a seguir.  
  
A tabela a seguir fornece uma descrição dos campos na caixa de diálogo.  
  
|||  
|-|-|  
|**Campo**|**Description**|  
|AzureResourceManagerConnection|Selecione um Gerenciador de Conexão do Gerenciador de recursos do Azure existente ou crie um novo que será usado para excluir o cluster HDInsight.|
|subscriptionId|Especifique a ID da assinatura, em que o cluster HDInsight está.|
|Grupo de recursos|Especifique o grupo de recursos do Azure que está o cluster HDInsight.|
|ClusterName|Especifique o nome do cluster a ser excluído.|  
|FailIfNotExists|Especifique se a tarefa deve falhar ou não caso o cluster não exista.|

