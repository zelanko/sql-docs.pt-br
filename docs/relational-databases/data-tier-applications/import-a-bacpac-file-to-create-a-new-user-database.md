---
title: Importar um arquivo BACPAC para criar um novo banco de dados de usuário | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: data-tier-applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-data-tier-apps
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb. importdac.results.f1
- sql13.swb.importdac.settings.f1
- sql13.swb.importdac.storagebrowser.f1
- sql13.swb.importdac.results.f1
- sql13.swb.importdac.progress.f1
- sql13.swb. importdac.summary.f1
- sql13.swb.importdac.summary.f1
- sql13.swb. importdac.progress.f1
- sql13.swb.importdac.welcome.f1
- sql13.swb. importdac.settings.f1
helpviewer_keywords:
- Data-tier application
- SQL Server DAC
- Migrate database
- DAC
ms.assetid: 736d8d9a-39f1-4bf8-b81f-2e56c134d12e
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 44f703190a26dd022d96ba1e94a156982bc01b72
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="import-a-bacpac-file-to-create-a-new-user-database"></a>Importar um arquivo BACPAC para criar um novo banco de dados de usuário
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Importar um arquivo DAC (aplicativo da camada de dados) – um arquivo .bacpac – para criar uma cópia do banco de dados original, com os dados, em uma nova instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)], ou para [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]. As operações de importação-exportação podem ser combinadas para migrar um DAC ou banco de dados entre instâncias ou para criar um backup lógico, como criar uma cópia no local de um banco de dados implantado no [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
## <a name="before-you-begin"></a>Antes de começar  
 O processo de importação compila um novo DAC em dois estágios.  
  
1.  A importação cria um novo DAC e o banco de dados associado usando a definição do DAC armazenada no arquivo de exportação, do mesmo modo que a implantação de um DAC cria um novo DAC a partir da definição em um arquivo de pacote do DAC.  
  
2.  A importação em massa copia os dados do arquivo de exportação.  
  
## <a name="sql-server-utility"></a>Utilitário do SQL Server  
 Se você importar um DAC para uma instância gerenciada do Mecanismo de Banco de Dados, o DAC importado será incorporado no Utilitário do SQL Server na próxima vez que o conjunto de coleta do utilitário for enviado da instância para o ponto de controle do utilitário. O DAC estará presente no nó **Aplicativos da Camada de Dados Implantados** do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **Utility Explorer** and reported in the **Aplicativos da Camada de Dados Implantados** details page.  
  
## <a name="database-options-and-settings"></a>Opções e configurações de banco de dados  
 Por padrão, o banco de dados criado durante a importação terá todas as configurações padrão da instrução CREATE DATABASE; a única diferença é que o agrupamento de banco de dados e o nível de compatibilidade são definidos como os valores estabelecidos no arquivo de exportação do DAC. Um arquivo de exportação do DAC usa os valores do banco de dados original.  
  
 Algumas opções de banco de dados, como TRUSTWORTHY, DB_CHAINING e HONOR_BROKER_PRIORITY, não podem ser ajustadas como parte do processo de importação. Propriedades físicas, como número de grupos de arquivos ou números e tamanhos de arquivos, não podem ser alteradas como parte do processo de importação. Após a importação, você pode usar a instrução ALTER DATABASE, o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell para personalizar o banco de dados. Para obter mais informações, consulte [Databases](../../relational-databases/databases/databases.md).  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Um DAC pode ser importado para o [!INCLUDE[ssSDS](../../includes/sssds-md.md)]ou uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que executa o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) ou posterior. Se você exportar um DAC de uma versão superior, o DAC poderá conter objetos sem suporte do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Você não pode implantar esses DACs nas instâncias do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
