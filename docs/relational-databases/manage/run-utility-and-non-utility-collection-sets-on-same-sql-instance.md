---
title: "Executar conjuntos de coleção utilitário e não utilitário na mesma instância do SQL | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ca7ee9b3-ef9a-4ba4-83d0-9ee9f80dab27
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d6f1a687472d2ee83f48fe273008a0d60f51bc58
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="run-utility-and-non-utility-collection-sets-on-same-sql-instance"></a>Executar conjuntos de coleção utilitário e não utilitário na mesma instância do SQL
  O conjunto de coleta do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility tem suporte lado a lado com conjuntos de coleta não Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ou seja, uma instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser monitorada por outros conjuntos de coleta enquanto ainda é membro de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility. No entanto, você deve desabilitar a funcionalidade de coleta de dados não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility enquanto a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo inscrita no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility.  
  
 Depois que a instância for inscrita no UCP, você poderá reiniciar conjuntos de coleta não - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility. Observe, no entanto, que todos os conjuntos de coleta na instância gerenciada carregarão seus dados no UMDW (data warehouse de gerenciamento do utilitário); o nome de arquivo UMDW é sysutility_mdw.  
  
 Para executar conjuntos de coleta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility lado a lado com conjuntos de coleta não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility, leve em consideração os seguintes pontos:  
  
-   Há suporte para conjuntos de coleta lado a lado.  
  
-   Você deve desabilitar os coletores de dados existentes ao inscrever instâncias no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility.  
  
-   Para cumprir os requisitos de validação, você deve executar os seguintes procedimentos armazenados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , antes de criar um UCP, e na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , antes de inscrevê-lo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility:  
  
    ```  
    exec msdb.dbo.sp_syscollector_set_warehouse_database_name NULL  
    exec msdb.dbo.sp_syscollector_set_warehouse_instance_name NULL  
    ```  
  
     Se você não executar esses procedimentos armazenados antes de iniciar o Assistente para Criar UCP ou o Assistente para Adicionar Instância Gerenciada, a operação falhará.  
  
-   Você deve usar o UMDW (sysutility_mdw) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility para todos os conjuntos de coleta em uma instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Recursos e tarefas do utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Configurar o data warehouse do ponto de controle do utilitário &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/configure-your-utility-control-point-data-warehouse-sql-server-utility.md)  
  
  
