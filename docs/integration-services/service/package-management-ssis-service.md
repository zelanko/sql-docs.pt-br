---
title: Gerenciamento de Pacotes (Serviço SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: service
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.dtsserver.importpackage.f1
- sql13.dts.dtsserver.exportpackage.f1
helpviewer_keywords:
- SQL Server Integration Services packages, managing
- packages [Integration Services], managing
- Integration Services packages, managing
- storing packages
- Stored Packages folder
- current packages
- Running Packages folder
- status information [Integration Services]
- SSIS packages, managing
- storage [Integration Services]
- monitoring [Integration Services], packages
- Integration Services service, package management
- services [Integration Services], package management
ms.assetid: 0261ed9e-3b01-4e37-a9d4-d039c41029b6
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0ef5f56d09d34fa2688fe46fdf6d7983af4e9e1f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="package-management-ssis-service"></a>Gerenciamento de pacotes (serviço SSIS)
  O gerenciamento de pacotes inclui monitoramento, gerenciamento, importação e exportação de pacotes.  
 
 ## <a name="package-store"></a>Repositório de pacotes  
 O [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece duas pastas de nível superior para acessar os pacotes: 
 - **Pacotes em Execução** 
 - **Pacotes Armazenados**

 A pasta **Pacotes em Execução** lista os pacotes que estão sendo executados atualmente no servidor. A pasta **Pacotes Armazenados** lista os pacotes que são salvos no armazenamento de pacotes. Esses são os únicos pacotes que o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] gerencia. O repositório de pacotes pode consistir em um ou em ambos, o banco de dados msdb e as pastas do sistema de arquivos, listados no arquivo de configuração de serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . O arquivo de configuração especifica o msdb e as pastas do sistema de arquivos a serem gerenciados. Você também pode ter pacotes armazenados em outros lugares no sistema de arquivos que não são gerenciados pelo serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Os pacotes salvos no msdb são armazenados em uma tabela chamada sysssispackages. Quando você salva pacotes no msdb, pode agrupá-los em pastas lógicas. O uso de pastas lógicas pode ajudar a organizar os pacotes por finalidade ou filtrar os pacotes na tabela sysssispackages. Crie novas pastas lógicas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Por padrão, qualquer pasta lógica que você adicionar ao msdb será automaticamente incluída no repositório de pacotes.  
  
 As pastas lógicas criadas são representadas como linhas na tabela sysssispackagefolders no msdb. As colunas folderid e parentfolderid no sysssispackagefolders definem a hierarquia de pastas. As pastas raiz lógicas do msdb são as linhas do sysssispackagefolders com valores nulos na coluna parentfolderid. Para obter mais informações, consulte [sysssispackages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysssispackages-transact-sql.md) e [sysssispackagefolders (Transact-SQL&)](../../relational-databases/system-tables/sysssispackagefolders-transact-sql.md).  
  
 Ao abrir o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e se conectar ao [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você verá as pastas do msdb gerenciadas pelo serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] listadas na pasta Pacotes Armazenados. Se o arquivo de configuração especificar pastas do sistema do arquivo raiz, a pasta Pacotes Armazenados também listará pacotes salvos no sistema de arquivos nessas pastas e em todas as subpastas.  
  
 Você pode armazenar pacotes em qualquer pasta do sistema de arquivos, mas eles não serão listados nas subpastas da pasta **Pacotes Armazenados** , a menos que você adicione a pasta à lista de pastas no arquivo de configuração para armazenamento de arquivos. Para obter mais informações sobre esse arquivo de configuração, veja [Serviço Integration Services &#40;Serviço SSIS&#41;](../../integration-services/service/integration-services-service-ssis-service.md).  
  
 A pasta **Pacotes em Execução** não contém nenhuma subpasta e não é extensível.  
  
 Por padrão, a pasta **Pacotes Armazenados** contém duas pastas: **Sistema de Arquivos** e **MSDB**. A pasta **Sistema de Arquivos** lista os pacotes salvos no sistema de arquivos. O local desses arquivos é especificado no arquivo de configuração do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . A pasta padrão é a pasta Pacotes, localizada em %Arquivos de Programas%\Microsoft SQL Server\100\DTS. A pasta **MSDB** lista os pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que foram salvos no banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do msdb no servidor. A tabela sysssispackages contém os pacotes salvos no msdb.  
  
 Para exibir a lista de pacotes no repositório de pacotes, você precisa abrir o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e conectar-se ao [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="monitor-running-packages"></a>Monitorar os pacotes em execução  
 A pasta **Pacotes em Execução** lista os pacotes que estão sendo executados atualmente. Para visualizar as informações sobre pacotes existentes na página **Resumo** do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique na pasta **Pacotes em Execução** . Informações como a duração da execução dos pacotes em execução são listadas na página **Resumo** . Opcionalmente, atualize a pasta para exibir as informações mais recentes.  
  
 Para visualizar as informações sobre um único pacote em execução na página **Resumo** , clique no pacote. A página **Resumo** exibe informações como a versão e a descrição do pacote.  
  
Interrompa um pacote em execução na pasta **Pacotes em Execução** clicando com o botão direito do mouse no pacote e, em seguida, clicando em **Parar**.  
  
## <a name="view-packages-in-ssms"></a>Exibir pacotes no SSMS
    
 Este procedimento descreve como se conectar ao [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e exibir uma lista dos pacotes gerenciados pelo serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
### <a name="to-connect-to-integration-services"></a>Para se conectar ao Integration Services  
  
1.  Clique em **Iniciar**, aponte para **Todos os Programas**, aponte para **Microsoft SQL Server**e clique em **SQL Server Management Studio**.  
  
2.  Na caixa de diálogo **Conectar ao Servidor** , selecione **Integration Services** na lista **Tipo de servidor** , forneça um nome de servidor na caixa **Nome do servidor** e clique em **Conectar**.  
  
    > [!IMPORTANT]  
    >  Se você não consegue se conectar ao [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], provavelmente o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não está sendo executado. Para saber o status do serviço, clique em **Iniciar**, aponte para **Todos os Programas**, aponte para **Microsoft SQL Server**, aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**. No painel esquerdo, clique em **Serviços do SQL Server**. No painel direito, localize o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Inicie o serviço se ainda não estiver em execução.  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é aberto. Por padrão, a janela do Pesquisador de Objetos é aberta e posicionada no canto inferior esquerdo do estúdio. Se o Pesquisador de Objetos não for aberto, clique em **Pesquisador de Objetos** no menu **Exibir** .  
  
### <a name="to-view-the-packages-that-integration-services-service-manages"></a>Para visualizar os pacotes gerenciados pelo serviço Integration Services  
  
1.  No Pesquisador de Objetos, expanda a pasta Pacotes Armazenados.  
  
2.  Expanda as subpastas Pacotes Armazenados para exibir os pacotes.  

## <a name="import-and-export-packages"></a>Importar e exportar pacotes
 
 Os pacotes podem ser salvos na tabela sysssispackages no banco de dados msdb do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou no sistema de arquivos.  
  
 O repositório de pacotes, que é o armazenamento lógico que o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] monitora e gerencia, pode incluir o banco de dados msdb e as pastas do sistema de arquivos especificadas no arquivo de configuração para o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Você pode importar e exportar pacotes entre os seguintes tipos de armazenamento:  
  
-   Pastas do sistema de arquivos em qualquer lugar do sistema de arquivos.  
  
-   Pastas no repositório de pacotes SSIS. As duas pastas padrão são nomeadas Sistema de Arquivos e MSDB.  
  
-   O banco de dados msdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] permite importar e exportar pacotes e, ao fazer isso, alterar o formato de armazenamento e o local de pacotes. Usando os recursos de importação e exportação, você pode adicionar pacotes ao sistema de arquivos, ao repositório de pacotes ou ao banco de dados msdb e copiar pacotes de um formato de armazenamento para outro. Por exemplo, os pacotes salvos no msdb podem ser copiados para o sistema de arquivos e vice-versa.  
  
 Você também pode copiar um pacote em um formato diferente por meio do utilitário do prompt de comando **dtutil** (dtutil.exe). Para obter mais informações, consulte [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
 Você pode importar ou exportar um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] de ou para os seguintes locais:  
  
-   É possível importar um pacote armazenado em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no sistema de arquivos ou no repositório de pacotes [!INCLUDE[ssIS](../../includes/ssis-md.md)] . O pacote importado é salvo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou em uma pasta do armazenamento de pacotes [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
-   É possível exportar um pacote armazenado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no sistema de arquivos ou no Repositório de Pacotes [!INCLUDE[ssIS](../../includes/ssis-md.md)] para outro formato e outro local de armazenamento.  
  
 No entanto, existem algumas restrições sobre a importação e a exportação de pacotes entre diferentes versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Em uma instância do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], você pode importar pacotes de uma instância do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], mas não é possível exportar pacotes para uma instância do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
-   Em uma instância do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], você não pode importar pacotes de, ou exportar pacotes para, uma instância do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
 Os procedimentos a seguir descrevem como usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para importar ou exportar um pacote.  
  
