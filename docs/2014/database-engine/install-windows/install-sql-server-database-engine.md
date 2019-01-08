---
title: Sobre o mecanismo de banco de dados do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], installing
ms.assetid: d0876e7f-aa52-4dd7-bd5c-029e2ffded5f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6373f67d40b9da97f652f3bcb05b3414deab5c8d
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53370559"
---
# <a name="about-the-sql-server-database-engine"></a>Sobre o Mecanismo de Banco de Dados do SQL Server
  O componente [!INCLUDE[ssDE](../../includes/ssde-md.md)] do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é o principal serviço para armazenamento, processamento e proteção de dados. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] fornece acesso controlado e processamento rápido de transações para atender aos requisitos dos mais exigentes aplicativos de consumo de dados em sua empresa.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a até 50 instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)] em um único computador. Para criar um típico [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalação, consulte [instalar o SQL Server 2014 do Assistente de instalação do &#40;instalação&#41;](install-sql-server-from-the-installation-wizard-setup.md).  
  
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
>  Por padrão, os bancos de dados de exemplo e o código de exemplo não são instalados como parte da instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para instalar bancos de dados e código de exemplo, veja o [site CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843).  
  
## <a name="see-also"></a>Consulte também  
 [Recursos com suporte nas edições do SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Edições e componentes do SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [Planejando uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Soluções de alta disponibilidade &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [Atualizar para o SQL Server 2014 usando o Assistente de instalação &#40;programa de instalação&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  
