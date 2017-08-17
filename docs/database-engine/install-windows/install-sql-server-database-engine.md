---
title: Instalar o Mecanismo de Banco de Dados do SQL Server | Microsoft Docs
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
- Database Engine [SQL Server], installing
ms.assetid: d0876e7f-aa52-4dd7-bd5c-029e2ffded5f
caps.latest.revision: 45
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 192549457850c9c24fd72ce3f205e0ddedfe1d12
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-database-engine"></a>Instalar o Mecanismo de Banco de Dados do SQL Server
  O componente [!INCLUDE[ssDE](../../includes/ssde-md.md)] do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é o principal serviço para armazenamento, processamento e proteção de dados. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] fornece acesso controlado e processamento rápido de transações para atender aos requisitos dos mais exigentes aplicativos de consumo de dados em sua empresa.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a até 50 instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)] em um único computador. Para criar uma instalação típica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Instalar o SQL Server 2016 por meio do Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
 **Importante** Para instalações locais, é necessário executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.  
  
 Os seguintes recursos são instalados quando você seleciona o **Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** na página Componentes a Serem Instalados do Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   Replicação - é um componente opcional  
  
-   Pesquisa de Texto Completo - é um componente opcional  
  
-   Data Quality Services – é um componente opcional  
  
    > [!NOTE]  
    >  Nesta versão, se você marcar a caixa de seleção **Data Quality Services** na instalação, o servidor DQS (Data Quality Services) não será instalado. Será necessário executar etapas adicionais pós-instalação para instalar o servidor DQS. Para obter mais informações, consulte [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  
  
 Os seguintes recursos adicionais são opções para muitos cenários de usuário típicos:  
  
-   Cliente Data Quality  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   Componentes de conectividade  
  
-   Modelos de programação  
  
-   Ferramentas de gerenciamento  
  
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
-   Componentes de documentação  
  
> [!NOTE]  
>  Por padrão, os bancos de dados de exemplo e o código de exemplo não são instalados como parte da instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para instalar bancos de dados e código de exemplo, veja o [site CodePlex](http://go.microsoft.com/fwlink/?LinkId=87843).  
  
## <a name="see-also"></a>Consulte também  
 [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [Edições e componentes do SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [Planejando uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Soluções de alta disponibilidade &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [Atualizar para o SQL Server 2016 usando o Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  

