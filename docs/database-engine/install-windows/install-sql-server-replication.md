---
title: "Instalar a Replica&#231;&#227;o do SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "componentes [replicação do SQL Server]"
  - "instalações de linha de comando [replicação do SQL Server]"
  - "instalando a replicação"
  - "replicação [SQL Server], instalando"
  - "prompt de comando [replicação do SQL Server]"
ms.assetid: c50ad078-060b-4a8d-ad45-9e31a8d85729
caps.latest.revision: 41
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 41
---
# Instalar a Replica&#231;&#227;o do SQL Server
  É possível instalar componentes de replicação usando o Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um prompt de comando. Instale a replicação ao instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou ao modificar uma instância existente.  
  
 Depois da instalação dos componentes de replicação, é necessário configurar o servidor antes de usar a replicação. Para obter mais informações, veja [Configurar distribuição](../../relational-databases/replication/configure-distribution.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Se você instalar componentes de replicação ao modificar uma instância existente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é necessário parar e reiniciar o agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando a instalação for concluída. Essa ação ajuda a assegurar que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent reconheça os subsistemas de agente de replicação e possa chamar agentes de replicação em etapas de trabalho.  
  
## Instalando a replicação com o uso de instalação  
 **Para instalar a replicação ao instalar uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
-   Para instalar componentes de replicação, incluindo o RMO (Replication Management Objects), selecione **SQL Server Replication** na página **Seleção de Recursos** do Assistente de Instalação.  
  
## Instalando a replicação a partir do prompt de comando  
 **Para instalar a replicação ao instalar uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
-   Veja [Instalar o SQL Server 2016 por meio do Prompt de Comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
## Consulte também  
 [Instalar o SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016.md)   
 [Instalar o SQL Server 2016 do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [Recursos com suporte nas edições do SQL Server 2016](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
  
  