---
title: Configurar políticas de integridade (Utilitário do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 030aac3b-8901-4c41-91ed-aba96420276c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c59138d5d1f06ffee0266f9e97d5faf46ef28f08
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68115440"
---
# <a name="configure-health-policies-sql-server-utility"></a>Configurar políticas de integridade (Utilitário do SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use o painel do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para exibir parâmetros de recursos do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aplicativos da camada de dados. Para obter mais informações, consulte [Recursos e tarefas do utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
 Para exibir os resultados da política de integridade do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , conecte-se a um ponto de controle de utilitário no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para obter mais informações, consulte [Usar o Gerenciador do Utilitário para gerenciar o Utilitário do SQL Server](../../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] As políticas de integridade do Utilitário podem ser configuradas para aplicativos da camada de dados e instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As políticas de integridade podem ser definidas globalmente para todos os aplicativos da camada de dados e instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou podem ser definidas individualmente para cada aplicativo da camada de dados e para cada instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="monitoring-policies-for-data-tier-applications"></a>Monitorando políticas para aplicativos da camada de dados  
 As políticas de superutilização e subutilização para aplicativos da camada de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são as seguintes:  
  
-   Utilização do processador de aplicativo da camada de dados.  
  
-   Espaço de arquivo de aplicativo da camada de dados para arquivos de banco de dados.  
  
-   Espaço de arquivo de aplicativo da camada de dados para volumes de armazenamento.  
  
-   Utilização do processador do computador.  
  
> [!NOTE]  
>  O volume de armazenamento e a utilização do processador são políticas somente leitura para aplicativos da camada de dados.  
  
 Para obter mais informações sobre como exibir ou alterar políticas de monitoramento globais para aplicativos da camada de dados, consulte [Administração do Utilitário &#40;Utilitário do SQL Server&#41;](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d).  
  
 Para obter mais informações sobre como exibir ou alterar as políticas de monitoramento para aplicativos da camada de dados individuais, consulte [Detalhes do aplicativo da camada de dados implantado &#40;Utilitário do SQL Server&#41;](https://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867).  
  
## <a name="monitoring-policies-for-managed-instances-of-sql-server"></a>Políticas de monitoramento para instâncias gerenciadas do SQL Server  
 As políticas de superutilização e de subutilização para instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são as seguintes:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para arquivos de banco de dados.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para volumes de armazenamento.  
  
-   Utilização do processador do computador.  
  
 Para obter mais informações sobre como exibir ou alterar políticas de monitoramento globais para instâncias gerenciadas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Administração do Utilitário &#40;Utilitário do SQL Server&#41;](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d).  
  
 Para obter mais informações sobre como exibir ou alterar as políticas de monitoramento para instâncias gerenciadas individuais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Detalhes de instâncias gerenciadas &#40;Utilitário do SQL Server&#41;](https://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2).  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos e tarefas do Utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Reduzir o ruído em políticas de utilização da CPU &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)  
  
  
