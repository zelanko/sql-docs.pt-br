---
title: Executar conjuntos de coleção utilitário e não utilitário na mesma instância do SQL | Microsoft Docs
description: Saiba como monitorar uma instância do SQL Server usando conjuntos de coleta utilitários e não utilitários que funcionam lado a lado. Veja os requisitos de configuração.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ca7ee9b3-ef9a-4ba4-83d0-9ee9f80dab27
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 522b21e2a2c7e78c8ca16483fc02f2564e0ebaf5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773468"
---
# <a name="run-utility-and-non-utility-collection-sets-on-same-sql-instance"></a>Executar conjuntos de coleção utilitário e não utilitário na mesma instância do SQL
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
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
  
## <a name="see-also"></a>Consulte Também  
 [Recursos e tarefas do Utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Configurar o data warehouse do ponto de controle do utilitário &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/configure-your-utility-control-point-data-warehouse-sql-server-utility.md)  
  
  
