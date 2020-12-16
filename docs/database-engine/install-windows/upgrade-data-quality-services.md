---
title: Fazer upgrade do Data Quality Services | Microsoft Docs
description: Este artigo fornece informações sobre como atualizar a instalação existente do SQL Server DQS (Data Quality Services).
ms.custom: ''
ms.date: 06/29/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: f396666b-7754-4efc-9507-0fd114cc32d5
author: cawrites
ms.author: chadam
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 1be8d8e6b320af96bc3acf7a28ec2c017a92914a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480317"
---
# <a name="upgrade-data-quality-services"></a>Atualizar o Data Quality Services

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]

Este artigo fornece informações sobre como fazer upgrade da instalação existente do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] DQS (Data Quality Services). Como parte do upgrade do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Data Quality Server, você também deverá fazer upgrade do esquema de bancos de dados do DQS.  
  
> [!IMPORTANT]
>  -   Você deve fazer backup de seus bancos de dados do DQS antes de atualizar o DQS para impedir qualquer perda de dados acidental durante a atualização do esquema. Para obter informações sobre como fazer backup de bancos de dados DQS, veja [Fazendo backup e restaurando banco de dados do DQS](../../data-quality-services/backing-up-and-restoring-dqs-databases.md).  
> -   Conecte-se ao [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Data Quality Server usando a versão atual ou uma versão anterior do Data Quality Client ou a [Transformação de Limpeza DQS](../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md) no Integration Services para executar suas tarefas de qualidade de dados.  
> -   Depois de fazer upgrade do Data Quality Services e do Master Data Services, uma versão anterior do Suplemento Master Data Services para Excel deixará de funcionar. Você pode baixar a versão [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] do suplemento Master Data Services para Excel [aqui](../../master-data-services/master-data-services-installation-and-configuration.md).  
  
##  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
  
-   Você deve estar conectado como um membro do grupo Administradores no computador do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] .  
  
-   Sua conta de usuário do Windows deve ser um membro da função de servidor fixa sysadmin na instância do SQL Server em que o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] está instalado.  
  
##  <a name="upgrading-dqs"></a><a name="Upgrade"></a> Atualizando o DQS  
 Para atualizar o DQS:  
  
1.  Faça backup de seus bancos de dados do DQS antes de iniciar o processo de atualização. Para obter informações sobre como fazer backup de bancos de dados DQS, veja [Fazendo backup e restaurando banco de dados do DQS](../../data-quality-services/backing-up-and-restoring-dqs-databases.md).  
  
2.  Faça upgrade da instância do SQL Server na qual o DQS está instalado.  
  
    1.  Execute o assistente de instalação do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] .  
  
    2.  No painel esquerdo, clique em **Instalação**.  
  
    3.  No painel direito, clique em **Fazer upgrade de...** uma versão anterior do SQL Server.  
  
    4.  Conclua o assistente de Instalação.  
  
        > [!NOTE]  
        >  Isso atualizará a instância do SQL Server para o [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] e também instalará o último Cliente Data Quality, caso o Cliente Data Quality tenha sido instalado anteriormente neste computador. Se você tiver o Cliente Data Quality instalado em outros computadores, execute as etapas secundárias na Etapa 2 nesses computadores para instalar a versão atual do Cliente Data Quality. O assistente de instalação instala a versão atual do Cliente Data Quality próximo à versão existente do Cliente Data Quality. Depois de você atualizar o esquema de bancos de dados do DQS, você pode se conectar à versão do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] do Data Quality Server usando a versão atual ou anterior do Cliente Data Quality.  
  
3.  Atualize o esquema de banco de dados do DQS.  
  
    1.  Inicie o prompt de comando como administrador.  
  
    2.  Ao prompt de comando, altere seu diretório ao local onde DQSInstaller.exe está disponível. Para a instância padrão do SQL Server, o arquivo DQSInstaller.exe está disponível em C:\Program Files\Microsoft SQL Server\MSSQL[nn].MSSQLSERVER\MSSQL\Binn:  

        >[!NOTE]
        >No caminho da pasta, substitua [nn] pelo número de versão do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].
        >- Para o SQL Server 2016: 13
        >- Para o SQL Server 2017: 14
    
        ```console
        cd C:\Program Files\Microsoft SQL Server\MSSQL[nn].MSSQLSERVER\MSSQL\Binn  
        ```  
  
    3.  No prompt de comando, digite o seguinte comando e pressione ENTER:  
  
        ```console
        dqsinstaller.exe -upgrade  
        ```  
  
    4.  O instalador solicita que você faça backup dos bancos de dados do DQS antes de continuar. Se você já tiver feito backup de seus bancos de dados do DQS, digite **Y** ou **Sim** e pressione ENTER para continuar com a atualização.  
  
    5.  Uma mensagem de conclusão é exibida depois da atualização bem-sucedida do esquema de bancos de dados do DQS.  
  
##  <a name="verifying-the-dqs-databases-schema-upgrade"></a><a name="Verify"></a> Verificando a atualização do esquema de banco de dados do DQS  
 Para verificar se o esquema de banco de dados do DQS foi atualizado com êxito, você poderá verificar a versão atual nos bancos de dados DQS_MAIN e DQS_PROJECTS consultando a tabela A_DB_VERSION em cada banco de dados. Para fazer isso:  
  
1.  Inicie o SQL Server Management Studio e conecte-se à instância do SQL Server que contém o esquema de banco de dados do DQS atualizado.  
  
2.  Execute a seguinte consulta:  
  
    ```sql
    SELECT * FROM DQS_MAIN.dbo.A_DB_VERSION WHERE STATUS=2;  
    SELECT * FROM DQS_PROJECTS.dbo.A_DB_VERSION WHERE STATUS=2;  
    ```  
  
3.  A saída exibirá uma entrada para cada atualização junto com a data da atualização. O VERSION_ID e ASSEMBLY_VERSION máximo na última data é a versão atual. Um valor de 2 na coluna STATUS indica êxito. Se um erro ocorreu, o erro será listado na coluna ERROR. Uma saída de exemplo:  
  
    |ID|UPGRADE_DATE|VERSION_ID|ASSEMBLY_VERSION|USER_NAME|STATUS|ERROR|  
    |--------|-------------------|-----------------|-----------------------|----------------|------------|-----------|  
    |1000|2013-08-11 05:26:39.567|1200|11.0.3000.0|\<DOMAIN\UserName>|2||  
    |1001|2013-09-19 15:09:37.750|1600|12.0.xxxx.0|\<DOMAIN\UserName>|2||  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar o Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [Remover objetos do Data Quality Server](../../sql-server/install/remove-data-quality-server-objects.md)   
 [Atualizar o SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)  
  
