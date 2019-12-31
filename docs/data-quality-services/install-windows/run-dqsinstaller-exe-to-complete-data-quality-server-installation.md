---
title: Executar o DQSInstaller.exe para concluir a instalação do Data Quality Server
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 7a8c96e0-1328-4f35-97fc-b6d9cb808bae
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 9921840e66adc166004143deca7f9310b6e242ca
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258590"
---
# <a name="run-dqsinstallerexe-to-complete-data-quality-server-installation"></a>Executar o DQSInstaller.exe para concluir a instalação do Data Quality Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Para concluir a instalação do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] , você terá de executar o arquivo DQSInstaller.exe depois de instalar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Este tópico descreve como executar o DQSInstaller.exe na tela **Iniciar** , menu **Iniciar** , Windows Explorer ou Prompt de comando; você pode escolher qualquer uma das formas de executar o arquivo DQSInstaller.exe.  
  
##  <a name="Prerequisites"></a>Pré-requisitos  
  
-   Você deve ter selecionado **Data Quality Services** em **Serviços de Mecanismo de Banco de Dados** na página Seleção de Recursos na instalação do SQL Server ao instalar o SQL Server e deve ter concluído a instalação do SQL Server. Para obter mais informações, consulte [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  
  
-   Sua conta de usuário do Windows deve ser um membro da função de servidor fixa sysadmin na instância do mecanismo de banco de dados do SQL Server.  
  
-   Você deve estar conectado como um membro do grupo Administradores no computador em que você está executando o DQSInstaller.exe.  
  
##  <a name="WindowsExplorer"></a>Execute DQSInstaller. exe na tela iniciar, no menu iniciar ou no Windows Explorer  
  
1.  No computador onde você decidiu instalar o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)], execute o arquivo DQSInstaller.exe usando qualquer um destes procedimentos, conforme aplicável:  
  
    -   **Tela inicial**: na tela **Iniciar** , clique em **instalador do servidor de Data Quality.**  
  
    -   **Menu iniciar**: na barra de tarefas, clique em **Iniciar**, aponte para **todos os programas**e clique em [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]. Em [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], clique em **Data Quality Services**e depois clique em **Instalador do Data Quality Services**.  
  
    -   **Windows Explorer**: Localize o arquivo DQSInstaller. exe. Se você tiver instalado a instância padrão do SQL Server, o arquivo DQSInstaller.exe estará disponível em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn. Clique duas vezes no arquivo DQSInstaller.exe.  
  
2.  Uma janela do prompt de comando aparece que mostra o status da instalação. Você notará estas três características:  
  
    1.  O instalador cria um arquivo de log de instalação, DQS_install.log que contém informações sobre as ações executado em como executar o DQSInstaller.exe arquivo. Se você tiver instalado a instância padrão do SQL Server, o arquivo DQS_install.log estará disponível em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log.  
  
    2.  O instalador usa a ordenação do servidor padrão, SQL_Latin1_General_CP1_CI_AS, para instalar o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)].  
  
        > [!IMPORTANT]  
        >  Você poderá oferecer um valor de ordenação do servidor diferente para instalar o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] apenas se estiver executando o DQSInstaller.exe do prompt de comando. Para obter mais informações, consulte [Executar o DQSInstaller.exe do prompt de comando](#CommandPrompt) mais adiante neste tópico.  
  
    3.  O instalador verifica se existem reinicializações pendentes no seu computador devido a qualquer atualização recém-instalada em seu computador. Se for encontrada uma reinicialização pendente, uma mensagem aparecerá para notificá-lo sobre o mesmo e você poderá optar por continuar ou anular a instalação pressionando Y ou N, respectivamente. É recomendável, em caso de reinicializações pendentes, anular a instalação, reiniciar o computador e executar o DQSInstaller.exe novamente.  
  
3.  Você é solicitado a digitar uma senha para a chave mestra de banco de dados. A chave mestra de banco de dados é exigida criptografar o provedor de serviço de dados de referência tecla que será armazenada no DQS_MAIN banco de dados quando você configurar provedores de dados de referência posteriormente no [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS)  
  
    > [!IMPORTANT]  
    >  A senha deve ter pelo menos 8 caracteres e deve conter caracteres de três das quatro categorias a seguir: letra maiúscula em inglês (A, B, C,... Z), letra minúscula inglesa (a, b, c,... z), numeral (0, 1, 2,... 9) e caractere não alfanumérico ou especial (~! @ # $% ^& * () _-+ = |\\ {}[]:;"' <>,.? /). Por exemplo: P@ssword. O instalador o solicitará inserir outra senha se a senha atual não corresponder ao requisito.  
  
4.  Forneça uma senha, confirme a senha e pressione a ENTER para continuar com a instalação.  
  
    > [!IMPORTANT]  
    >  Você deve reter a senha especificada para a chave mestra de banco de dados porque precisará dela ao restaurar os bancos de dados DQS de um backup no futuro, caso opte por fazer isso. Para obter mais informações sobre como restaurar bancos de dados DQS, consulte [Backing Up and Restoring DQS Databases](../../data-quality-services/backing-up-and-restoring-dqs-databases.md).  
  
5.  Se um banco de dados do Master Data Services estiver presente na mesma instância do SQL Server que o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)], o instalador cria um usuário mapeado para o logon de Master Data Services será criado e concede a ele a função dqs_administrator no banco de dados DQS_MAIN. Para obter mais informações sobre como instalar o Master Data Services e criar um banco de dados do Master Data Services, consulte [Install Master Data Services](../../master-data-services/install-windows/install-master-data-services.md).  
  
