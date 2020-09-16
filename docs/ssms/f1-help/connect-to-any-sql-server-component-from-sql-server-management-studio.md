---
description: Conectar a qualquer componente do SQL Server a partir do SQL Server Management Studio
title: Conectar-se a qualquer componente do SQL Server
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], SQL Server Management Studio
- saving connections
- components [SQL Server], connections
- SQL Server Management Studio [SQL Server], connections
ms.assetid: 5eeb41bd-b25b-4d3b-a005-a7d9e4b5978e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 8f89371787c66271d8298beed886b04b2b4aade1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497413"
---
# <a name="connect-to-any-sql-server-component-from-sql-server-management-studio"></a>Conectar a qualquer componente do SQL Server a partir do SQL Server Management Studio

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece funcionalidade para gerenciar todos os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para se conectar a:  
  
-   Uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)].  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)].  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
Apesar de o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] permitir que você trabalhe com consultas sem primeiro estabelecer uma conexão com uma fonte de dados, a maioria das outras tarefas requer uma conexão. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] fornece a caixa de diálogo **Conectar ao Servidor** para configurar propriedades de conexão com componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] é iniciado, a caixa de diálogo **Conectar ao Servidor** é exibida e solicita a conexão com um servidor. A caixa de diálogo **Conectar ao Servidor** retém as configurações de conexão da última vez que foi utilizada.  
  
> [!NOTE]  
> Esse recurso pode ser desativado de forma que nenhuma conexão seja iniciada automaticamente. Para obter mais informações, consulte [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
## <a name="saving-connections"></a>salvando conexões  
Você pode salvar conexões com servidores específicos em Servidores Registrados ou pode salvar conexões em projetos com o Gerenciador de Soluções.  
  
### <a name="saving-connections-in-registered-servers"></a>Salvando conexões em Servidores Registrados  
Ao registrar um servidor, o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] salva as informações de conexão em Servidores Registrados. Para se conectar a um servidor registrado, faça uma seleção dupla no nome do servidor em Servidores Registrados. O Pesquisador de Objetos abre uma conexão com o servidor.  
  
### <a name="saving-connections-in-solution-explorer"></a>Salvando conexões no Gerenciador de Soluções  
O Gerenciador de Soluções permite o armazenamento de consultas relacionadas, scripts, conexões e outras informações associadas em um projeto. Cada projeto de script contém um nó denominado **Conexões**, no qual você pode salvar uma ou mais conexões. Para adicionar uma conexão, selecione **Conexões** com o botão direito do mouse e escolha **Nova Conexão**. Para acessar uma conexão salva, expanda **Conexões** e faça uma seleção dupla na conexão. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] abre uma janela de consulta associada àquela conexão. Quando salvos, os scripts retêm sua associação com uma conexão específica.  
  
## <a name="see-also"></a>Consulte Também  
[Usar o SQL Server Management Studio](../../ssms/use-sql-server-management-studio.md)  
[Pesquisador de Objetos](../../ssms/object/object-explorer.md)  
  