### <a name="to-import-a-package-by-using-sql-server-management-studio"></a>Para importar um pacote usando o SQL Server Management Studio  
  
1.  Clique em **Iniciar**, aponte para **Microsoft** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e clique em **SQL Server Management Studio**.  
  
2.  Na caixa de diálogo **Conectar ao Servidor**, defina as seguintes opções:  
  
    -   Na caixa **Tipo de servidor** , selecione **Integration Services**.  
  
    -   Na caixa **Nome do servidor**, forneça um nome do servidor ou clique em **\<Browse for more…>** e localize o servidor a ser usado.  
  
3.  Se o Pesquisador de Objetos não estiver aberto, clique em **Pesquisador de Objetos** no menu **Exibir**.  
  
4.  No Pesquisador de Objetos, expanda a pasta **Pacotes Armazenados** .  
  
5.  Expanda as subpastas para localizar a pasta para a qual você deseja importar um pacote.  
  
6.  Clique com o botão direito do mouse na pasta e clique em **Importar Pacote**. Em seguida, proceda de uma das seguintes maneiras:  
  
    -   Para importar de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selecione a opção **SQL Server** e depois especifique o servidor e selecione o modo de autenticação. Se você selecionar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , forneça um nome de usuário e uma senha.  
  
         Clique no botão Procurar **(...)**, selecione o pacote para importar e clique em **OK.**  
  
    -   Para importar do sistema de arquivos, selecione a opção **Sistema de arquivos** .  
  
         Clique no botão Procurar **(...)**, selecione o pacote para importar e então clique em **Abrir.**  
  
    -   Para importar usando o Repositório de Pacotes [!INCLUDE[ssIS](../../includes/ssis-md.md)] , selecione a opção **Repositório de Pacotes SSIS** e especifique o servidor.  
  
         Clique no botão Procurar **(...)**, selecione o pacote para importar e clique em **OK.**  
  
