---
title: Instalar o Mecanismo de Banco de Dados do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], installing
ms.assetid: d0876e7f-aa52-4dd7-bd5c-029e2ffded5f
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e50fd6037b10008029d5373348605d11726b6199
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70148042"
---
# <a name="install-sql-server-database-engine"></a>Instalar o Mecanismo de Banco de Dados do SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

## <a name="overview"></a>Visão geral
O componente [!INCLUDE[ssDE](../../includes/ssde-md.md)] do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é o principal serviço para armazenamento, processamento e proteção de dados. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] fornece acesso controlado e processamento rápido de transações para atender aos requisitos dos mais exigentes aplicativos de consumo de dados em sua empresa.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a até 50 instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)] em um único computador. Para criar uma instalação típica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Instalar o SQL Server por meio do Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
>[!IMPORTANT]
>Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.  

## <a name="features"></a>Recursos
Os seguintes recursos são instalados quando você seleciona o **Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** na página Componentes a Serem Instalados do Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [Replicação do SQL Server](../../relational-databases/replication/sql-server-replication.md) – é um componente opcional  

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions" 
-   [Serviços de Machine Learning](../../advanced-analytics/install/sql-machine-learning-services-windows-install.md) (R e Python) e [Extensões de Idioma](../..//language-extensions/install/install-sql-server-language-extensions-on-windows.md) (Java) – componente opcional
::: moniker-end

::: monikerRange=">=sql-server-2017 <=sql-server-2017||=sqlallproducts-allversions"
-   [Serviços de Machine Learning (no banco de dados)](../../advanced-analytics/install/sql-machine-learning-services-windows-install.md)(R e Python) – componente opcional
::: moniker-end

::: monikerRange=">=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions"
-   [Serviços R (no banco de dados) ](../../advanced-analytics/install/sql-r-services-windows-install.md) – componente opcional
::: moniker-end

-   Pesquisa de Texto Completo - é um componente opcional  
  
-   Data Quality Services – é um componente opcional  
  
    > [!NOTE]  
    >  Nesta versão, se você marcar a caixa de seleção **Data Quality Services** na instalação, o servidor DQS (Data Quality Services) não será instalado. Será necessário executar etapas adicionais pós-instalação para instalar o servidor DQS. Para obter mais informações, consulte [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  
    
- [Serviço de Consulta PolyBase para Dados Externos](../../relational-databases/polybase/polybase-guide.md) – é um componente opcional. No SQL Server 2019 em diante, o conector do Java para fontes de dados HDFS também está disponível.

  
 Os seguintes recursos adicionais são opções para muitos cenários de usuário típicos:  
  
-   Cliente Data Quality
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]
-   Componentes de conectividade
-   Modelos de programação
-   Ferramentas de gerenciamento
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]
-   Componentes de documentação  
  

> [!NOTE]  
>  Por padrão, os bancos de dados de exemplo e o código de exemplo não são instalados como parte da instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para instalar bancos de dados de exemplo e o código de exemplo, consulte [Exemplos do Microsoft SQL Server](../../sample/microsoft-sql-server-samples.md). Consulte exemplos mais antigos no [CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843).  

  
## <a name="see-also"></a>Confira também  
 [Edições e recursos com suporte do SQL Server 2017](~/sql-server/editions-and-components-of-sql-server-2017.md)   
 [Planejando uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Soluções de alta disponibilidade &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [Fazer Upgrade do SQL Server Usando o Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  
