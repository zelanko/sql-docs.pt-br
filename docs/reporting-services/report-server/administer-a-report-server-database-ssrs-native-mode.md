---
title: Administrar um banco de dados de servidor de relatório (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], databases
- renaming databases
- report server database
- databases [Reporting Services], administering
- reportservertempdb
- reportserver database
ms.assetid: 97b2e1b5-3869-4766-97b9-9bf206b52262
caps.latest.revision: 63
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: ae7cd7716186c0bf6e03623f4c8a8f5665c2d4a7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33028513"
---
# <a name="administer-a-report-server-database-ssrs-native-mode"></a>Administrar um banco de dados de servidor de relatório (modo nativo do SSRS)
  Uma implantação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa dois bancos de dados relacionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenamento interno. Por padrão, os bancos de dados são nomeados como ReportServer e ReportServerTempdb. O ReportServerTempdb é criado com o banco de dados primário do servidor de relatórios e é usado para armazenar dados temporários, informações de sessão e relatórios em cache.  
  
 No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], as tarefas de administração de banco de dados incluem o backup e a restauração dos bancos de dados do servidor de relatórios e o gerenciamento das chaves de criptografia usadas para criptografar e descriptografar dados confidenciais.  
  
 Para administrar os bancos de dados do servidor de relatório, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece uma variedade de ferramentas.  
  