7.  Opcionalmente, atualize o nome de pacote.  
  
8.  Para atualizar o nível de proteção do pacote, clique no botão Procurar **(...)** e, na caixa de diálogo **Nível de Proteção do Pacote** , escolha um nível de proteção diferente. Se a opção **Criptografar dados confidenciais com senhas** ou **Criptografar todos os dados com senhas** for selecionada, digite e confirme uma senha.  
  
9. Clique em **OK** para concluir a importação.  
  
### <a name="to-export-a-package-by-using-sql-server-management-studio"></a>Para exportar um pacote usando o SQL Server Management Studio  
  
1.  Clique em **Iniciar**, aponte para **Microsoft** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e clique em **SQL Server Management Studio**.  
  
2.  Na caixa de diálogo **Conectar ao Servidor** , defina as seguintes opções:  
  
    -   Na caixa **Tipo de servidor** , selecione **Integration Services**.  
  
    -   Na caixa **Nome do servidor**, forneça um nome do servidor ou clique em **\<Browse for more…>** e localize o servidor a ser usado.  
  
3.  Se o Pesquisador de Objetos não estiver aberto, clique em **Pesquisador de Objetos** no menu **Exibir**.  
  
4.  No Pesquisador de Objetos, expanda a pasta **Pacotes Armazenados**.  
  
