---
title: Ajuda do SQL Server Configuration Manager
ms.custom: seo-lt-2019
ms.date: 02/01/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Configuration Manager, help
ms.assetid: 6e909911-39a6-469b-b22a-3afdfd08a30b
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 8ade0d0e0944b01005866fc5c38e50ce45fae0fd
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75306951"
---
# <a name="sql-server-configuration-manager-help"></a>Ajuda do SQL Server Configuration Manager
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para configurar os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e configurar a conectividade de rede. Para criar ou gerenciar objetos de banco de dados, configurar a segurança e escrever consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] , use o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações sobre o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], consulte os Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

 > [!TIP]
 > Se você precisar configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Linux, use a ferramenta **mssql-conf**. Para obter mais informações, confira [Configurar o SQL Server em Linux com a ferramenta mssql-conf](../../linux/sql-server-linux-configure-mssql-conf.md).

 Esta seção contém os tópicos da Ajuda F1 para as caixas de diálogo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
> [!NOTE]
>  O Configuration Manager [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode configurar versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores à [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
## <a name="services"></a>Serviços  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager gerencia serviços relacionados ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Embora muitas dessas tarefas possam ser realizadas com a caixa de diálogo Serviços do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, é importante observar que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager executa operações adicionais nos serviços que gerencia, como aplicar as permissões corretas quando a conta do serviço é alterada. O uso da caixa de diálogo normal Serviços do Windows para configurar quaisquer serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderia prejudicar o funcionamento do serviço.  
  
 Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para as seguintes tarefas de serviços:  
  
-   Iníciar, parar e pausar serviços  
  
-   Configurar serviços para iniciar automática ou manualmente, desabilitar os serviços ou alterar outras configurações de serviço  
  
-   Alterar as senhas das contas usadas pelos serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando sinalizadores de rastreamento (parâmetros de linha de comando)  
  
-   Exibir as propriedades dos serviços  
  
## <a name="sql-server-network-configuration"></a>Configuração de rede do SQL Server  
 Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para as seguintes tarefas relacionadas aos serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neste computador:  
  
-   Habilitar ou desabilitar um protocolo de rede do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Configurar um protocolo de rede do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
> [!NOTE]  
>  Para obter um breve tutorial sobre como configurar protocolos e conectar-se ao [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], confira [: Introdução ao Mecanismo de Banco de Dados.](../../relational-databases/tutorial-getting-started-with-the-database-engine.md)  
  
## <a name="sql-server-native-client-configuration"></a>Configuração do SQL Server Native Client  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conectam ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a biblioteca de rede do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para as seguintes tarefas relacionadas aos aplicativos clientes neste computador:  
  
-   Para aplicativos cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neste computador, especifique a ordem dos protocolos, ao conectar instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Configure protocolos de conexão de cliente.  
  
-   Para aplicativos cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , crie aliases para instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], para que os clientes possam se conectar usando uma cadeia de conexão padrão.  
  
 Para obter mais informações sobre cada uma dessas tarefas, consulte a ajuda F1 de cada tarefa.  
  
#### <a name="to-open-sql-server-configuration-manager"></a>Para abrir o SQL Server Configuration Manager  
  
-   No menu **Iniciar** , aponte para **Todos os Programas**, aponte para **Microsoft SQL Server** (versão), aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
  
 **Para acessar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager usando o [!INCLUDE[win8](../../includes/win8-md.md)]**  
  
 Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager é um snap-in do programa [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console (MMC) e não um programa autônomo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager não aparece como um aplicativo ao executar o [!INCLUDE[win8](../../includes/win8-md.md)]. Para abrir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no botão **Pesquisar**, em **Aplicativos**, digite **SQLServerManager12.msc** (para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) ou **SQLServerManager11.msc** (para [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) e pressione **Enter**.  
  

## <a name="see-also"></a>Consulte Também  
 [Serviços do SQL Server](../../tools/configuration-manager/sql-server-services.md)   
 [Configuração de rede do SQL Server](../../tools/configuration-manager/sql-server-network-configuration.md)   
 [Configuração do SQL Native Client 11.0](../../tools/configuration-manager/sql-native-client-11-0-configuration.md)   
 [Escolhendo um protocolo de rede](https://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)  
  
  
