---
title: "Tarefa Excluir Cluster do Azure HDInsight | Microsoft Docs"
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
  - "sql13.dts.designer.afpdelcltask.f1"
  - "sql14.dts.designer.afpdelcltask.f1"
ms.assetid: e298776e-d18a-4393-a8e6-65ee3d555749
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# Tarefa Excluir Cluster do Azure HDInsight
  A **Tarefa Excluir Cluster do Azure HDInsight** permite que um pacote do SSIS exclua um cluster do Azure HDInsight na assinatura do Azure especificada.  
  
 A **Tarefa Excluir Cluster do Azure HDInsight** é um componente do SSIS (SQL Server Integration Services) Feature Pack para Azure do SQL Server 2016. Baixe o Feature Pack [daqui](http://go.microsoft.com/fwlink/?LinkID=626967).  
  
> [!NOTE]  
>  Excluir um cluster HDInsight geralmente leva 10 minutos.  
  
 Para adicionar uma **Tarefa Excluir Cluster do Azure HDInsight**, arraste e solte-a no Designer SSIS e clique duas vezes ou com o botão direito do mouse e clique em **Editar** para ver a caixa de diálogo **Editor de Tarefa Excluir Cluster do Azure HDInsight** a seguir.  
  
 A tabela a seguir fornece uma descrição dos campos na caixa de diálogo.  
  
|||  
|-|-|  
|**Campo**|**Description**|  
|AzureSubscriptionConnection|Selecione um Gerenciador de conexão de assinatura do Azure existente ou crie um novo que se refere a uma assinatura do Azure que hospeda o cluster do HDInsight.|  
|ClusterName|Especifique o nome do cluster a ser excluído.|  
|FailIfNotExists|Especifique se a tarefa deve falhar ou não caso o cluster não exista.|  
  
  