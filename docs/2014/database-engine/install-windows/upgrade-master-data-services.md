---
title: Fazer upgrade do Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9c3543f3-3eb9-455d-a9bf-f17e9506ad21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: da78f21c6346281dc23332f40e8e6f46ff07aa06
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62774650"
---
# <a name="upgrade-master-data-services"></a>Atualizar o Master Data Services
  Há quatro cenários para atualizar para o Microsoft [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2. Escolha o cenário que se ajusta à sua situação.  
  
-   [Atualizar sem Mecanismo de Banco de Dados atualização](#noengine)  
  
-   [Atualizar com a atualização do Mecanismo de Banco de Dados](#engine)  
  
-   [Atualizar em cenário de dois computadores](#twocomputer)  
  
-   [Atualizar com a restauração de um banco de dados do backup](#restore)  
  
> [!IMPORTANT]
>  -   A atualização da versão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP1 para a versão CTP2 não tem suporte.  
> -   Faça um backup do banco de dados antes de executar atualizações.  
> -   O processo de atualização recria os procedimentos armazenados e atualiza tabelas usadas pelo [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Talvez você perca as personalizações feitas em um desses componentes.  
> -   Pacotes de implantação de modelo só podem ser usados na edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na qual foram criados. Você não pode implantar pacotes de implantação de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] / [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] modelo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]criados no para.  
> -   Você pode continuar a usar a versão do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 do suplemento Master Data Services para Excel depois de atualizar o Master Data Services e o Data Quality Services para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2. No entanto, qualquer versão anterior do suplemento Master Data Services para Excel não funcionará depois de atualizar para o SQL Server 2014 CTP2. Você pode baixar a versão do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 do suplemento Master Data Services para Excel [aqui](https://go.microsoft.com/fwlink/?LinkId=328664).  
  
##  <a name="noengine"></a>Atualizar sem Mecanismo de Banco de Dados atualização  
 Esse cenário pode ser considerado uma instalação lado [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] / [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a lado, porque o e [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o são instalados em paralelo, no mesmo computador ou em computadores separados.  
  
 Neste cenário, você continua usando o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] para hospedar seu banco de dados MDS. Entretanto, você precisa atualizar o esquema do banco de dados MDS e, depois, criar um aplicativo Web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para acessar o banco de dados MDS. O banco de dados MDS não pode mais ser acessado pelo aplicativo Web [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
 Se você optar por instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o e uma versão anterior do SQL Server[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]/[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]() no mesmo computador, poderá fazer isso porque os arquivos são instalados em um local diferente.  
  
-   No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\120\Master Data Services.  
  
-   No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\110\Master Data Services.  
  
-   No [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\Master Data Services.  
  
 Para executar esta tarefa, conclua as etapas a seguir.  
  
1.  Instale o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e outros recursos desejados.  
  
    1.  Abra o assistente de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
    2.  No painel esquerdo, clique em **Instalação**.  
  
    3.  No painel direito, clique em **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.  
  
    4.  Na página **Seleção de Recursos** , selecione **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** e outros recursos que você deseje instalar.  
  
    5.  Conclua o assistente.  
  
2.  Quando a instalação for concluída, atualize o esquema de banco de dados MDS.  
  
    1.  Abra a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
        > [!IMPORTANT]  
        >  Para atualizar o esquema de banco de dados MDS, você deve estar conectado como a Conta de Administrador que foi especificada quando o banco de dados MDS foi criado. No banco de dados MDS, em mdm.tblUser, este usuário tem o valor de **ID** de **1**. Para obter informações sobre como alterar esse usuário, consulte [alterar a conta de administrador do sistema &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
    2.  No painel esquerdo, clique em **Configuração do Banco de Dados**.  
  
    3.  No painel direito, clique em **Selecionar Banco de dados** e especifique as informações [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] para [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] sua instância do banco de dados do ou do.  
  
    4.  Clique em **Atualizar Banco de Dados** para iniciar o **Assistente para Atualizar Banco de Dados**. Para obter mais informações, consulte [Assistente para Fazer Upgrade de Banco de Dados &#40;Gerenciador de Configuração do Master Data Services&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md).  
  
3.  Quando a atualização for concluída, crie um aplicativo Web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    1.  Abra a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
    2.  No painel esquerdo, clique em **Configuração da Web**.  
  
    3.  No painel direito, na lista **Site** , selecione uma das seguintes opções:  
  
        -   **Site da Web padrão**e clique em **criar aplicativo**.  
  
        -   **Criar novo site**. Um novo aplicativo Web é criado automaticamente quando o site é criado.  
  
        > [!IMPORTANT]  
        >  Seu aplicativo Web do MDS existente de uma versão anterior do SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) está disponível para seleção na versão SQL Server 2014 do Gerenciador de Configuração do Master Data Services. Você não deve selecionar o aplicativo Web existente e, em vez disso, deve criar um aplicativo Web do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para o MDS. Caso contrário, você receberá um erro ao tentar associar o aplicativo Web com o banco de dados do MDS atualizado que indica que a página solicitada não pode ser acessada porque os dados de configuração relacionados à página são inválidos.  
        >   
        >  Se você quiser usar o mesmo nome (alias) para o aplicativo Web do MDS como seu aplicativo Web existente ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]), primeiro você deve excluir o aplicativo Web e o pool de aplicativos associado do IIS, e cria um aplicativo Web com o mesmo nome usando a versão SQL Server 2014 do Gerenciador de Configuração do Master Data Services. Para obter mais informações sobre como remover o aplicativo Web e os pools de aplicativos do IIS, veja [Remover um aplicativo (IIS)](https://go.microsoft.com/fwlink/?LinkId=323537) e [Remover um pool de aplicativos (IIS)](https://go.microsoft.com/fwlink/?LinkId=323538).  
  
4.  Agora, associe o novo aplicativo Web ao banco de dados MDS atualizado.  
  
    1.  Na seção **Associar Aplicativo ao Banco de Dados** , clique em **Selecionar**.  
  
    2.  Selecione o banco de dados MDS.  
  
    3.  Clique em **Aplicar**.  
  
##  <a name="engine"></a>Atualizar com a atualização do Mecanismo de Banco de Dados  
 Neste cenário, você atualizará o mecanismo de banco de dados e o aplicativo [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou SQL Server 2012 para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Para executar esta tarefa, conclua as etapas a seguir.  
  
1.  **Somente [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] para**o: Abra o **painel** > de controle**programas e recursos** e desinstale o Microsoft [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
2.  Atualizar o mecanismo de banco de dados para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    1.  Abra o assistente de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
    2.  No painel esquerdo, clique em **Instalação**.  
  
    3.  No painel direito, clique em **Atualizar do SQL Server 2005, SQL Server 2008, SQL Server 2008 R2 ou SQL Server 2012**.  
  
    4.  Conclua o assistente.  
  
3.  **Somente [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] para**: quando a atualização for concluída, adicione o **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** recurso.  
  
    1.  Abra o assistente de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
    2.  No painel esquerdo, clique em **Instalação**.  
  
    3.  No painel direito, clique em **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.  
  
    4.  Na página **tipo de instalação** do assistente, selecione a opção **Adicionar recursos a uma instância existente** e escolha a instância em que o banco de dados MDS está instalado.  
  
    5.  Na página **seleção de recursos** , em **recursos compartilhados**, selecione **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]**.  
  
    6.  Conclua o assistente.  
  
4.  Atualize o esquema de banco de dados de MDS.  
  
    1.  Abra a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
        > [!IMPORTANT]  
        >  Para atualizar o esquema de banco de dados MDS, você deve estar conectado como a Conta de Administrador que foi especificada quando o banco de dados MDS foi criado. No banco de dados MDS, em mdm.tblUser, este usuário tem o valor de **ID** de **1**. Para obter informações sobre como alterar esse usuário, consulte [alterar a conta de administrador do sistema &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
    2.  No painel esquerdo, clique em **Configuração do Banco de Dados**.  
  
    3.  No painel direito, clique em **Selecionar Banco de dados** e especifique as informações para sua instância de banco de dados.  
  
    4.  Clique em **Atualizar Banco de Dados** para iniciar o **Assistente para Atualizar Banco de Dados**. Para obter mais informações, consulte [Assistente para Fazer Upgrade de Banco de Dados &#40;Gerenciador de Configuração do Master Data Services&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md).  
  
    5.  Clique em **Aplicar**.  
  
5.  Quando a atualização for concluída, crie um aplicativo Web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    1.  Abra a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
    2.  No painel esquerdo, clique em **Configuração da Web**.  
  
    3.  No painel direito, na lista **Site** , selecione uma das seguintes opções:  
  
        -   **Site da Web padrão**e clique em **criar aplicativo**.  
  
        -   **Criar novo site**. Um novo aplicativo Web é criado automaticamente quando o site é criado.  
  
        > [!IMPORTANT]  
        >  Seu aplicativo Web do MDS existente de uma versão anterior do SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) está disponível para seleção na versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do Gerenciador de Configuração do Master Data Services. Você não deve selecionar o aplicativo Web existente e, em vez disso, deve criar um aplicativo Web do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para o MDS. Caso contrário, você receberá um erro ao tentar associar o aplicativo Web com o banco de dados do MDS atualizado que indica que a página solicitada não pode ser acessada porque os dados de configuração relacionados à página são inválidos.  
        >   
        >  Se você quiser usar o mesmo nome (alias) para o aplicativo Web do MDS como seu aplicativo Web existente ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]), primeiro você deve excluir o aplicativo Web e o pool de aplicativos associado do IIS, e cria um aplicativo Web com o mesmo nome usando a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do Gerenciador de Configuração do Master Data Services. Para obter mais informações sobre como remover o aplicativo Web e os pools de aplicativos do IIS, veja [Remover um aplicativo (IIS)](https://go.microsoft.com/fwlink/?LinkId=323537) e [Remover um pool de aplicativos (IIS)](https://go.microsoft.com/fwlink/?LinkId=323538).  
  
6.  Agora, associe o novo aplicativo Web ao banco de dados MDS atualizado.  
  
    1.  Na seção **Associar Aplicativo ao Banco de Dados** , clique em **Selecionar**.  
  
    2.  Selecione o banco de dados MDS.  
  
    3.  Clique em **Aplicar**.  
  
##  <a name="twocomputer"></a>Atualizar em cenário de dois computadores  
 Este cenário envolve a atualização de um sistema no qual o SQL Server está instalado em dois computadores: um com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e o outro com SQL Server 2008 R2 ou SQL Server 2012.  
  
 Se o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] estiver instalado, você continuará usando o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] respectivamente para hospedar seu banco de dados MDS em um computador. Entretanto, você precisa atualizar o esquema do banco de dados MDS e, depois, usar o aplicativo Web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para acessar o banco de dados MDS. O banco de dados MDS não pode mais ser acessado pelo aplicativo Web [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
-   No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\120\Master Data Services.  
  
-   No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\110\Master Data Services.  
  
-   No [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\Master Data Services.  
  
 Para executar esta tarefa, conclua as etapas a seguir.  
  
1.  Instale o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e outros recursos desejados.  
  
    1.  Abra o assistente de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
    2.  No painel esquerdo, clique em **Instalação**.  
  
    3.  No painel direito, clique em **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.  
  
    4.  Na página **Seleção de Recursos** , selecione **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** e outros recursos que você deseje instalar.  
  
    5.  Conclua o assistente.  
  
2.  Quando a instalação for concluída, atualize o esquema de banco de dados MDS.  
  
    1.  Abra a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
        > [!IMPORTANT]  
        >  Para atualizar o esquema de banco de dados MDS, você deve estar conectado como a Conta de Administrador que foi especificada quando o banco de dados MDS foi criado. No banco de dados MDS, em mdm.tblUser, este usuário tem o valor de **ID** de **1**. Para obter informações sobre como alterar esse usuário, consulte [alterar a conta de administrador do sistema &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
    2.  No painel esquerdo, clique em **Configuração do Banco de Dados**.  
  
    3.  No painel direito, clique em **Selecionar Banco de dados** e especifique as informações [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] para [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] sua instância do ou do banco de dados [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] outro computador, se o ou o estiver instalado no outro computador.  
  
    4.  Clique em **Atualizar Banco de Dados** para iniciar o **Assistente para Atualizar Banco de Dados**. Para obter mais informações, consulte [Assistente para Fazer Upgrade de Banco de Dados &#40;Gerenciador de Configuração do Master Data Services&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md).  
  
3.  Quando a atualização for concluída, crie um aplicativo Web SQL Server 2014.  
  
    1.  Abra a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
    2.  No painel esquerdo, clique em **Configuração da Web**.  
  
    3.  No painel direito, na lista **Site** , selecione uma das seguintes opções:  
  
        -   **Site da Web padrão**e clique em **criar aplicativo**.  
  
        -   **Criar novo site**. Um novo aplicativo Web é criado automaticamente quando o site é criado.  
  
        > [!IMPORTANT]  
        >  Seu aplicativo Web do MDS existente de uma versão anterior do SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) está disponível para seleção na versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do Gerenciador de Configuração do Master Data Services. Você não deve selecionar o aplicativo Web existente e, em vez disso, deve criar um aplicativo Web do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para o MDS. Caso contrário, você receberá um erro ao tentar associar o aplicativo Web com o banco de dados do MDS atualizado que indica que a página solicitada não pode ser acessada porque os dados de configuração relacionados à página são inválidos.  
        >   
        >  Se você quiser usar o mesmo nome (alias) para o aplicativo Web do MDS como seu aplicativo Web existente ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]), primeiro você deve excluir o aplicativo Web e o pool de aplicativos associado do IIS, e cria um aplicativo Web com o mesmo nome usando a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do Gerenciador de Configuração do Master Data Services. Para obter mais informações sobre como remover o aplicativo Web e os pools de aplicativos do IIS, veja [Remover um aplicativo (IIS)](https://go.microsoft.com/fwlink/?LinkId=323537) e [Remover um pool de aplicativos (IIS)](https://go.microsoft.com/fwlink/?LinkId=323538).  
  
4.  Agora, associe o aplicativo Web ao banco de dados MDS atualizado.  
  
    1.  Na seção **Associar Aplicativo ao Banco de Dados** , clique em **Selecionar**.  
  
    2.  Selecione o banco de dados MDS.  
  
    3.  Clique em **Aplicar**.  
  
##  <a name="restore"></a>Atualizar com a restauração de um banco de dados do backup  
 Neste cenário, o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] é instalado junto com o SQL Server 2008 R2 ou SQL Server 2012 no mesmo computador ou em dois computadores diferentes. Além disso, um banco de dados foi armazenado em backup em uma versão anterior ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2, antes da atualização, e o banco de dados teve que ser restaurado.  
  
-   No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\120\Master Data Services.  
  
-   No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\110\Master Data Services.  
  
-   No [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\Master Data Services.  
  
 Para executar esta tarefa, conclua as etapas a seguir.  
  
1.  Instale o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e outros recursos desejados.  
  
    1.  Abra o assistente de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
    2.  No painel esquerdo, clique em **Instalação**.  
  
    3.  No painel direito, clique em **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.  
  
    4.  Na página **Seleção de Recursos** , selecione **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** e outros recursos que você deseje instalar.  
  
    5.  Conclua o assistente.  
  
2.  Restaure o banco de dados cujo backup foi feito.  
  
3.  Quando a instalação for concluída, atualize o esquema de banco de dados MDS.  
  
    1.  Abra a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
        > [!IMPORTANT]  
        >  Para atualizar o esquema de banco de dados MDS, você deve estar conectado como a Conta de Administrador que foi especificada quando o banco de dados MDS foi criado. No banco de dados MDS, em mdm.tblUser, este usuário tem o valor de **ID** de **1**. Para obter informações sobre como alterar esse usuário, consulte [alterar a conta de administrador do sistema &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
    2.  No painel esquerdo, clique em **Configuração do Banco de Dados**.  
  
    3.  No painel direito, clique em **Selecionar Banco de dados** e especifique as informações [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] para [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] sua instância do banco de dados do ou do.  
  
    4.  Clique em **Atualizar Banco de Dados** para iniciar o **Assistente para Atualizar Banco de Dados**. Para obter mais informações, consulte [Assistente para Fazer Upgrade de Banco de Dados &#40;Gerenciador de Configuração do Master Data Services&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md).  
  
4.  Quando a atualização for concluída, crie um aplicativo Web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    1.  Abra a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
    2.  No painel esquerdo, clique em **Configuração da Web**.  
  
    3.  No painel direito, na lista **Site** , selecione uma das seguintes opções:  
  
        -   **Site da Web padrão**e clique em **criar aplicativo**.  
  
        -   **Criar novo site**. Um novo aplicativo Web é criado automaticamente quando o site é criado.  
  
        > [!IMPORTANT]  
        >  Seu aplicativo Web do MDS existente de uma versão anterior do SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) está disponível para seleção na versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do Gerenciador de Configuração do Master Data Services. Você não deve selecionar o aplicativo Web existente e, em vez disso, deve criar um aplicativo Web do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para o MDS. Caso contrário, você receberá um erro ao tentar associar o aplicativo Web com o banco de dados do MDS atualizado que indica que a página solicitada não pode ser acessada porque os dados de configuração relacionados à página são inválidos.  
        >   
        >  Se você quiser usar o mesmo nome (alias) para o aplicativo Web do MDS como seu aplicativo Web existente ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]), primeiro você deve excluir o aplicativo Web e o pool de aplicativos associado do IIS, e cria um aplicativo Web com o mesmo nome usando a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do Gerenciador de Configuração do Master Data Services. Para obter mais informações sobre como remover o aplicativo Web e os pools de aplicativos do IIS, veja [Remover um aplicativo (IIS)](https://go.microsoft.com/fwlink/?LinkId=323537) e [Remover um pool de aplicativos (IIS)](https://go.microsoft.com/fwlink/?LinkId=323538).  
  
5.  Agora, associe o novo aplicativo Web ao banco de dados MDS atualizado.  
  
    1.  Na seção **Associar Aplicativo ao Banco de Dados** , clique em **Selecionar**.  
  
    2.  Selecione o banco de dados MDS.  
  
    3.  Clique em **Aplicar**.  
  
## <a name="troubleshooting"></a>Solução de problemas  
 **Problema:** Quando você abre o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] aplicativo [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web ou, uma mensagem de erro "a versão do cliente não é compatível com a versão do banco de dados" é exibida.  
  
 **Solução:** Esse problema ocorre quando um [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Master Data Manager aplicativo Web tenta acessar um banco de dados que foi atualizado para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Master Data Services. Você deve usar um aplicativo Web SQL [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
 O problema também poderá ocorrer se você não parar e reiniciar o **Pool de Aplicativos MDS** no IIS ao atualizar o esquema de banco de dados MDS. Reinicie o **Pool de Aplicativos MDS** para corrigir o problema.  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar o Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
