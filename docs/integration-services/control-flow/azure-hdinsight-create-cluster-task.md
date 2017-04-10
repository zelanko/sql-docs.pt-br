---
title: "Tarefa Criar Cluster do Azure HDInsight | Microsoft Docs"
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
  - "sql13.dts.designer.afpcreatecltask.f1"
  - "sql14.dts.designer.afpcreatecltask.f1"
ms.assetid: a8ec413a-38d3-45df-887e-6f5f4d9f8465
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Tarefa Criar Cluster do Azure HDInsight
  A **Tarefa Criar Cluster do Azure HDInsight** permite que um pacote do SSIS crie um cluster do Azure HDInsight na assinatura do Azure especificada.  
  
 A **Tarefa Criar Cluster do Azure HDInsight** é um componente do SSIS (SQL Server Integration Services) Feature Pack para Azure do SQL Server 2016. Baixe o Feature Pack [daqui](http://go.microsoft.com/fwlink/?LinkID=626967).  
  
> [!NOTE]  
>  -   Criar um novo cluster HDInsight geralmente leva 10 minutos.  
> -   Há um custo associado à criação e execução de um cluster Azure HDInsight. Consulte o tópico [Preços do HDInsight](http://azure.microsoft.com/en-us/pricing/details/hdinsight/) para ver mais detalhes.  
  
 Para adicionar uma **Tarefa Criar Cluster do Azure HDInsight**, arraste e solte-a no Designer SSIS e clique duas vezes ou, com o botão direito do mouse, clique em **Editar** para ver a caixa de diálogo **Editor de Tarefa Criar Cluster do Azure HDInsight** a seguir.  
  
 A tabela a seguir fornece uma descrição dos campos nesta caixa de diálogo.  
  
|||  
|-|-|  
|**Campo**|**Description**|  
|AzureSubscriptionConnection|Selecione um Gerenciador de conexão de assinatura do Azure existente ou crie um novo que se refere a uma assinatura do Azure que hospeda o cluster do HDInsight.|  
|AzureStorageConnection|Selecione um Gerenciador de conexão de armazenamento do Azure existente ou crie um novo, relacionado a uma conta de armazenamento do Azure, que será associado com o cluster HDInsight.|  
|Local|Especifique o local do cluster HDInsight. O cluster deve ser criado no mesmo local que o Armazenamento do Azure.|  
|ClusterName|Especifique um nome para o cluster HDInsight que será criado.|  
|ClusterSize|Especifique o número de nós que devem estar no cluster.|  
|BlobContainer|Especifique o nome do contêiner de armazenamento padrão associado ao cluster HDInsight.|  
|UserName|Especifique o nome do usuário que terá acesso ao cluster.|  
|Senha|Especifique a senha para o usuário.|  
|FailIfExists|Especifique se a tarefa deve falhar ou não caso o cluster já exista.|  
  
> [!NOTE]  
>  O local do cluster HDInsight e do Armazenamento do Azure deve ser o mesmo.  
  
  