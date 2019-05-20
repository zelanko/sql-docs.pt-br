---
title: Tarefa Excluir Cluster do Azure HDInsight | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpdelcltask.f1
- sql14.dts.designer.afpdelcltask.f1
ms.assetid: e298776e-d18a-4393-a8e6-65ee3d555749
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d9f33fa68288f216f0b4cbac61f1ef75086feb21
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727975"
---
# <a name="azure-hdinsight-delete-cluster-task"></a>Tarefa Excluir Cluster do Azure HDInsight

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


A **Tarefa Excluir Cluster do Azure HDInsight** permite que um pacote do SSIS exclua um cluster do Azure HDInsight na assinatura e grupo de recursos do Azure especificados.
  
A **Tarefa Excluir Cluster do Azure HDInsight** é um componente do [SSIS (SQL Server Integration Services) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
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
