---
title: Fazer upgrade do Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 9c3543f3-3eb9-455d-a9bf-f17e9506ad21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1d60defaef135a87669b9f87257e0856f0c1dca2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079666"
---
# <a name="upgrade-master-data-services"></a>Atualizar o Master Data Services
  Há quatro cenários para atualizar para o Microsoft [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2. Escolha o cenário que se ajusta à sua situação.  
  
-   [Atualize sem a atualização do Mecanismo de Banco de Dados](#noengine)  
  
-   [Atualize com a atualização do Mecanismo de Banco de Dados](#engine)  
  
-   [Atualizar em Cenário de Dois Computadores](#twocomputer)  
  
-   [Atualizar com Restaurar um banco de dados do backup](#restore)  
  
> [!IMPORTANT]  
>  -   A atualização da versão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP1 para a versão CTP2 não tem suporte.  
> -   Faça um backup do banco de dados antes de executar atualizações.  
> -   O processo de atualização recria os procedimentos armazenados e atualiza tabelas usadas pelo [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Talvez você perca as personalizações feitas em um desses componentes.  
> -   Pacotes de implantação de modelo só podem ser usados na edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na qual foram criados. Você não pode implantar pacotes de implantação de modelo criados no [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] / [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
> -   Você pode continuar usando o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 versão do mestre de dados serviços de suplemento para Excel depois de atualizar o Master Data Services e Data Quality Services para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2. No entanto, qualquer versão anterior do suplemento Master Data Services para Excel não funcionará depois de atualizar para o SQL Server 2014 CTP2. Você pode baixar o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a versão SP1 do mestre dados serviços de suplemento para Excel a partir do [aqui](http://go.microsoft.com/fwlink/?LinkId=328664).  
  
##  <a name="noengine"></a> Atualize sem a atualização do Mecanismo de Banco de Dados  
 Esse cenário pode ser considerado uma instalação lado a lado, pois ambos [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] / [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] são instalados em paralelo, no mesmo computador ou em computadores separados.  
  
 Neste cenário, você continua usando o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] para hospedar seu banco de dados MDS. Entretanto, você precisa atualizar o esquema do banco de dados MDS e, depois, criar um aplicativo Web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para acessar o banco de dados MDS. O banco de dados MDS não pode mais ser acessado pelo aplicativo Web [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
 Se você optar por instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e uma versão anterior do SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]/[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) no mesmo computador, você poderá fazer isso pois os arquivos são instalados em um local diferente.  
  
-   No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\120\Master Data Services.  
  
-   No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\110\Master Data Services.  
  
-   No [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\Master Data Services.  
  
 Para executar esta tarefa, conclua as etapas a seguir.  
  
1.  Instale o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e outros recursos desejados.  
  
    1.  Abra o assistente de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    2.  No painel esquerdo, clique em **Instalação**.  
  
    3.  No painel direito, clique em **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.  
  
    4.  Na página **Seleção de Recursos** , selecione **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** e outros recursos que você deseje instalar.  
  
    5.  Conclua o assistente.  
  
2.  Quando a instalação for concluída, atualize o esquema de banco de dados MDS.  
  
    1.  Abra o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versão do [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
        > [!IMPORTANT]  
        >  Para atualizar o esquema de banco de dados MDS, você deve estar conectado como a Conta de Administrador que foi especificada quando o banco de dados MDS foi criado. No banco de dados MDS, em mdm.tblUser, este usuário tem o valor de **ID** de **1**. Para obter informações sobre como alterar esse usuário, consulte [alterar a conta de administrador do sistema &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
    2.  No painel esquerdo, clique em **Configuração do Banco de Dados**.  
  
    3.  No painel direito, clique em **Selecionar banco de dados** e especifique as informações para seus [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] instância de banco de dados.  
  
    4.  Clique em **Atualizar Banco de Dados** para iniciar o **Assistente para Atualizar Banco de Dados**. Para obter mais informações, consulte [Assistente para Fazer Upgrade de Banco de Dados &#40;Gerenciador de Configuração do Master Data Services&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md).  
  
3.  Quando a atualização for concluída, crie um aplicativo Web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    1.  Abra o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versão do [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
    2.  No painel esquerdo, clique em **Configuração da Web**.  
  
    3.  No painel direito, na lista **Site** , selecione uma das seguintes opções:  
  
        -   **Site Padrão da Web**e depois clique em **Criar Aplicativo**.  
  
        -   **Criar novo site**. Um novo aplicativo Web é criado automaticamente quando o site é criado.  
  
        > [!IMPORTANT]  
        >  Seu aplicativo Web do MDS existente de uma versão anterior do SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) está disponível para seleção na versão SQL Server 2014 do Gerenciador de Configuração do Master Data Services. Você não deve selecionar o aplicativo Web existente e, em vez disso, deve criar um aplicativo Web do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para o MDS. Caso contrário, você receberá um erro ao tentar associar o aplicativo Web com o banco de dados do MDS atualizado que indica que a página solicitada não pode ser acessada porque os dados de configuração relacionados à página são inválidos.  
        >   
        >  Se você quiser usar o mesmo nome (alias) para o aplicativo Web do MDS como seu aplicativo Web existente ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]), primeiro você deve excluir o aplicativo Web e o pool de aplicativos associado do IIS, e cria um aplicativo Web com o mesmo nome usando a versão SQL Server 2014 do Gerenciador de Configuração do Master Data Services. Para obter mais informações sobre como remover o aplicativo Web e os pools de aplicativos do IIS, veja [Remover um aplicativo (IIS)](http://go.microsoft.com/fwlink/?LinkId=323537) e [Remover um pool de aplicativos (IIS)](http://go.microsoft.com/fwlink/?LinkId=323538).  
  
4.  Agora, associe o novo aplicativo Web ao banco de dados MDS atualizado.  
  
    1.  Na seção **Associar Aplicativo ao Banco de Dados** , clique em **Selecionar**.  
  
    2.  Selecione o banco de dados MDS.  
  
    3.  Clique em **Aplicar**.  
  
##  <a name="engine"></a> Atualize com a atualização do Mecanismo de Banco de Dados  
 Neste cenário, você atualizará o mecanismo de banco de dados e o aplicativo [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou SQL Server 2012 para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Para executar esta tarefa, conclua as etapas a seguir.  
  
1.  **Somente para o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]**: abra o **Painel de Controle** > **Programas e Recursos** e desinstale o Microsoft [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
2.  Atualizar o mecanismo de banco de dados para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    1.  Abra o assistente de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    2.  No painel esquerdo, clique em **Instalação**.  
  
    3.  No painel direito, clique em **atualizar do SQL Server 2005, SQL Server 2008, SQL Server 2008 R2 ou SQL Server 2012**.  
  
    4.  Conclua o assistente.  
  
3.  **Para [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] só**: quando a atualização for concluída, adicione o **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** recurso.  
  
    1.  Abra o assistente de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    2.  No painel esquerdo, clique em **Instalação**.  
  
    3.  No painel direito, clique em **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.  
  
    4.  Sobre o **tipo de instalação** página do assistente, selecione a **adicionar recursos a uma instância existente** opção e, em seguida, escolha a instância onde o banco de dados MDS está instalado.  
  
    5.  Sobre o **seleção de recursos** página, em **recursos compartilhados**, selecione **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]**.  
  
    6.  Conclua o assistente.  
  
4.  Atualize o esquema de banco de dados de MDS.  
  
    1.  Abra o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versão do [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
        > [!IMPORTANT]  
        >  Para atualizar o esquema de banco de dados MDS, você deve estar conectado como a Conta de Administrador que foi especificada quando o banco de dados MDS foi criado. No banco de dados MDS, em mdm.tblUser, este usuário tem o valor de **ID** de **1**. Para obter informações sobre como alterar esse usuário, consulte [alterar a conta de administrador do sistema &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
    2.  No painel esquerdo, clique em **Configuração do Banco de Dados**.  
  
    3.  No painel direito, clique em **Selecionar banco de dados** e especifique as informações para sua instância de banco de dados.  
  
    4.  Clique em **Atualizar Banco de Dados** para iniciar o **Assistente para Atualizar Banco de Dados**. Para obter mais informações, consulte [Assistente para Fazer Upgrade de Banco de Dados &#40;Gerenciador de Configuração do Master Data Services&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md).  
  
    5.  Clique em **Aplicar**.  
  
5.  Quando a atualização for concluída, crie um aplicativo Web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    1.  Abra o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versão do [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
    2.  No painel esquerdo, clique em **Configuração da Web**.  
  
    3.  No painel direito, na lista **Site** , selecione uma das seguintes opções:  
  
        -   **Site Padrão da Web**e depois clique em **Criar Aplicativo**.  
  
        -   **Criar novo site**. Um novo aplicativo Web é criado automaticamente quando o site é criado.  
  
        > [!IMPORTANT]  
        >  Seu aplicativo Web do MDS existente de uma versão anterior do SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) está disponível para seleção na versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do Gerenciador de Configuração do Master Data Services. Você não deve selecionar o aplicativo Web existente e, em vez disso, deve criar um aplicativo Web do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para o MDS. Caso contrário, você receberá um erro ao tentar associar o aplicativo Web com o banco de dados do MDS atualizado que indica que a página solicitada não pode ser acessada porque os dados de configuração relacionados à página são inválidos.  
        >   
        >  Se você quiser usar o mesmo nome (alias) para o aplicativo Web do MDS como seu aplicativo Web existente ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]), primeiro você deve excluir o aplicativo Web e o pool de aplicativos associado do IIS, e cria um aplicativo Web com o mesmo nome usando a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do Gerenciador de Configuração do Master Data Services. Para obter mais informações sobre como remover o aplicativo Web e os pools de aplicativos do IIS, veja [Remover um aplicativo (IIS)](http://go.microsoft.com/fwlink/?LinkId=323537) e [Remover um pool de aplicativos (IIS)](http://go.microsoft.com/fwlink/?LinkId=323538).  
  
6.  Agora, associe o novo aplicativo Web ao banco de dados MDS atualizado.  
  
    1.  Na seção **Associar Aplicativo ao Banco de Dados** , clique em **Selecionar**.  
  
    2.  Selecione o banco de dados MDS.  
  
    3.  Clique em **Aplicar**.  
  
##  <a name="twocomputer"></a> Atualizar em Cenário de Dois Computadores  
 Este cenário envolve a atualização de um sistema no qual o SQL Server está instalado em dois computadores: um com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e o outro com SQL Server 2008 R2 ou SQL Server 2012.  
  
 Se o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] estiver instalado, você continuará usando o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] respectivamente para hospedar seu banco de dados MDS em um computador. Entretanto, você precisa atualizar o esquema do banco de dados MDS e, depois, usar o aplicativo Web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para acessar o banco de dados MDS. O banco de dados MDS não pode mais ser acessado pelo aplicativo Web [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
-   No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\120\Master Data Services.  
  
-   No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\110\Master Data Services.  
  
-   No [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\Master Data Services.  
  
 Para executar esta tarefa, conclua as etapas a seguir.  
  
1.  Instale o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e outros recursos desejados.  
  
    1.  Abra o assistente de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    2.  No painel esquerdo, clique em **Instalação**.  
  
    3.  No painel direito, clique em **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.  
  
    4.  Na página **Seleção de Recursos** , selecione **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** e outros recursos que você deseje instalar.  
  
    5.  Conclua o assistente.  
  
2.  Quando a instalação for concluída, atualize o esquema de banco de dados MDS.  
  
    1.  Abra o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versão do [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
        > [!IMPORTANT]  
        >  Para atualizar o esquema de banco de dados MDS, você deve estar conectado como a Conta de Administrador que foi especificada quando o banco de dados MDS foi criado. No banco de dados MDS, em mdm.tblUser, este usuário tem o valor de **ID** de **1**. Para obter informações sobre como alterar esse usuário, consulte [alterar a conta de administrador do sistema &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
    2.  No painel esquerdo, clique em **Configuração do Banco de Dados**.  
  
    3.  No painel direito, clique em **Selecionar banco de dados** e especifique as informações para seus [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] instância em outro computador, do banco de dados se [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] está instalado no outro computador.  
  
    4.  Clique em **Atualizar Banco de Dados** para iniciar o **Assistente para Atualizar Banco de Dados**. Para obter mais informações, consulte [Assistente para Fazer Upgrade de Banco de Dados &#40;Gerenciador de Configuração do Master Data Services&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md).  
  
3.  Quando a atualização for concluída, crie um aplicativo Web SQL Server 2014.  
  
    1.  Abra o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versão do [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
    2.  No painel esquerdo, clique em **Configuração da Web**.  
  
    3.  No painel direito, na lista **Site** , selecione uma das seguintes opções:  
  
        -   **Site Padrão da Web**e depois clique em **Criar Aplicativo**.  
  
        -   **Criar novo site**. Um novo aplicativo Web é criado automaticamente quando o site é criado.  
  
        > [!IMPORTANT]  
        >  Seu aplicativo Web do MDS existente de uma versão anterior do SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) está disponível para seleção na versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do Gerenciador de Configuração do Master Data Services. Você não deve selecionar o aplicativo Web existente e, em vez disso, deve criar um aplicativo Web do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para o MDS. Caso contrário, você receberá um erro ao tentar associar o aplicativo Web com o banco de dados do MDS atualizado que indica que a página solicitada não pode ser acessada porque os dados de configuração relacionados à página são inválidos.  
        >   
        >  Se você quiser usar o mesmo nome (alias) para o aplicativo Web do MDS como seu aplicativo Web existente ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]), primeiro você deve excluir o aplicativo Web e o pool de aplicativos associado do IIS, e cria um aplicativo Web com o mesmo nome usando a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do Gerenciador de Configuração do Master Data Services. Para obter mais informações sobre como remover o aplicativo Web e os pools de aplicativos do IIS, veja [Remover um aplicativo (IIS)](http://go.microsoft.com/fwlink/?LinkId=323537) e [Remover um pool de aplicativos (IIS)](http://go.microsoft.com/fwlink/?LinkId=323538).  
  
4.  Agora, associe o aplicativo Web ao banco de dados MDS atualizado.  
  
    1.  Na seção **Associar Aplicativo ao Banco de Dados** , clique em **Selecionar**.  
  
    2.  Selecione o banco de dados MDS.  
  
    3.  Clique em **Aplicar**.  
  
##  <a name="restore"></a> Atualizar com Restaurar um banco de dados do backup  
 Neste cenário, o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] é instalado junto com o SQL Server 2008 R2 ou SQL Server 2012 no mesmo computador ou em dois computadores diferentes. Além disso, um banco de dados foi armazenado em backup em uma versão anterior ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2, antes da atualização, e o banco de dados teve que ser restaurado.  
  
-   No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\120\Master Data Services.  
  
-   No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\110\Master Data Services.  
  
-   No [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\Master Data Services.  
  
 Para executar esta tarefa, conclua as etapas a seguir.  
  
1.  Instale o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e outros recursos desejados.  
  
    1.  Abra o assistente de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    2.  No painel esquerdo, clique em **Instalação**.  
  
    3.  No painel direito, clique em **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.  
  
    4.  Na página **Seleção de Recursos** , selecione **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** e outros recursos que você deseje instalar.  
  
    5.  Conclua o assistente.  
  
2.  Restaure o banco de dados cujo backup foi feito.  
  
3.  Quando a instalação for concluída, atualize o esquema de banco de dados MDS.  
  
    1.  Abra o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versão do [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
        > [!IMPORTANT]  
        >  Para atualizar o esquema de banco de dados MDS, você deve estar conectado como a Conta de Administrador que foi especificada quando o banco de dados MDS foi criado. No banco de dados MDS, em mdm.tblUser, este usuário tem o valor de **ID** de **1**. Para obter informações sobre como alterar esse usuário, consulte [alterar a conta de administrador do sistema &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
    2.  No painel esquerdo, clique em **Configuração do Banco de Dados**.  
  
    3.  No painel direito, clique em **Selecionar banco de dados** e especifique as informações para seus [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] instância de banco de dados.  
  
    4.  Clique em **Atualizar Banco de Dados** para iniciar o **Assistente para Atualizar Banco de Dados**. Para obter mais informações, consulte [Assistente para Fazer Upgrade de Banco de Dados &#40;Gerenciador de Configuração do Master Data Services&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md).  
  
4.  Quando a atualização for concluída, crie um aplicativo Web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    1.  Abra o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versão do [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
    2.  No painel esquerdo, clique em **Configuração da Web**.  
  
    3.  No painel direito, na lista **Site** , selecione uma das seguintes opções:  
  
        -   **Site Padrão da Web**e depois clique em **Criar Aplicativo**.  
  
        -   **Criar novo site**. Um novo aplicativo Web é criado automaticamente quando o site é criado.  
  
        > [!IMPORTANT]  
        >  Seu aplicativo Web do MDS existente de uma versão anterior do SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) está disponível para seleção na versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do Gerenciador de Configuração do Master Data Services. Você não deve selecionar o aplicativo Web existente e, em vez disso, deve criar um aplicativo Web do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para o MDS. Caso contrário, você receberá um erro ao tentar associar o aplicativo Web com o banco de dados do MDS atualizado que indica que a página solicitada não pode ser acessada porque os dados de configuração relacionados à página são inválidos.  
        >   
        >  Se você quiser usar o mesmo nome (alias) para o aplicativo Web do MDS como seu aplicativo Web existente ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]), primeiro você deve excluir o aplicativo Web e o pool de aplicativos associado do IIS, e cria um aplicativo Web com o mesmo nome usando a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do Gerenciador de Configuração do Master Data Services. Para obter mais informações sobre como remover o aplicativo Web e os pools de aplicativos do IIS, veja [Remover um aplicativo (IIS)](http://go.microsoft.com/fwlink/?LinkId=323537) e [Remover um pool de aplicativos (IIS)](http://go.microsoft.com/fwlink/?LinkId=323538).  
  
5.  Agora, associe o novo aplicativo Web ao banco de dados MDS atualizado.  
  
    1.  Na seção **Associar Aplicativo ao Banco de Dados** , clique em **Selecionar**.  
  
    2.  Selecione o banco de dados MDS.  
  
    3.  Clique em **Aplicar**.  
  
## <a name="troubleshooting"></a>Solução de problemas  
 **Problema:** quando você abre o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] aplicativo da web, uma mensagem de erro "versão do cliente não é compatível com a versão do banco de dados" é exibido.  
  
 **Solução:** esse problema ocorre quando um [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] aplicativo web Master Data Manager tenta acessar um banco de dados que foi atualizado para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Master Data Services. Você deve usar um aplicativo Web SQL [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 O problema também poderá ocorrer se você não parar e reiniciar o **Pool de Aplicativos MDS** no IIS ao atualizar o esquema de banco de dados MDS. Reinicie o **Pool de Aplicativos MDS** para corrigir o problema.  
  
## <a name="see-also"></a>Consulte também  
 [Instalar o Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
