---
title: Fazer upgrade do Data Quality Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: f396666b-7754-4efc-9507-0fd114cc32d5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5c76fda112acae7b8a9314d217f5c32d197e87f9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62775626"
---
# <a name="upgrade-data-quality-services"></a>Atualizar o Data Quality Services
  Este tópico fornece informações sobre como atualizar sua instalação existente do Data Quality Services (DQS) para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2. Como parte de atualizar seu Data Quality Server no DQS para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], você também deverá atualizar o esquema de bancos de dados do DQS.  
  
> [!IMPORTANT]
>  -   Você deve fazer backup de seus bancos de dados do DQS antes de atualizar o DQS para impedir qualquer perda de dados acidental durante a atualização do esquema. Para obter informações sobre como fazer backup de bancos de dados DQS, veja [Fazendo backup e restaurando banco de dados do DQS](../../data-quality-services/backing-up-and-restoring-dqs-databases.md).  
> -   Você pode se conectar à versão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do Data Quality Server usando a versão atual ou anterior do Cliente Data Quality ou a [Transformação de Limpeza DQS](../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md) no Integration Services para executar suas tarefas de qualidade de dados.  
> -   Você pode continuar a usar a versão do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 do suplemento Master Data Services para Excel depois de atualizar o Data Quality Services e o Master Data Services para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2. No entanto, qualquer versão anterior do suplemento Master Data Services para Excel não funcionará depois de atualizar para o SQL Server 2014 CTP2. Você pode baixar a versão do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 do suplemento Master Data Services para Excel [aqui](https://go.microsoft.com/fwlink/?LinkId=328664).  
  
##  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Você deve estar conectado como um membro do grupo Administradores no computador do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] .  
  
-   Sua conta de usuário do Windows deve ser um membro da função de servidor fixa sysadmin na instância do SQL Server em que o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] está instalado.  
  
##  <a name="Upgrade"></a> Atualizando o DQS  
 Para atualizar o DQS:  
  
1.  Faça backup de seus bancos de dados do DQS antes de iniciar o processo de atualização. Para obter informações sobre como fazer backup de bancos de dados DQS, veja [Fazendo backup e restaurando banco de dados do DQS](../../data-quality-services/backing-up-and-restoring-dqs-databases.md).  
  
2.  Atualizar a instância do SQL Server onde o DQS está instalado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    1.  Execute o assistente de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
    2.  No painel esquerdo, clique em **Instalação**.  
  
    3.  No painel direito, clique em **Atualizar do SQL Server 2005, SQL Server 2008, SQL Server 2008 R2 ou SQL Server 2012**.  
  
    4.  Conclua o assistente de Instalação.  
  
        > [!NOTE]  
        >  Isso atualizará a instância do SQL Server para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e também instalará o último Cliente Data Quality, caso o Cliente Data Quality tenha sido instalado anteriormente neste computador. Se você tiver o Cliente Data Quality instalado em outros computadores, execute as etapas secundárias na Etapa 2 nesses computadores para instalar a versão atual do Cliente Data Quality. O assistente de instalação instala a versão atual do Cliente Data Quality próximo à versão existente do Cliente Data Quality. Depois de você atualizar o esquema de bancos de dados do DQS, você pode se conectar à versão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do Data Quality Server usando a versão atual ou anterior do Cliente Data Quality.  
  
3.  Atualize o esquema de banco de dados do DQS.  
  
    1.  Inicie o prompt de comando como administrador.  
  
    2.  Ao prompt de comando, altere seu diretório ao local onde DQSInstaller.exe está disponível. Para a instância padrão do SQL Server, o arquivo DQSInstaller.exe estará disponível em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn:  
  
        ```  
        cd C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn  
        ```  
  
    3.  No prompt de comando, digite o seguinte comando e pressione ENTER:  
  
        ```  
        dqsinstaller.exe -upgrade  
        ```  
  
    4.  O instalador solicita que você faça backup dos bancos de dados do DQS antes de continuar. Se você já tiver feito backup dos bancos de dados do DQS, digite `Y` ou `Yes`e pressione ENTER para continuar com a atualização.  
  
    5.  Uma mensagem de conclusão é exibida depois da atualização bem-sucedida do esquema de bancos de dados do DQS.  
  
##  <a name="Verify"></a> Verificando a atualização do esquema de banco de dados do DQS  
 Para verificar se o esquema de banco de dados do DQS foi atualizado com êxito, você poderá verificar a versão atual nos bancos de dados DQS_MAIN e DQS_PROJECTS consultando a tabela A_DB_VERSION em cada banco de dados. Para fazer isso:  
  
1.  Inicie o SQL Server Management Studio e conecte-se à instância do SQL Server que contém o esquema de banco de dados do DQS atualizado.  
  
2.  Execute a seguinte consulta:  
  
    ```  
    SELECT * FROM DQS_MAIN.dbo.A_DB_VERSION WHERE STATUS=2;  
    SELECT * FROM DQS_PROJECTS.dbo.A_DB_VERSION WHERE STATUS=2;  
    ```  
  
3.  A saída exibirá uma entrada para cada atualização junto com a data da atualização. O VERSION_ID e ASSEMBLY_VERSION máximo na última data é a versão atual. Um valor de 2 na coluna STATUS indica êxito. Se um erro ocorreu, o erro será listado na coluna ERROR. Uma saída de exemplo:  
  
    |ID|UPGRADE_DATE|VERSION_ID|ASSEMBLY_VERSION|USER_NAME|STATUS|ERROR|  
    |--------|-------------------|-----------------|-----------------------|----------------|------------|-----------|  
    |1000|2013-08-11 05:26:39.567|1.200|11.0.3000.0|\<DOMAIN\UserName>|2||  
    |1001|2013-09-19 15:09:37.750|1600|12.0.xxxx.0|\<DOMAIN\UserName>|2||  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar o Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [Remover objetos do Data Quality Server](../../sql-server/install/remove-data-quality-server-objects.md)   
 [Atualizar para o SQL Server 2014](upgrade-sql-server.md)  
  
  