6.  Uma mensagem de conclusão é exibida depois que a instalação é concluída com êxito. Pressione qualquer tecla para fechar a janela de prompt de comando.  
  
##  <a name="CommandPrompt"></a>Executar DQSInstaller. exe do prompt de comando  
 Você pode executar o DQSInstaller.exe do prompt de comando usando os seguintes parâmetros de linha de comando:  
  
|Parâmetro DQSInstaller.exe|Descrição|Sintaxe de exemplo|  
|--------------------------------|-----------------|-------------------|  
|-collation|A ordenação do servidor a ser usada para instalar o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)].<br /><br /> O DQS oferece suporte apenas à ordenação sem diferenciação de maiúsculas e minúsculas. Se você especificar uma ordenação com diferenciação de maiúsculas e minúsculas, o instalador tentará usar a versão sem diferenciação de maiúsculas e minúsculas da ordenação especificada. Se não houver versão sem diferenciação de maiúsculas e minúsculas, ou se a ordenação não tiver suporte do SQL, haverá falha na instalação do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)].<br /><br /> Se uma ordenação do servidor não for especificada, a ordenação padrão, SQL_Latin1_General_CP1_CI_AS, será usada.|`dqsinstaller.exe -collation <collation_name>`|  
|-upgradedlls|Ignora a recriação dos bancos de dados DQS (DQS_MAIN, DQS_PROJECTS e DQS_STAGING_DATA) e atualiza somente os assemblies SQLCLR (SQL Common Language Runtime) usados pelo DQS no banco de dados do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .<br /><br /> Para obter mais informações, veja [Atualizar assemblies SQLCLR após atualização do .NET Framework](../../data-quality-services/install-windows/upgrade-sqlclr-assemblies-after-net-framework-update.md)|`dqsinstaller.exe -upgradedlls`|  
|-exportkbs|Exporte todas as bases de dados de conhecimento em um arquivo de backup DQS (.dqsb). Você também tem de especificar o caminho completo e o nome de arquivo onde deseja exportar todas as bases de dados de conhecimento.<br /><br /> Para obter mais informações, consulte [Export and Import DQS Knowledge Bases Using DQSInstaller.exe](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md).|`dqsinstaller.exe -exportkbs <path><filename>`<br /><br /> Por exemplo, `dqsinstaller.exe -exportkbs c:\DQSBackup.dqsb`|  
|-importkbs|Importe todas as bases de dados de conhecimento de um arquivo de backup DQS (.dqsb) após concluir a instalação do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . Você também tem de especificar o caminho completo e o nome de arquivo de onde deseja importar todas as bases de dados de conhecimento.<br /><br /> Para obter mais informações, consulte [Export and Import DQS Knowledge Bases Using DQSInstaller.exe](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md).|`dqsinstaller.exe -importkbs <path><filename>`<br /><br /> Por exemplo, `dqsinstaller.exe -importkbs c:\DQSBackup.dqsb`|  
|-upgrade|Atualizar o esquema de bancos de dados do DQS. Você deve usar este parâmetro depois de ter instalado uma atualização do SQL Server em uma instância previamente configurada do DQS. Para obter mais informações, consulte [Upgrade DQS Databases Schema After Installing SQL Server Update](../../data-quality-services/install-windows/upgrade-dqs-databases-schema-after-installing-sql-server-update.md).|`dqsinstaller.exe -upgrade`|  
|-uninstall|Desinstala o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] da instância do SQL Server atual.<br /><br /> Você também pode exportar todas as bases de dados de conhecimento na instalação do Data Quality Server em um arquivo de backup DQS (.dqsb) e depois desinstalar o Data Quality Server. Para obter mais informações, consulte [Export and Import DQS Knowledge Bases Using DQSInstaller.exe](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md).<br /><br /> ** \* Importante \* \* ** Se você desinstalar [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] o de uma instância do SQL Server `-uninstall` usando o parâmetro de linha de comando, todos os objetos do DQS serão excluídos como parte do processo de desinstalação. Você não precisa excluí-los manualmente depois de desinstalar o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] , conforme mencionado em [Remover objetos do Data Quality Server](../../sql-server/install/remove-data-quality-server-objects.md).|**Para desinstalar apenas o Data Quality Server:**<br /><br /> `dqsinstaller.exe -uninstall`<br /><br /> **Para exportar todas as bases de dados de conhecimento para um arquivo e, em seguida, desinstalar o Data Quality Server:**<br /><br /> `dqsinstaller.exe -uninstall <path><filename>`<br /><br /> Por exemplo, `dqsinstaller.exe -uninstall c:\DQSBackup.dqsb`|  
  
 **Para executar o DQSInstaller. exe do prompt de comando:**  
  