5.  Expanda as subpastas para localizar o pacote que deseja exportar.  
  
6.  Clique com o botão direito do mouse no pacote, clique em **Exportar**e depois execute uma das seguintes tarefas:  
  
    -   Para exportar para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selecione a opção **SQL Server** e depois especifique o servidor e selecione o modo de autenticação. Se você selecionar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , forneça um nome de usuário e uma senha.  
  
         Clique no botão Procurar **(...)** e expanda a pasta do **Pacotes SSIS** para localizar a pasta na qual deseja salvar o pacote. Opcionalmente, atualize o nome padrão do pacote e então clique em **OK**.  
  
    -   Para exportar para o sistema de arquivos, selecione a opção **Sistema de Arquivos** .  
  
         Clique no botão Procurar **(...)** para localizar a pasta para a qual deseja exportar o pacote, digite o nome do arquivo do pacote e clique em **Salvar**.  
  
    -   Para exportar para o repositório de pacotes [!INCLUDE[ssIS](../../includes/ssis-md.md)] , selecione a opção **Repositório de Pacotes SISS** e especifique o servidor.  
  
         Clique no botão Procurar **(...)**, expanda a pasta dos **Pacotes SSIS** e selecione a pasta na qual deseja salvar o pacote. Opcionalmente, digite um novo nome para o pacote na caixa de texto **Nome do Pacote** . [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  Para atualizar o nível de proteção do pacote, clique no botão Procurar **(...)** e, na caixa de diálogo **Nível de Proteção do Pacote**, escolha um nível de proteção diferente. Se a opção **Criptografar dados confidenciais com senhas** ou **Criptografar todos os dados com senhas** for selecionada, digite e confirme uma senha.  
  
8.  Clique em **OK** para completar a exportação.  

## <a name="import-package-dialog-box-ui-reference"></a>Referência da interface do usuário da caixa de diálogo Importar Pacote
  Use a caixa de diálogo **Importar Pacote** , disponível no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], para importar um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e para definir ou modificar o nível de proteção do pacote.  
  
### <a name="options"></a>Opções  
 **Local do pacote**  
 Selecione o tipo de local de armazenamento para importar o pacote. As seguintes opções estão disponíveis:  
  
 **SQL Server**  
  
 **Sistema de Arquivos**  
  
 **Armazenamento de Pacotes SSIS**  
  
 **Servidor**  
 Digite um nome de servidor ou selecione um servidor na lista.  
  
 **Autenticação**  
 Selecione a Autenticação do Windows ou a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Essa opção estará disponível apenas se o local de armazenamento for o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Sempre que for possível, use a Autenticação do Windows.  
  
 **Tipo de autenticação**  
 Selecione um tipo de autenticação.  
  
 **User name**  
 Se estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , forneça um nome de usuário.  
  
 **Senha**  
 Se estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , forneça uma senha.  
  
 **Caminho do pacote**  
 Digite o nome do pacote ou clique no botão Procurar **(…)** e localize o pacote.  
  
 **Nome do pacote**  
 Opcionalmente, renomeie o pacote. O nome padrão é o nome do pacote a ser importado.  
  
 **Nível de proteção**  
 Clique no botão Procurar **(…)** e, na caixa de diálogo **Nível de Proteção do Pacote** , atualize o nível de proteção. Para obter mais informações, consulte [Caixa de diálogo Nível de Proteção do Pacote e do Projeto](../../integration-services/security/access-control-for-sensitive-data-in-packages.md#protection_dialog).  

## <a name="export-package-dialog-box-ui-reference"></a>Referência da interface do usuário da caixa de diálogo Exportar Pacote
  Use a caixa de diálogo **Exportar Pacote** , disponível no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], para exportar um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para um local diferente e, opcionalmente, modificar o nível de proteção do pacote.  
  