## <a name="prerequisites"></a>Prerequisites  
 Recomendamos que você não importe um arquivo de exportação do DAC de fontes desconhecidas ou não confiáveis. Esses arquivos podem conter código mal-intencionado que possivelmente executarão códigos Transact-SQL inesperados ou provocarão erros ao modificar o esquema. Antes de usar um arquivo de exportação de uma fonte desconhecida ou não confiável, desempacote o DAC e examine o código, como procedimentos armazenados e outro código definido pelo usuário. Para obter mais informações sobre como executar essas verificações, consulte [Validar um pacote de DAC](https://msdn.microsoft.com/library/ee633948(SQL.130).aspx).  
  
## <a name="security"></a>Segurança  
 Para melhorar a segurança, os logons de Autenticação do SQL Server são armazenados em um arquivo de exportação do DAC sem nenhuma senha. Quando o arquivo é importado, o logon é criado como um logon desabilitado com uma senha gerada. Para habilitar os logons, faça logon usando um logon que tenha a permissão de ALTER ANY LOGIN e use ALTER LOGIN para habilitar o logon e atribuir uma nova senha que possa ser comunicada ao usuário. Isso não é necessário para logons de Autenticação do Windows porque suas senhas não são gerenciadas pelo SQL Server.  
  
## <a name="permissions"></a>Permissões  
 Um DAC pode ser importado somente pelos membros das funções de servidor fixas **sysadmin** ou **serveradmin** , ou por logons que estejam na função de servidor fixa **dbcreator** e que tenham permissões ALTER ANY LOGIN. A conta interna do administrador de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chamada **sa** também pode importar um DAC. A importação de um DAC com logons no [!INCLUDE[ssSDS](../../includes/sssds-md.md)] exige associação nas funções loginmanager ou serveradmin. A importação de um DAC sem logons no [!INCLUDE[ssSDS](../../includes/sssds-md.md)] exige a associação nas funções dbmanager ou serveradmin.  
  
## <a name="using-the-import-data-tier-application-wizard"></a>Usando o Assistente para Importar Aplicativo da Camada de Dados  
 **Para iniciar o assistente, use as seguintes etapas:**  
  
1.  Conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], seja no local ou no [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
2.  Em **Pesquisador de Objetos**, clique com o botão direito do mouse em **Bancos de Dados**e selecione o item de menu **Importar Aplicativo da Camada de Dados** para iniciar o assistente.  
  
3.  Conclua as etapas das caixas de diálogo do assistente:  
  
    -   [Página de Introdução](#Introduction)  
  
    -   [Página Configurações de Importação](#Import_settings)  
  
    -   [Página Configurações de Banco de Dados](#Database_settings)  
  
    -   [Página de Resumo](#Summary)  
  
    -   [Página Progresso](#Progress)  
  
    -   [Página Resultados](#Results)  
  
###  <a name="Introduction"></a> Página de Introdução  
 Esta página descreve as etapas do Assistente de Importação do Aplicativo da Camada de Dados.  
  
 **Opções**  
  
-   **Não exibir esta página novamente.** – Clique nesta caixa de seleção para não exibir mais a página Introdução no futuro.  
  
-   **Avançar** – Continua na página **Configurações de Importação** .  
  
-   **Cancelar** – cancela a operação e fecha o assistente.  
  
###  <a name="Import_settings"></a> Página Configurações de Importação  
 Use essa página para especificar a localização do arquivo .bacpac a ser importado.  
  
-   **Importar de disco local** – Clique em **Procurar…** para navegar no computador local ou especifique o caminho no espaço fornecido. O nome do caminho deve incluir um nome de arquivo e a extensão .bacpac.  
  
-   **Importar do Azure** – importa um arquivo BACPAC de um contêiner do Microsoft Azure. É necessário se conectar a um contêiner do Microsoft Azure para validar esta opção. Observe que esta opção também exige que você especifique um diretório local para o arquivo temporário. O arquivo temporário será criado no local especificado e permanecerá lá após a conclusão da operação.  
  
     Ao procurar o Azure, você poderá mudar entre contêineres em uma única conta. Você deve especificar um único arquivo .bacpac para continuar a operação de importação. Observe que você pode classificar colunas por **Nome**, **Tamanho**ou **Data da Modificação**.  
  
     Para continuar, especifique o arquivo .bacpac a ser importado e clique em **Abrir**.  
  
###  <a name="Database_settings"></a> Página Configurações de Banco de Dados  
 Use essa página para especificar detalhes do banco de dados que será criado.  
  
 **Para uma instância local do SQL Server:**  
  
-   **Nome do novo banco de dados** – Forneça um nome para o banco de dados importado.  
  
-   **Caminho do arquivo de dados** – Forneça um diretório local para arquivos de dados. Clique em **Procurar…** para navegar no computador local ou especifique o caminho no espaço fornecido.  
  
-   **Caminho do arquivo de log** – Forneça um diretório local para arquivos de log. Clique em **Procurar…** para navegar no computador local ou especifique o caminho no espaço fornecido.  
  
 Para continuar, clique em **Avançar**.  
  
 **Para um Banco de Dados SQL do Azure:**  
  
 - **[Importar um arquivo BACPAC para criar um novo banco de dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-import/)** fornece instruções passo a passo sobre como usar o portal do Azure, PowerShell, SSMS ou SqlPackage.  
 - Consulte **[Opções e desempenho do Banco de Dados SQL: Entender o que está disponível em cada camada de serviço](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)** para obter uma visão detalhada das diferentes camadas de serviço.  

### <a name="validation-page"></a>Página de Validação  
 Use esta página para revisar os problemas que bloqueiam a operação. Para continuar, resolva os problemas de bloqueio e clique em **Executar Novamente a Validação** para verificar se a validação foi bem-sucedida.  
  
 Para continuar, clique em **Avançar**.  
  
###  <a name="Summary"></a> Página de Resumo  
 Use esta página para analisar a origem especificada e as configurações de destino para a operação. Para concluir a operação de importação usando as configurações especificadas, clique em **Concluir**. Para cancelar a operação de importação e sair do assistente, clique em **Cancelar**.  
  
###  <a name="Progress"></a> Página Progresso  
 Esta página exibe a barra de progresso que indica o status da operação. Para exibir o status detalhado, clique na opção **Exibir detalhes** .  
  
 Para continuar, clique em **Avançar**.  
  
###  <a name="Results"></a> Página Resultados  
 Esta página relata o êxito ou a falha das operações de importação e criação de bancos de dados, mostrando o êxito ou a falha de cada ação. Todas as ações que encontrarem um erro terão um link na coluna **Resultado** . Clique no link para exibir um relatório do erro para essa ação.  
  
 Clique em **Fechar** para fechar o assistente.  
  
## <a name="see-also"></a>Consulte Também  
[Importar um arquivo BACPAC para criar um novo banco de dados SQL do Azure](https://azure.microsoft.com/en-us/documentation/articles/sql-database-import/)  
 [Aplicativos da Camada de Dados](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Exportar um aplicativo da camada de dados](../../relational-databases/data-tier-applications/export-a-data-tier-application.md)  
  
  