1.  Iniciar o prompt de comando.  
  
2.  Ao prompt de comando, altere seu diretório ao local onde DQSInstaller.exe está disponível. Se você tiver instalado a instância padrão do SQL Server, o arquivo DQSInstaller.exe estará disponível em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn:  
  
    ```  
    cd C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn  
    ```  
  
3.  No prompt de comando, execute DQSInstaller.exe com ou sem parâmetros de linha de comando:  
  
    -   **Sem o parâmetro de linha de comando**: digite `dqsinstaller.exe`e pressione Enter.  
  
    -   **Com o parâmetro de linha de comando**: digite o comando necessário, conforme mencionado na tabela acima, e pressione Enter.  
  
4.  As ações exigidas são executadas com base no comando especificado. Se você prefere instalar o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] sem parâmetros de linha de comando, o restante das etapas são as mesmas, conforme descrito nas etapas 2 a 6 na seção anterior, [Executar o DQSInstaller.exe na tela Iniciar, no menu Iniciar ou no Windows Explorer](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md#WindowsExplorer).  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   Conceda funções DQS apropriadas a usuários com base em seu perfil de trabalho. Veja [Conceder funções DQS a usuários](../../data-quality-services/install-windows/grant-dqs-roles-to-users.md).  
  
-   Se o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] será acessado remotamente do [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)], habilite o protocolo TCP/IP que usa SQL Server Configuration Manager neste computador.  
  
-   Verifique se você pode acessar seus dados de origem para as operações do DQS e se pode exportar os dados processados para uma tabela em um banco de dados. Veja [Acessar dados para as operações do DQS](../../data-quality-services/install-windows/access-data-for-the-dqs-operations.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar o Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [Atualizar assemblies SQLCLR após a atualização de .NET Framework](../../data-quality-services/install-windows/upgrade-sqlclr-assemblies-after-net-framework-update.md)   
 [Exportar e importar bases de dados de conhecimento do DQS usando o DQSInstaller. exe](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)  
  
  