### <a name="options"></a>Opções  
 **Local do pacote**  
 Selecione o tipo armazenamento para exportar o pacote. As seguintes opções estão disponíveis:  
  
 **SQL Server**  
  
 **Sistema de Arquivos**  
  
 **Armazenamento de Pacotes SSIS**  
  
 **Servidor**  
 Digite um nome de servidor ou selecione um servidor na lista.  
  
 **Autenticação**  
 Selecione a Autenticação do Windows ou a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Essa opção estará disponível apenas se o local de armazenamento for o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Sempre que for possível, use a Autenticação do Windows.  
  
 **Tipo de autenticação**  
 Selecione um tipo de autenticação.  
  
 **User name**  
 Se estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , forneça um nome de usuário.  
  
 **Senha**  
 Se estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , forneça uma senha.  
  
 **Caminho do pacote**  
 Digite o caminho do pacote ou clique no botão Procurar **(…)** e localize a pasta na qual o pacote será armazenado.  
  
 **Nível de proteção**  
 Clique no botão Procurar **(…)** e atualize o nível de proteção na caixa de diálogo **Nível de Proteção do Pacote** . Para obter mais informações, consulte [Caixa de diálogo Nível de Proteção do Pacote e do Projeto](../../integration-services/security/access-control-for-sensitive-data-in-packages.md#protection_dialog).  

## <a name="back-up-and-restore-packages"></a>Fazer backup e restaurar pacotes
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacotes podem ser salvos no sistema de arquivos ou no msdb, um banco de dados do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os pacotes salvos no msdb podem ter backup e serem restaurados usando recursos de backup e restauração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para obter mais informações sobre como fazer backups e restauração do banco de dados msdb, clique em um dos seguintes tópicos:  
  
-   [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
-   [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui o utilitário de prompt de comando **dtutil** (dtutil.exec), que pode ser usado para gerenciar pacotes. Para obter mais informações, consulte [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
### <a name="configuration-files"></a>Arquivos de configuração  
 Qualquer arquivo de configuração incluído nos pacotes é armazenado no sistema de arquivos. Esses arquivos não são salvos ao fazer o backup do banco de dados msdb; portanto, você deve verificar se o backup é realizado regularmente em todos os arquivos de configuração como parte de seu plano para proteger os pacotes salvos no msdb. Para incluir as configurações no backup do banco de dados msdb, você deve considerar o uso do tipo de configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , em vez das configurações baseadas em arquivos.  
  
### <a name="packages-stored-in-the-file-system"></a>Pacotes armazenados no sistema de arquivos  
 O backup de pacotes salvos no sistema de arquivos deveria ser incluído no plano de backup do sistema de arquivos do servidor. O arquivo de configuração do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , com o nome padrão de MsDtsSrvr.ini.xml, lista no servidor as pastas monitoradas pelo serviço. Você deve verificar se essas pastas têm backup. Além disso, os pacotes podem ser armazenados em outras pastas no servidor e você deve verificar se essas pastas estão incluídas no backup.  

## <a name="see-also"></a>Consulte Também  
 [Serviço Integration Services &#40;Serviço SSIS&#41;](../../integration-services/service/integration-services-service-ssis-service.md)  
  
  