-   Para fazer backup e restaurar, mover ou recuperar um banco de dados do servidor de relatório, use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], os comandos [!INCLUDE[tsql](../../includes/tsql-md.md)] ou os utilitários de prompt de comando de banco de dados. Para obter instruções, consulte [Movendo os bancos de dados do servidor de relatório para outro computador &#40;modo nativo do SSRS&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md) nos Manuais Online do SQL Server.  
  
-   Para copiar o conteúdo do banco de dados existente em outro banco de dados do servidor de relatórios, anexe uma cópia de um banco de dados do servidor de relatórios e use-a com uma instância diferente do servidor de relatórios. Se preferir, crie e execute um script que usa chamadas SOAP para recriar o conteúdo do servidor de relatórios em um novo banco de dados. Você pode usar o utilitário **rs** para executar o script.  
  
-   Para gerenciar conexões entre o servidor de relatórios e o banco de dados do servidor de relatórios e para descobrir qual banco de dados é usado para uma instância específica do servidor de relatórios, use a página Instalação do Banco de Dados da ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para saber mais sobre a conexão do servidor de relatório para o banco de dados do servidor de relatório, consulte [Configurar uma conexão de banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
## <a name="sql-server-login-and-database-permissions"></a>Permissões de logon e de banco de dados do SQL Server  
 Os bancos de dados do servidor de relatórios são usados internamente pelo servidor de relatórios. As conexões com qualquer banco de dados são feitas pelo serviço Servidor de relatórios. Use a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para configurar a conexão do servidor de relatório com o banco de dados do servidor de relatório.  
  
 As credenciais para a conexão do servidor de relatório com o banco de dados podem ser a conta de serviço, uma conta de usuário local ou de domínio do Windows ou um usuário do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Você deve escolher uma conta existente para a conexão; o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não cria contas para você.  
  
 Um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o banco de dados do servidor de relatório é criado automaticamente para a conta especificada.  
  
 As permissões para o banco de dados também são configuradas automaticamente. A ferramenta Configuração do Reporting Services atribuirá o usuário da conta ou do banco de dados às funções **Public** e **RSExecRole** para os bancos de dados do servidor de relatório. A função **RSExecRole** fornece permissões para acessar as tabelas do banco de dados e para executar os procedimentos armazenados. A função **RSExecRole** é criada em master e msdb quando o banco de dados do servidor de relatório é criado. A função **RSExecRole** é um membro da função **db_owner** para os bancos de dados do servidor de relatório, permitindo que o servidor de relatório atualize seu próprio esquema para dar suporte ao processo de atualização automática.  
  
## <a name="naming-conventions-for-the-report-server-databases"></a>Convenções de nomenclatura para os bancos de dados do servidor de relatórios  
 Ao criar o banco de dados primário, o nome do banco de dados deve seguir as regras especificadas para [Identificadores de Banco de Dados](../../relational-databases/databases/database-identifiers.md). O nome do banco de dados temporário sempre usa o mesmo nome do banco de dados primário do servidor de relatórios, mas com um sufixo Tempdb. Você não pode escolher um nome diferente para o banco de dados temporário.  
  
 A renomeação de um banco de dados do servidor de relatórios não tem suporte porque os bancos de dados do servidor de relatórios são considerados como componentes internos. A renomeação dos bancos de dados do servidor de relatórios gera erros. Especificamente, se você renomear o banco de dados primário, uma mensagem de erro explicará que os nomes de banco de dados estão fora de sincronização. Se você renomear o banco de dados ReportServerTempdb, o seguinte erro interno ocorrerá posteriormente ao executar relatórios:  
  
 "Um erro interno ocorreu no servidor de relatórios. Consulte o log de erros para obter mais detalhes. (rsInternalError)  
  
 Nome de objeto inválido 'ReportServerTempDB.dbo.PersistedStream'."  
  
 Este erro ocorre porque o nome ReportServerTempdb é armazenado internamente e usado pelos procedimentos armazenados para executar operações internas. A renomeação do banco de dados temporário impede o funcionamento correto dos procedimentos armazenados.  
  
## <a name="enabling-snapshot-isolation-on-the-report-server-database"></a>Habilitando o isolamento de instantâneo no banco de dados do servidor de relatórios  
 Você não pode habilitar o isolamento de instantâneo no banco de dados do servidor de relatórios. Se o isolamento de instantâneo for ativado, o seguinte erro aparecerá: “O relatório selecionado não está pronto para exibição. O relatório ainda está sendo renderizado ou um instantâneo de relatório não está disponível.”  
  
 Caso não tenha habilitado o isolamento de instantâneo intencionalmente, o atributo pode ter sido definido por outro aplicativo ou o **modelo** de banco de dados pode ter habilitado o isolamento de instantâneo, fazendo com que todos os novos bancos de dados herdem a configuração.  
  
 Para desativar o isolamento de instantâneo no banco de dados do servidor de relatórios, inicie o Management Studio, abra uma nova janela de consulta, cole e, em seguida, execute o seguinte script:  
  
```  
ALTER DATABASE ReportServer  
SET ALLOW_SNAPSHOT_ISOLATION OFF  
ALTER DATABASE ReportServerTempdb  
SET ALLOW_SNAPSHOT_ISOLATION OFF  
ALTER DATABASE ReportServer  
SET READ_COMMITTED_SNAPSHOT OFF  
ALTER DATABASE ReportServerTempDb  
SET READ_COMMITTED_SNAPSHOT OFF  
```  
  
## <a name="about-database-versions"></a>Sobre as versões de banco de dados  
 No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], não há informações explícitas sobre a versão do banco de dados disponíveis. No entanto, como as versões de banco de dados sempre são sincronizados com as versões de produto, você pode usar as informações de versão do produto para saber quando a versão de banco de dados foi alterada. As informações de versão do produto do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] são indicadas pelas informações de versão do arquivo exibidas nos arquivos de log, nos cabeçalhos de todas as chamadas SOAP e ao conectar-se à URL do servidor de relatório (por exemplo, ao abrir um navegador em `http://localhost/reportserver`).  
  
## <a name="see-also"></a>Consulte Também  
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Criar um banco de dados de servidor de relatório do modo nativo &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Configurar a conta de serviço do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configurar uma conexão de banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Criar um banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)   
 [Operações de backup e restauração do Reporting Services](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md)   
 [Banco de dados do servidor de relatório &#40;modo nativo do SSRS&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
 [Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Armazenar dados criptografados do servidor de relatório &#40;Configuration Manager do SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Configurar e gerenciar chaves de criptografia &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
