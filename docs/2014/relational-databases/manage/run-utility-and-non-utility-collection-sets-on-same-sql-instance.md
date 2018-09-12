---
title: Considerações sobre a execução e não - utilitário de conjuntos de coleta na mesma instância do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ca7ee9b3-ef9a-4ba4-83d0-9ee9f80dab27
caps.latest.revision: 5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 52afbefb6f8a6dc42c1de2503bbe1dadc564962f
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43816592"
---
# <a name="considerations-for-running-utility-and-non-utility-collection-sets-on-the-same-instance-of-sql-server"></a>Considerações sobre a execução de Conjuntos de Coleta do Utilitário e não Utilitário na mesma instância do SQL Server
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
 [Recursos e tarefas do Utilitário do SQL Server](sql-server-utility-features-and-tasks.md)   
 [Configurar o data warehouse do ponto de controle do utilitário &#40;Utilitário do SQL Server&#41;](configure-your-utility-control-point-data-warehouse-sql-server-utility.md)  
  
  
