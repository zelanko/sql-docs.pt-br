---
title: "Instalar a Replicação do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- components [SQL Server replication]
- command line installations [SQL Server replication]
- installing replication
- replication [SQL Server], installing
- command prompt [SQL Server replication]
ms.assetid: c50ad078-060b-4a8d-ad45-9e31a8d85729
caps.latest.revision: 41
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 0afd7ea022cb4901e1f536a1066036f246802173
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-replication"></a>Instalar a Replicação do SQL Server
  É possível instalar componentes de replicação usando o Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um prompt de comando. Instale a replicação ao instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou ao modificar uma instância existente.  
  
 Depois da instalação dos componentes de replicação, é necessário configurar o servidor antes de usar a replicação. Para obter mais informações, veja [Configurar distribuição](../../relational-databases/replication/configure-distribution.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Se você instalar componentes de replicação ao modificar uma instância existente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é necessário parar e reiniciar o agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando a instalação for concluída. Essa ação ajuda a assegurar que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent reconheça os subsistemas de agente de replicação e possa chamar agentes de replicação em etapas de trabalho.  
  
## <a name="installing-replication-by-using-setup"></a>Instalando a replicação com o uso de instalação  
 **Para instalar a replicação ao instalar uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
-   Para instalar componentes de replicação, incluindo o RMO (Replication Management Objects), selecione **SQL Server Replication** na página **Seleção de Recursos** do Assistente de Instalação.  
  
## <a name="installing-replication-from-the-command-prompt"></a>Instalando a replicação a partir do prompt de comando  
 **Para instalar a replicação ao instalar uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
-   Veja [Instalar o SQL Server 2016 por meio do Prompt de Comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instalar o SQL Server 2016](../../database-engine/install-windows/install-sql-server.md)   
 [Instalar o SQL Server 2016 do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)  
  
  

