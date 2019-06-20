---
title: Alterar o Assistente de banco de dados (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.changedatabase.F1
helpviewer_keywords:
- Change Database Wizard
- report server database, create
ms.assetid: 1a2e8d18-5997-482f-a9c1-87d99f7407b8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: bc07e94db985ce156fdd5cd59620c2e7fddc2d73
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66096665"
---
# <a name="change-database-wizard-ssrs-native-mode"></a>Assistente para Alterar Banco de Dados (modo nativo do SSRS)
  O Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece o Assistente para Alterar Banco de Dados que orienta o usuário nas etapas de criação de um novo banco de dados do servidor de relatório ou de seleção de um banco de dados do servidor de relatório existente a ser usado com a instância do servidor de relatório atual.  
  
 Se você selecionar um banco de dados do servidor de relatório de uma versão anterior, ele será atualizado para corresponder à versão da instância do servidor de relatório ao qual está conectado. Quando o serviço inicia, ele verifica a versão do banco de dados e o atualiza automaticamente para o esquema atual.  
  
 Para iniciar o assistente, clique em **Alterar Banco de Dados** na página Banco de Dados do Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter instruções sobre como iniciar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager, consulte [Reporting Services Configuration Manager &#40;nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
## <a name="options"></a>Opções  
 **Ação**  
 Selecione a tarefa que você deseja executar. Você pode criar um novo banco de dados no modo nativo ou integrado do SharePoint. Se preferir, você pode selecionar um banco de dados existente do servidor de relatório e usá-lo com a instância do servidor de relatório atual.  
  
 **Servidor de banco de dados**  
 Especifique o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] que hospeda o banco de dados do servidor de relatório. Não é possível usar uma instância nomeada ou padrão em um computador local ou remoto. Se você estiver se conectando a uma instância nomeada, digite o nome do servidor neste formato: \< *server*>\\<*instância*>.  
  
 Para se conectar à instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , use credenciais com permissão para efetuar logon no servidor e atualizar informações do banco de dados. O Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa suas credenciais atuais do Windows. Mas, se você não tiver um logon ou permissões de banco de dados, especifique um logon de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Não é possível especificar credenciais diferentes do Windows. Para conectar-se como um usuário diferente do Windows, faça logon como esse usuário e inicie o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Para se conectar a uma instância remota, primeiro você deve habilitar essa instância para conexões remotas. Por padrão, algumas versões e edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não habilitam conexões remotas. Para confirmar se conexões remotas são permitidas, use o Gerenciador de Configurações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e verifique se os protocolos TCP/IP e Pipes Nomeados estão habilitados. Se a instância remota também for uma instância nomeada, verifique se o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está habilitado e em execução no servidor de destino. O Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informa o número da porta usado pela instância nomeada para o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 **Backup de banco de dados**  
 Especifica o nome do banco de dados do servidor de relatório que armazena dados do servidor. É possível especificar um banco de dados existente ou criar um novo banco de dados.  
  
 As propriedades usadas para criar um novo banco de dados aparecem no Assistente quando você seleciona **Criar novo banco de dados** na página Ações. O Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] cria dois bancos de dados que são associados por nome: um banco de dados para conter dados estáticos e um banco de dados temporário para armazenar dados da sessão e de trabalho. Para obter mais informações, consulte [banco de dados de servidor de relatório &#40;modo nativo do SSRS&#41; ](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md) na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.  
  
 Você também pode escolher um banco de dados existente do servidor de relatório. O Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não filtra bancos de dados inválidos. Os bancos de dados válidos têm como base o esquema de banco de dados do servidor de relatório (não é possível selecionar um banco de dados que não tenha as tabelas, exibições ou procedimentos armazenados necessários). Se você escolher um banco de dados que foi criado para uma versão anterior do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], ele será atualizado para o formato atual.  
  
 **Idioma**  
 Este valor só é definido quando você cria um novo banco de dados do servidor de relatório.  
  
 Com esse valor, você especifica o idioma no qual são criadas definições e descrições de função. O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece um modelo de autorização baseada em função que inclui um conjunto de funções predefinidas. Essas funções são criadas uma única vez no idioma especificado. Os nomes e as descrições de função nunca aparecem em outros idiomas, mesmo que você se conecte ao servidor de relatório usando um navegador que tenha configurações de cultura ou idioma suportadas pelo servidor. O idioma especificado também determina o idioma usado para criar o nome da pasta Meus Relatórios e as pastas Usuários que fazem parte do recurso Meus Relatórios.  
  
 **Modo de servidor**  
 Um banco de dados do servidor de relatório dá suporte ao modo nativo ou ao modo integrado do SharePoint. Os modos são mutuamente exclusivos.  
  
 Se você estiver criando um novo banco de dados do servidor de relatório, deverá especificar um modo. O modo selecionado determina a estrutura do banco de dados do servidor de relatório e define a propriedade `SharePointIntegrated` do sistema de servidor de relatório como `true` ou `false`.  
  
 Se você selecionar outro banco de dados do servidor de relatório, o modo do banco de dados atual será exibido para que você saiba como o banco de dados atual é usado.  
  
 **Credenciais**  
 Especifica a conta pela qual o servidor de relatório se conecta ao banco de dados do servidor de relatório. Os valores válidos incluem a conta de serviço do serviço Web Servidor de Relatório, um logon de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definido na instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que está sendo utilizada para hospedar o servidor de relatório ou uma conta do Windows. Se você estiver usando uma conta do Windows, você pode especificar uma conta local (*\<computername >\\< nome de usuário\>*) se o servidor de relatório e o banco de dados estiverem no mesmo computador ou um usuário de domínio conta (*\<domínio >\\< nome de usuário\>*) se eles estiverem em computadores diferentes no mesmo domínio.  
  
 O servidor de relatório criará um logon de banco de dados e atribuirá permissões de banco de dados para a conta especificada.  
  
 O servidor de relatório não cria a própria conta. A conta especificada já deve existir e deve ser válida para sua configuração de implantação. Especificamente, se o banco de dados estiver em um computador remoto e você deseja usar uma conta do Windows, deverá especificar uma conta que tenha permissões de logon nesse computador.  
  
 Se o computador estiver em um domínio diferente ou não confiável, considere o uso de um logon de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações sobre como escolher uma conta, consulte [configurar uma Conexão de banco de dados do servidor de relatório &#40;Configuration Manager do SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
 **Resumo**  
 Verifique as configurações antes que a instalação configure a conexão.  
  
 **Progresso e conclusão**  
 Monitore o progresso de cada tarefa.  
  
## <a name="see-also"></a>Consulte também  
 [Banco de dados &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/database-ssrs-native-mode.md)   
 [Assistente para alterar credenciais &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/change-credentials-wizard-ssrs-native-mode.md)   
 [Criar um banco de dados de servidor de relatório do modo nativo &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Tópicos de Ajuda F1 do Configuration Manager do Reporting Services &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Configurar uma conexão de banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  
