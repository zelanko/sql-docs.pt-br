---
title: Conectar a qualquer componente do SQL Server do SSMS | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-f1
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], SQL Server Management Studio
- saving connections
- components [SQL Server], connections
- SQL Server Management Studio [SQL Server], connections
ms.assetid: 5eeb41bd-b25b-4d3b-a005-a7d9e4b5978e
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a30dd4d3eedea208255e02b6cbef6a842ad81906
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38981488"
---
# <a name="connect-to-any-sql-server-component-from-sql-server-management-studio"></a>Conectar a qualquer componente do SQL Server a partir do SQL Server Management Studio
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] fornece funcionalidade para gerenciar todos os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Use o [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] para se conectar a:  
  
-   Uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)].  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)].  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)].  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)].  
  
Apesar de o [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] permitir que você trabalhe com consultas sem primeiro estabelecer uma conexão com uma fonte de dados, a maioria das outras tarefas requer uma conexão. [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] fornece a caixa de diálogo **Conectar ao Servidor** para configurar propriedades de conexão com componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . Quando o [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] é iniciado, a caixa de diálogo **Conectar ao Servidor** é exibida e solicita a conexão com um servidor. A caixa de diálogo **Conectar ao Servidor** retém as configurações de conexão da última vez que foi utilizada.  
  
> [!NOTE]  
> Esse recurso pode ser desativado de forma que nenhuma conexão seja iniciada automaticamente. Para obter mais informações, consulte [Opções de inicialização do serviço Mecanismo de Banco de Dados](http://msdn.microsoft.com/d373298b-f6cf-458a-849d-7083ecb54ef5).  
  
## <a name="saving-connections"></a>salvando conexões  
Você pode salvar conexões com servidores específicos em Servidores Registrados ou pode salvar conexões em projetos com o Gerenciador de Soluções.  
  
### <a name="saving-connections-in-registered-servers"></a>Salvando conexões em Servidores Registrados  
Ao registrar um servidor, o [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] salva as informações de conexão em Servidores Registrados. Para conectar a um servidor registrado, clique duas vezes no nome do servidor em Servidores Registrados. O Pesquisador de Objetos abre uma conexão com o servidor.  
  
### <a name="saving-connections-in-solution-explorer"></a>Salvando conexões no Gerenciador de Soluções  
O Gerenciador de Soluções permite o armazenamento de consultas relacionadas, scripts, conexões e outras informações associadas em um projeto. Cada projeto de script contém um nó denominado **Conexões**, no qual você pode salvar uma ou mais conexões. Para adicionar uma conexão, clique com o botão direito do mouse em **Conexões**e clique em **Nova Conexão**. Para acessar uma conexão salva, expanda **Conexões** e clique duas vezes na conexão. [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] abre uma janela de consulta associada àquela conexão. Quando salvos, os scripts retêm sua associação com uma conexão específica.  
  
## <a name="see-also"></a>Consulte Também  
[Usar o SQL Server Management Studio](../../ssms/use-sql-server-management-studio.md)  
[Pesquisador de Objetos](../../ssms/object/object-explorer.md)  
  
