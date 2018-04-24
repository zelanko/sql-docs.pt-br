---
title: Fazer upgrade do Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 07/21/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9c3543f3-3eb9-455d-a9bf-f17e9506ad21
caps.latest.revision: 31
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4abb0b1083aab2b944636e838586a39990e6ad06
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="upgrade-master-data-services"></a>Atualizar o Master Data Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  Veja a seguir os cenários de upgrade do Microsoft [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Master Data Services.  
  
-   [Atualize sem a atualização do Mecanismo de Banco de Dados](../../database-engine/install-windows/upgrade-master-data-services.md#noengine)  
  
-   [Atualize com a atualização do Mecanismo de Banco de Dados](../../database-engine/install-windows/upgrade-master-data-services.md#engine)  
  
-   [Atualizar em Cenário de Dois Computadores](../../database-engine/install-windows/upgrade-master-data-services.md#twocomputer)  
  
-   [Atualizar com Restaurar um banco de dados do backup](../../database-engine/install-windows/upgrade-master-data-services.md#restore)  
  
> [!IMPORTANT]  
> -   A atualização da versão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP1 para a versão CTP2 não tem suporte.  
> -   Faça um backup do banco de dados antes de executar atualizações.  
> -   O processo de atualização recria os procedimentos armazenados e atualiza tabelas usadas pelo [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Talvez você perca as personalizações feitas em um desses componentes.  
> -   Pacotes de implantação de modelo só podem ser usados na edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na qual foram criados. Você não pode implantar pacotes de implantação de modelo criados no [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
> -   Depois de atualizar o Data Quality Services e o Master Data Services para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], uma versão anterior do suplemento Master Data Services para Excel deixará de funcionar. Baixe o suplemento [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Master Data Services para Excel em [Suplemento Master Data Services para Microsoft Excel](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md).  
  
##  <a name="fileLocation"></a> Local do arquivo  
  
-   No [!INCLUDE[ss2017](../../includes/sssqlv14-md.md)], por padrão, os arquivos são instalados em *drive*:\Program Files\Microsoft SQL Server\140\Master Data Services.  

-   No [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], por padrão, os arquivos são instalados em *drive*:\Program Files\Microsoft SQL Server\130\Master Data Services.  
  
-   No [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\120\Master Data Services.  
  
-   No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\110\Master Data Services.  
  
-   No [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], por padrão, os arquivos são instalados em *unidade*:\Arquivos de Programas\Microsoft SQL Server\Master Data Services.  
  
##  <a name="noengine"></a> Atualize sem a atualização do Mecanismo de Banco de Dados  
 Neste cenário, você continua usando o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ou [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] para hospedar o banco de dados do MDS. Entretanto, você precisa fazer upgrade do esquema do banco de dados do MDS e, depois, criar um aplicativo Web do [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] atual para acessar o banco de dados do MDS. Após o upgrade, o banco de dados do MDS não poderá mais ser acessado pelo aplicativo Web anterior.  
  
 Você pode instalar o [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] atual e uma versão anterior do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] no mesmo computador. Os arquivos são instalados em locais diferentes, conforme mostrado no [Local do arquivo](#fileLocation).  
  
 **Para atualizar sem a atualização do mecanismo de banco de dados**  
  
1.  Instale o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e outros recursos desejados.  
  
    1.  Abra o assistente de instalação do [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)].  
  
    2.  No painel esquerdo, clique em **Instalação**.  
  
    3.  No painel direito, clique em **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.  
  
    4.  Na página **Seleção de Recursos** , selecione **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** e outros recursos que você deseje instalar.  
  
    5.  Conclua o assistente.  
  
2.  Atualize o esquema de banco de dados de MDS.  
  
    1.  Abra o [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] atual.  
  
        > [!IMPORTANT]  
        >  Para atualizar o esquema de banco de dados MDS, você deve estar conectado como a Conta de Administrador que foi especificada quando o banco de dados MDS foi criado. No banco de dados MDS, em mdm.tblUser, este usuário tem o valor de **ID** de **1**.  
  
    2.  No painel esquerdo, clique em **Configuração do Banco de Dados**.  
  
    3.  No painel direito, clique em **Selecionar Banco de Dados** e especifique as informações da instância de banco de dados do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ou [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
    4.  Clique em **Atualizar Banco de Dados** para iniciar o **Assistente para Atualizar Banco de Dados**. Para obter mais informações, consulte [Assistente para Fazer Upgrade de Banco de Dados &#40;Gerenciador de Configuração do Master Data Services&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md).  
  
3.  Crie um aplicativo Web.  
  
    1.  Abra o [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] atual.  
  
    2.  No painel esquerdo, clique em **Configuração da Web**.  
  
    3.  No painel direito, na lista **Site** , selecione uma das seguintes opções:  
  
        -   **Site Padrão da Web**e depois clique em **Criar Aplicativo**.  
  
        -   **Criar novo site**. Um novo aplicativo Web é criado automaticamente quando o site é criado.  
  
        > [!IMPORTANT]  
        >  O aplicativo Web do MDS existente de uma versão anterior do SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ou [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) está disponível para seleção na versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do Gerenciador de Configuração do Master Data Services. Você não deve selecionar o aplicativo Web existente e, em vez disso, deve criar um aplicativo Web do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] para o MDS. Caso contrário, você receberá um erro ao tentar associar o aplicativo Web com o banco de dados do MDS atualizado que indica que a página solicitada não pode ser acessada porque os dados de configuração relacionados à página são inválidos.  
        >   
        >  Se desejar usar o mesmo nome (alias) para o aplicativo Web do MDS do aplicativo Web existente ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ou [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]), primeiro deverá excluir o aplicativo Web e o pool de aplicativos associado do IIS e, depois, criar um aplicativo Web com o mesmo nome usando a versão [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] do Gerenciador de Configuração do Master Data Services. Para obter mais informações sobre como remover o aplicativo Web e os pools de aplicativos do IIS, veja [Remover um aplicativo (IIS)](http://go.microsoft.com/fwlink/?LinkId=323537) e [Remover um pool de aplicativos (IIS)](http://go.microsoft.com/fwlink/?LinkId=323538).  
  
4.  Associe o novo aplicativo Web ao banco de dados MDS atualizado.  
  
    1.  Na seção **Associar Aplicativo ao Banco de Dados** , clique em **Selecionar**.  
  
    2.  Selecione o banco de dados MDS.  
  
    3.  Clique em **Aplicar**.  
  
##  <a name="engine"></a> Atualize com a atualização do Mecanismo de Banco de Dados  
 Neste cenário, você fará upgrade do mecanismo de banco de dados e do aplicativo [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] de uma versão anterior para o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ou [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)].  
  
 **Para atualizar com a atualização do Mecanismo de Banco de Dados**  
  
1.  **Somente para o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]**: abra o **Painel de Controle** > **Programas e Recursos** e desinstale o Microsoft [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
2.  Faça upgrade do mecanismo de banco de dados para o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ou [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)]. Para obter mais informações, consulte [Choose a Database Engine Upgrade Method](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md).  
  
3.  Conclua todas as etapas em [Atualize sem a atualização do Mecanismo de Banco de Dados](#noengine) .  
  
##  <a name="twocomputer"></a> Atualizar em Cenário de Dois Computadores  
 Neste cenário, você faz upgrade de um sistema no qual o SQL Server está instalado em dois computadores: um com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ou [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)] e o outro com uma versão anterior do [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)].  
  
 Se uma versão anterior do [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] estiver instalada, você continuará usando a versão anterior para hospedar o banco de dados do MDS em um computador. Entretanto, é necessário fazer upgrade do esquema do banco de dados do MDS e, depois, usar o aplicativo Web [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ou [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)], respectivamente, para acessar o banco de dados do MDS. O banco de dados do MDS não pode mais ser acessado pelo aplicativo Web com a versão anterior.  
  
 **Para atualizar em cenário de dois computadores**  
  
-   Conclua todas as etapas em [Atualize sem a atualização do Mecanismo de Banco de Dados](#noengine).  
  
##  <a name="restore"></a> Atualizar com Restaurar um banco de dados do backup  
 Neste cenário, o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ou o [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)] é instalado junto com uma versão anterior no mesmo computador ou em dois computadores diferentes. Um banco de dados foi copiado em backup em uma versão anterior ao [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ou [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)], antes do upgrade e o banco de dados deve ser restaurado.  
  
 **Para atualizar com restauração de um banco de dados do backup**  
  
1.  Instale o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e outros recursos desejados.  
  
    1.  Abra o assistente de instalação do [!INCLUDE[sssnoversion](../../includes/ssnoversion-md.md)].  
  
    2.  No painel esquerdo, clique em **Instalação**.  
  
    3.  No painel direito, clique em **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.  
  
    4.  Na página **Seleção de Recursos** , selecione **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** e outros recursos que você deseje instalar.  
  
    5.  Conclua o assistente.  
  
2.  Restaure o banco de dados cujo backup foi feito.  
  
3.  Atualize o esquema de banco de dados do MDS, crie um aplicativo Web e associe o novo aplicativo Web com o banco de dados do MDS atualizado. Para obter instruções, confira as etapas 2 a 4 em [Atualizar sem a atualização do Mecanismo de Banco de Dados](#noengine)  
  
## <a name="troubleshooting"></a>Solução de problemas  
 **Problema:** ao abrir o aplicativo Web [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ou [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], a mensagem de erro “a versão de cliente não é compatível com a versão de banco de dados” é exibida.  
  
 **Solução:** esse problema ocorre quando um aplicativo Web do Master Data Manager do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ou [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tenta acessar um banco de dados que foi atualizado para o [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)] Master Data Services. Use um ou um aplicativo Web [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)].  
  
 O problema também poderá ocorrer se você não parar e reiniciar o **Pool de Aplicativos MDS** no IIS ao atualizar o esquema de banco de dados MDS. Reinicie o **Pool de Aplicativos MDS** para corrigir o problema.  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar o Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
