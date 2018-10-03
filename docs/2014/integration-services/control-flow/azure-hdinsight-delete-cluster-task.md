---
title: Tarefa Excluir Cluster do Azure HDInsight | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpdelcltask.f1
- sql11.dts.designer.afpdelcltask.f1
ms.assetid: e298776e-d18a-4393-a8e6-65ee3d555749
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fc5564e70c73830f89bc11cc2d6c59d3c2974862
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48078916"
---
# <a name="azure-hdinsight-delete-cluster-task"></a>Tarefa Excluir Cluster do Azure HDInsight
A **Tarefa Excluir Cluster do Azure HDInsight** permite que um pacote do SSIS exclua um cluster do Azure HDInsight na assinatura e grupo de recursos do Azure especificados.
  
> [!NOTE]
> Excluir um cluster HDInsight pode levar entre 10 e 20 minutos.  
  
Para adicionar uma **Tarefa Excluir Cluster do Azure HDInsight**, arraste e solte-a no Designer SSIS e clique duas vezes ou com o botão direito do mouse e clique em **Editar** para ver a caixa de diálogo **Editor de Tarefa Excluir Cluster do Azure HDInsight** a seguir.  
  
A tabela a seguir fornece uma descrição dos campos nessa caixa de diálogo.  
  
|||  
|-|-|  
|**Campo**|**Descrição**|  
|AzureResourceManagerConnection|Selecione um gerenciador de conexões do Azure Resource Manager existente ou crie um novo que será usado para excluir o cluster HDInsight.|
|SubscriptionId|Especifique a ID da assinatura na qual o cluster HDInsight está.|
|ResourceGroup|Especifique o grupo de recursos do Azure no qual o cluster HDInsight está.|
|ClusterName|Especifique o nome do cluster a ser excluído.|  
|FailIfNotExists|Especifique se a tarefa deve falhar ou não caso o cluster não exista.|
