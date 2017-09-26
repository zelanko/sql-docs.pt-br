---
title: HDInsight do Azure tarefa criar Cluster | Microsoft Docs
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
- sql13.dts.designer.afpcreatecltask.f1
- sql14.dts.designer.afpcreatecltask.f1
ms.assetid: a8ec413a-38d3-45df-887e-6f5f4d9f8465
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 71a24dc15253916c32b07e6024e2ab32514c9d39
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-create-cluster-task"></a>Tarefa Criar Cluster do Azure HDInsight
O **Azure tarefa criar Cluster HDInsight** permite que um pacote do SSIS criar um cluster Azure HDInsight ao grupo de recursos e assinatura do Azure especificado.
  
O **Azure tarefa criar Cluster HDInsight** é um componente do [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
> [!NOTE]  
> - Criar um novo cluster HDInsight pode levar 10 ~ 20 minutos.  
> - Há um custo associado à criação e execução de um cluster Azure HDInsight. Consulte [preços do HDInsight](http://azure.microsoft.com/en-us/pricing/details/hdinsight/) para obter detalhes.  
  
Para adicionar uma **Tarefa Criar Cluster do Azure HDInsight**, arraste e solte-a no Designer SSIS e clique duas vezes ou, com o botão direito do mouse, clique em **Editar** para ver a caixa de diálogo **Editor de Tarefa Criar Cluster do Azure HDInsight** a seguir.  
  
A tabela a seguir fornece uma descrição dos campos nessa caixa de diálogo.  
  
|||  
|-|-|  
|**Campo**|**Description**|  
|AzureResourceManagerConnection|Selecione um Gerenciador de Conexão do Gerenciador de recursos do Azure existente ou crie um novo que será usado para criar o cluster HDInsight.|  
|AzureStorageConnection|Selecione um Gerenciador de conexão de armazenamento do Azure existente ou crie um novo, relacionado a uma conta de armazenamento do Azure, que será associado com o cluster HDInsight.|
|subscriptionId|Especifique a ID da assinatura que será criado no cluster HDInsight.|
|Grupo de recursos|Especifique o HDInsight cluster será criado no grupo dos recursos do Azure.|
|Local|Especifique o local do cluster HDInsight. O cluster deve ser criado no mesmo local que a conta de armazenamento do Azure especificada.|  
|ClusterName|Especifique um nome para o cluster HDInsight que será criado.|  
|ClusterSize|Especifique o número de nós para criar o cluster.|  
|BlobContainer|Especifique o nome do contêiner de armazenamento padrão a ser associado com o cluster HDInsight.|  
|UserName|Especifique o nome de usuário a ser usado para conectar-se ao cluster HDInsight.|  
|Senha|Especifique a senha a ser usada para conectar-se ao cluster HDInsight.|
|SshUserName|Especifique o nome de usuário usado para acessar remotamente o cluster HDInsight usando o SSH.|
|SshPassword|Especifique a senha usada para acessar remotamente o cluster HDInsight usando o SSH.|
|FailIfExists|Especifique se a tarefa deve falhar ou não caso o cluster já exista.|  
  
> [!NOTE]  
> Os locais do cluster HDInsight e a conta de armazenamento do Azure devem ser o mesmo.

