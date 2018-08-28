---
title: Auditoria local da coleta de comentários sobre o uso do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Local Audit
ms.assetid: a0665916-7789-4f94-9086-879275802cf3
caps.latest.revision: 8
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: 5f432f23edf8c7cffff880112e9c6d22031d83fb
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40405270"
---
# <a name="local-audit-for-sql-server-usage-feedback-collection"></a>Auditoria Local da coleta de comentários sobre o uso do SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

## <a name="introduction"></a>Introdução

O Microsoft SQL Server contém recursos habilitados para Internet que podem coletar e enviar à Microsoft informações sobre seu computador ou dispositivo. Isso é chamado de *informações padrão do computador*. O componente de Auditoria Local da [Coleta de comentários sobre o uso do SQL Server](http://support.microsoft.com/kb/3153756) grava dados coletados pelo serviço em uma pasta designada, que representa os dados (logs) que serão enviados à Microsoft. A finalidade da Auditoria Local é permitir que os clientes vejam todos os dados que a Microsoft coleta com esse recurso, para fins de conformidade, regulatórios ou de validação de privacidade.  

Desde o SQL Server 2016 CU2, a Auditoria Local é configurável no nível da instância no Mecanismo de Banco de Dados do SQL Server e o SSAS (Analysis Services). No SQL Server 2016 CU4 e no SQL Server 2016 SP1, a Auditoria Local também está habilitada para o SQL Server Integration Services (SSIS). Outros componentes do SQL Server que são instalados durante a instalação e as ferramentas do SQL Server que são baixadas ou instaladas após a instalação não têm o recurso de Auditoria Local para coleta de comentários sobre uso. 

## <a name="prerequisites"></a>Prerequisites 

A seguir estão os pré-requisitos para habilitar a Auditoria Local em cada instância do SQL Server: 

1. A instância está corrigida para o SQL Server 2016 RTM CU2 ou posterior. Para o Integration Services, a instância é corrigida para o SQL 2016 RTM CU4 ou SQL 2016 SP1

1. O usuário deve ser um administrador do sistema ou ter uma função com acesso para adicionar e modificar a Chave do Registro, criar pastas, gerenciar a segurança das pastas e parar/iniciar um Serviço do Windows.  

## <a name="pre-configuration-steps-prior-to-turning-on-local-audit"></a>Etapas de pré-configuração antes de ativar a Auditoria Local 

Antes de ativar a Auditoria Local, um administrador do sistema deve:

1. Conhecer o nome da instância do SQL Server e a conta de logon do serviço de telemetria do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server. 

1. Configurar uma nova pasta para os arquivos de Auditoria Local.

1. Conceder permissões para a conta de logon do serviço de telemetria do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server.

1. Criar uma configuração de chave do registro para configurar o diretório de destino da Auditoria Local. 


### <a name="get-the-sql-server-ceip-service-logon-account"></a>Obter a conta de logon de serviço do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server 

Execute as seguintes etapas para obter a conta de logon do serviço de telemetria do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server
 
1. Inicie o console **Serviços**. Para fazer isso, selecione a **tecla Windows + R** no teclado para abrir a caixa de diálogo **Executar**. Em seguida, digite *services.msc* no campo de texto e selecione **OK** para iniciar o console **Serviços**.  

2. Navegue até o serviço apropriado. Por exemplo, para o mecanismo de banco de dados, localize o **Serviço do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server** **(*nome da instância*)**. Para o Analysis Services, localize **Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server Analysis Services** **(*nome da instância*)**. Para o Integration Services, localize o **serviço do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server Integration Services**.

3. Clique com o botão direito do mouse no serviço e escolha **Propriedades**. 

4. Selecione na guia **Logon**. A conta de Logon está listada em **Esta Conta**. 

### <a name="configure-a-new-folder-for-the-local-audit-files"></a>Configurar uma nova pasta para os arquivos de Auditoria Local.    

Crie uma nova pasta (Diretório da Auditoria Local) em que a Auditoria Local gravará os logs. Por exemplo, o caminho completo para o Diretório da Auditoria Local para uma instância padrão do mecanismo de banco de dados seria: *C:\\SQLCEIPAudit\\MSSQLSERVER\\DB\\*. 
 
  >[!NOTE] 
  >Configure o caminho do diretório da Auditoria Local fora do caminho de instalação do SQL Server para evitar que a funcionalidade de auditoria e a aplicação de patches causem problemas com o SQL Server.

  ||Decisão de design|Recomendação|  
  |------|-----------------|----------|  
  |![Caixa de seleção](../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Disponibilidade de espaço |Com uma carga de trabalho moderada com cerca de 10 bancos de dados, planeje ter cerca de 2 MB de espaço em disco por banco de dados por instância.|  
|![Caixa de seleção](../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Diretórios separados | Crie um diretório para cada instância. Por exemplo, use *C:\\SQLCEIPAudit\\MSSQLSERVER\\DB\\* para uma instância do SQL Server chamada `MSSQLSERVER`. Isso simplifica o gerenciamento de arquivos.
|![Caixa de seleção](../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Pastas separadas |Use uma pasta específica para cada serviço. Por exemplo, para um determinado nome de instância, tenha uma pasta para o mecanismo de banco de dados. Se uma instância do Analysis Services usar o mesmo nome de instância, crie uma pasta separada para o Analysis Services. Ter instâncias do Mecanismo de Banco de Dados e do Analysis Services configuradas para a mesma pasta fará com que a Auditoria Local grave no mesmo arquivo de log para as duas instâncias.| 
|![Caixa de seleção](../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Conceder permissões para a conta de logon do serviço de telemetria do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server|Habilite acesso para **Listar Conteúdo da Pasta**, **Ler** e **Gravar** à conta de logon do serviço de telemetria do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server|


### <a name="grant-permissions-to-the-sql-server-ceip-telemetry-service-logon-account"></a>Conceder permissões para a conta de logon do serviço de telemetria do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server
  
1. No **Explorador de Arquivos**, navegue até o local em que a nova pasta está localizada.

1. Clique com o botão direito do mouse na nova pasta e escolha **Propriedades**. 

1. Na guia **Segurança**, selecione **Editar** e gerenciar Permissão.

1. Selecione **Adicionar** e digite as credenciais do Serviço de Telemetria do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server. Por exemplo, `NT Service\SQLTELEMETRY`.

1. Selecione **Verificar Nomes** para validar o nome fornecido e selecione **OK**.

1. Na caixa de diálogo **Permissão**, escolha a conta de logon ao Serviço de Telemetria do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server e selecione **Listar conteúdo da pasta**, **Ler** e **Gravar**.

1. Selecione **OK** para aplicar as alterações de permissão imediatamente. 
  
### <a name="create-a-registry-key-setting-to-configure-local-audit-target-directory"></a>Criar uma configuração de chave do Registro para configurar o diretório de destino da Auditoria Local

1. Inicie o regedit.

1. Navegue até o caminho do CPE apropriado:

   | Versão | ***Mecanismo de banco de dados*** – chave do Registro |
   | :------ | :----------------------------- |
   | 2016    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSSQL**13**.*nome da instância*\\CPE |
   | 2017    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSSQL**14**.*nome da instância*\\CPE |
   | &nbsp; | &nbsp; |

   | Versão | ***Analysis Services*** – chave do Registro |
   | :------ | :------------------------------- |
   | 2016    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSAS**13**.*nome da instância*\\CPE |
   | 2017    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSAS**14**.*nome da instância*\\CPE |
   | &nbsp; | &nbsp; |

  | Versão | ***Integration Services*** – chave do Registro |
  | :------ | :---------------------------------- |
  | 2016    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\**130** |
  | 2017    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\**140** |
  | &nbsp; | &nbsp; |

1. Clique com o botão direito do mouse no caminho do CPE e escolha **Novo**. Selecione **Valor de cadeia de caracteres**.

1. Nomeie a nova chave do Registro `UserRequestedLocalAuditDirectory`. 
 
## <a name="turning-local-audit-on-or-off"></a>Ativando ou desativando a Auditoria Local

Depois de concluir as etapas de pré-configuração, você pode ativar a Auditoria Local. Para fazer isso, use uma conta de administrador do sistema ou com uma função semelhante com acesso para modificar chaves de registro para ativar ou desativar a Auditoria Local seguindo as etapas abaixo. 

1. Inicie o **regedit**.  

1. Navegue até o [caminho](#create-a-registry-key-setting-to-configure-local-audit-target-directory) do CPE apropriado. 

1. Clique com o botão direito do mouse em **UserRequestedLocalAuditDirectory** e selecione *Modificar*. 

1. Para ativar a Auditoria Local, digite o caminho da Auditoria Local, por exemplo, *C:\\SQLCEIPAudit\\MSSQLSERVER\\DB\\*.
 
    Para desativar a Auditoria Local, esvazie o valor em **UserRequestedLocalAuditDirectory**.

1. Feche o **regedit**. 

O Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server deve reconhecer a configuração da Auditoria Local imediatamente se o serviço já estiver em execução. Para iniciar o serviço do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server, o administrador do sistema ou alguém que tenha acesso para iniciar ou parar Serviços do Windows pode seguir as etapas abaixo: 

1. Inicie o console **Serviços**. Para fazer isso, selecione a **tecla Windows + R** no teclado para abrir a caixa de diálogo **Executar**. Em seguida, digite *services.msc* no campo de texto e selecione **OK** para iniciar o console **Serviços**.  

1. Navegue até o serviço apropriado. 

    - Para o Mecanismo de Banco de Dados, use **Serviço do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server (*nome da instância*)**.     
    - Para o Analysis Services, use **Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server Analysis Services (*nome da instância*)**.
    - Para o Integration Services, 
        - Para o SQL 2016, use *Serviço do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server Integration Services 13.0*.
        - Para o SQL 2017, use *Serviço do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server Integration Services 14.0*.

1. Clique com o botão direito do mouse no serviço e escolha Reiniciar. 

1. Verifique se o status do serviço é **Executando**. 

A Auditoria Local produzirá um arquivo de log por dia. Os arquivos de log estarão na forma de `<YYYY-MM-DD>.json`. Por exemplo, *2016-07-12.json*. Se houver um arquivo existente para o dia no diretório designado, a Auditoria Local acrescentará a ele. Caso contrário, criará um novo arquivo para o dia. 

  >[!NOTE]
  > Após habilitar a Auditoria Local, pode levar até 5 minutos para que o arquivo de log seja gravado pela primeira vez. 

## <a name="maintenance"></a>Manutenção 

1. Para limitar o uso do espaço em disco pelos arquivos gravados pela Auditoria Local, configure uma política ou um trabalho regular para limpar o Diretório da Auditoria Local para remover arquivos antigos e desnecessários.  

2. Proteja o caminho do Diretório da Auditoria Local para que ele seja acessível apenas para as pessoas apropriadas. Observe que os arquivos de log contêm as informações descritas em [Como configurar o SQL Server 2016 para enviar comentários à Microsoft](http://support.microsoft.com/kb/3153756). O acesso a este arquivo deve impedir que a maioria dos membros de sua organização o leiam.  

## <a name="data-dictionary-of-local-audit-output-data-structure"></a>Dicionário de dados da estrutura de dados de saída da Auditoria Local 

- Os arquivos de log da Auditoria Local estão em JSON, contendo um conjunto de objetos (linhas) que representam pontos de dados que são enviados de volta para a Microsoft em **emitTime**.
- Cada linha segue um esquema específico identificado por **schemaVersion**.
- Cada linha é uma saída de uma sessão de serviços SQLCEIP identificada como **sessionID**.
- As linhas são emitidas em sequência, identificadas por **sequence**.
- Cada linha de ponto de dados contém a saída de um **queryIdentifier**, que pode ser uma consulta T-SQL, uma sessão XE ou uma mensagem relacionada a um tipo de rastreamento, identificado como **traceName**.
- **queryIdentifiers** são agrupados e sua versão é controlada em conjunto com **querySetVersion**.
- **data** contêm a saída da execução da consulta correspondente que levou **queryTimeInTicks**.
- **queryIdentifiers** para consultas T-SQL têm a definição da consulta T-SQL armazenada na consulta.

| Hierarquia lógica de informações da Auditoria Local | Colunas relacionadas |
| ------ | -------|
| Cabeçalho | emitTime, schemaVersion 
| Computador | operatingSystem 
| Instância | instanceUniqueID, correlationID, clientVersion 
| Session | sessionID, traceName 
| Consulta | sequence, querySetVersion, queryIdentifier, query, queryTimeInTicks 
| data |  data 

### <a name="namevalue-pairs-definition-and-examples"></a>Definição e exemplos de pares nome/valor 

As colunas listadas abaixo representam a ordem da saída de arquivos da Auditoria Local. Hash unidirecional com SHA 256 é usado para valores mantidos em anonimato para várias das colunas abaixo.  

| Nome | Descrição | Valores de exemplo
|-------|--------| ----------|
|instanceUniqueID| Identificador da instância em anonimato | 888770C4D5A8C6729F76F33D472B28883AE518C92E1999888B171A085059FD 
|schemaVersion| Versão do esquema do SQLCEIP |  3 
|emitTime |Hora de emissão do ponto de dados em UTC | 2016-09-08T17:20:22.1124269Z 
|sessionID | Identificador da sessão para o serviço do SQLCEIP | 89decf9a-ad11-485c-94a7-fefb3a02ed86 
|correlationId | Espaço reservado para um identificador adicional | 0 
|sequence | Número de sequência de pontos de dados enviados dentro da sessão | 15 
|clientVersion | Versão da instância do SQL Server | 13.0.2161.3 ((SQL16_RTM_QFE-CU).160907-1223) 
|operatingSystem | A versão do sistema operacional em que a instância do SQL Server está instalada | Microsoft Windows Server 2012 R2 Datacenter 
|querySetVersion | Versão de um grupo de definições de consulta | 1.0.0.0 
|traceName | Categorias de rastreamentos: (SQLServerXeQueries, SQLServerPeriodicQueries, SQLServerOneSettingsException) | SQLServerPeriodicQueries 
|queryIdentifier | Um identificador da consulta | SQLServerProperties.002 
|data   | A saída das informações coletadas em queryIdentifier como uma saída de uma consulta T-SQL, sessão XE ou do aplicativo |  [{"Collation": "SQL_Latin1_General_CP1_CI_AS","SqlFTinstalled": "0" "SqlIntSec": "1","IsSingleUser": "0","SqlFilestreamMode": "0","SqlPbInstalled": "0","SqlPbNodeRole": "","SqlVersionMajor": "13","SqlVersionMinor": "0","SqlVersionBuild": "2161","ProductBuildType": "","ProductLevel": "RTM","ProductUpdateLevel": "CU2","ProductUpdateReference": "KB3182270","ProductRevision": "3","SQLEditionId": "-1534726760","IsClustered": "0","IsHadrEnabled": "0","SqlAdvAInstalled": "0","PacketReceived": "1210","Version": "Microsoft SQL Server 2016 (RTM-CU2) (KB3182270) - 13.0.2161.3 (X64) \n\tSep  7 2016 14:24:16 \n\tCopyright (c) Microsoft Corporation\n\tStandard Edition (64-bit) on Windows Server 2012 R2 Datacenter 6.3 \u003cX64\u003e (Build 9600: ) (Hypervisor)\n"}],
|Consulta| Se aplicável, a definição da consulta T-SQL relacionada com o queryIdentifier que produz os dados.        Este componente não é carregado pelo serviço do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server. Ele está incluído na Auditoria Local apenas como uma referência para os clientes.| SELECT\n      SERVERPROPERTY(\u0027Collation\u0027) AS [Collation],\n      SERVERPROPERTY(\u0027IsFullTextInstalled\u0027) AS [SqlFTinstalled],\n      SERVERPROPERTY(\u0027IsIntegratedSecurityOnly\u0027) AS [SqlIntSec],\n      SERVERPROPERTY(\u0027IsSingleUser\u0027) AS [IsSingleUser],\n      SERVERPROPERTY (\u0027FileStreamEffectiveLevel\u0027) AS [SqlFilestreamMode],\n      SERVERPROPERTY(\u0027IsPolybaseInstalled\u0027) AS [SqlPbInstalled],\n      SERVERPROPERTY(\u0027PolybaseRole\u0027) AS [SqlPbNodeRole],\n      SERVERPROPERTY(\u0027ProductMajorVersion\u0027) AS [SqlVersionMajor],\n      SERVERPROPERTY(\u0027ProductMinorVersion\u0027) AS [SqlVersionMinor],\n      SERVERPROPERTY(\u0027ProductBuild\u0027) AS [SqlVersionBuild],\n      SERVERPROPERTY(\u0027ProductBuildType\u0027) AS ProductBuildType,\n      SERVERPROPERTY(\u0027ProductLevel\u0027) AS ProductLevel,\n      SERVERPROPERTY(\u0027ProductUpdateLevel\u0027) AS ProductUpdateLevel,\n      SERVERPROPERTY(\u0027ProductUpdateReference\u0027) AS ProductUpdateReference,\n      RIGHT(CAST(SERVERPROPERTY(\u0027ProductVersion\u0027) AS NVARCHAR(30)),CHARINDEX(\u0027.\u0027, REVERSE(CAST(SERVERPROPERTY(\u0027ProductVersion\u0027) AS NVARCHAR(30)))) - 1) AS ProductRevision,\n      SERVERPROPERTY(\u0027EditionID\u0027) AS SQLEditionId,\n      SERVERPROPERTY(\u0027IsClustered\u0027) AS IsClustered,\n      SERVERPROPERTY(\u0027IsHadrEnabled\u0027) AS IsHadrEnabled,\n      SERVERPROPERTY(\u0027IsAdvancedAnalyticsInstalled\u0027) AS [SqlAdvAInstalled],\n      @@PACK_RECEIVED AS PacketReceived,\n      @@VERSION AS Version
|queryTimeInTicks | A duração necessária para que a consulta com a seguinte categoria de rastreamento seja executada: (SQLServerXeQueries, SQLServerPeriodicQueries) |  0 
 
### <a name="trace-categories"></a>Categorias de rastreamento 
Atualmente, coletamos as seguintes categorias de rastreamento: 

- **SQLServerXeQueries**: contém pontos de dados coletados por meio da sessão de Evento Estendido.
- **SQLServerPeriodicQueries**: contém pontos de dados coletados por meio de consultas periódicas executadas em uma instância do SQL Server.
- **SQLServerPerDBPeriodicQueries**: contém pontos de dados coletados por meio de consultas periódicas executadas em até 30 bancos de dados em uma instância do SQL Server.
- **SQLServerOneSettingsException**: contém mensagens de exceção relacionadas à atualização do esquema e/ou do conjunto de consultas.
- **DigitalProductID**: contém pontos de dados para agregar IDs de produtos digitais com hash (SHA-256) anônimos de instâncias do SQL Server. 

### <a name="local-audit-file-examples"></a>Exemplos de arquivos da Auditoria Local



Abaixo, temos um trecho de uma saída de arquivo JSON da Auditoria Local.

```JSON
[
  {
    "instanceUniqueId": "888770C4D5A8C6729F76F33D472B28883AE518C92E1999888B171A085059FD",
    "isSSEIInstance": "0",
    "schemaVersion": "5",
    "emitTime": "2018-05-04T15:27:59.7031518Z",
    "sessionId": "c3cd1b56-ab61-462f-8363-8881779aa223",
    "correlationId": 0,
    "sequence": 18,
    "clientVersion": "14.0.3025.34 ((SQLServer2017-CU6).180410-0033)",
    "isInternalMachine": "1",
    "operatingSystem": "Microsoft Windows 10 Enterprise",
    "querySetVersion": "14.0.3025.34",
    "traceName": "SQLServerPeriodicQueries",
    "queryIdentifier": "SQLServerProperties.002",
    "data": [
      {
        "Collation": "SQL_Latin1_General_CP1_CI_AS",
        "SqlFTinstalled": "0",
        "SqlIntSec": "1",
        "IsSingleUser": "0",
        "SqlFilestreamMode": "2",
        "SqlPbInstalled": "1",
        "SqlPbNodeRole": "Head",
        "SqlVersionMajor": "14",
        "SqlVersionMinor": "0",
        "SqlVersionBuild": "3025",
        "ProductBuildType": "",
        "ProductLevel": "RTM",
        "ProductUpdateLevel": "CU6",
        "ProductUpdateReference": "KB4101464",
        "ProductRevision": "34",
        "SQLEditionId": "1872460670",
        "IsClustered": "0",
        "IsHadrEnabled": "0",
        "SqlAdvAInstalled": "1",
        "PacketReceived": "422",
        "Version": "Microsoft SQL Server 2017 (RTM-CU6) (KB4101464) - 14.0.3025.34 (X64) \n\tApr  9 2018 18:00:41 \n\tCopyright (C) 2017 Microsoft Corporation\n\tEnterprise Edition: Core-based Licensing (64-bit) on Windows 10 Enterprise 10.0 <X64> (Build 16299: )\n"
      }
    ],
    "query": "SELECT\n      SERVERPROPERTY('Collation') AS [Collation],\n      SERVERPROPERTY('IsFullTextInstalled') AS [SqlFTinstalled],\n      SERVERPROPERTY('IsIntegratedSecurityOnly') AS [SqlIntSec],\n      SERVERPROPERTY('IsSingleUser') AS [IsSingleUser],\n      SERVERPROPERTY ('FileStreamEffectiveLevel') AS [SqlFilestreamMode],\n      SERVERPROPERTY('IsPolybaseInstalled') AS [SqlPbInstalled],\n      SERVERPROPERTY('PolybaseRole') AS [SqlPbNodeRole],\n      SERVERPROPERTY('ProductMajorVersion') AS [SqlVersionMajor],\n      SERVERPROPERTY('ProductMinorVersion') AS [SqlVersionMinor],\n      SERVERPROPERTY('ProductBuild') AS [SqlVersionBuild],\n      SERVERPROPERTY('ProductBuildType') AS ProductBuildType,\n      SERVERPROPERTY('ProductLevel') AS ProductLevel,\n      SERVERPROPERTY('ProductUpdateLevel') AS ProductUpdateLevel,\n      SERVERPROPERTY('ProductUpdateReference') AS ProductUpdateReference,\n      RIGHT(CAST(SERVERPROPERTY('ProductVersion') AS NVARCHAR(30)),CHARINDEX('.', REVERSE(CAST(SERVERPROPERTY('ProductVersion') AS NVARCHAR(30)))) - 1) AS ProductRevision,\n      SERVERPROPERTY('EditionID') AS SQLEditionId,\n      SERVERPROPERTY('IsClustered') AS IsClustered,\n      SERVERPROPERTY('IsHadrEnabled') AS IsHadrEnabled,\n      SERVERPROPERTY('IsAdvancedAnalyticsInstalled') AS [SqlAdvAInstalled],\n      @@PACK_RECEIVED AS PacketReceived,\n      @@VERSION AS Version",
    "queryTimeInTicks": 0
  },
  {
    "instanceUniqueId": "8884F770C4D5A8C6729F76F33D472B28883AE518C92E1999888B171A085059FD",
    "isSSEIInstance": "0",
    "schemaVersion": "5",
    "emitTime": "2018-05-04T15:28:00.9025999Z",
    "sessionId": "c3cd1b56-ab61-462f-8363-8881779aa223",
    "correlationId": 0,
    "sequence": 23,
    "clientVersion": "14.0.3025.34 ((SQLServer2017-CU6).180410-0033)",
    "isInternalMachine": "1",
    "operatingSystem": "Microsoft Windows 10 Enterprise",
    "querySetVersion": "14.0.3025.34",
    "traceName": "SQLServerPeriodicQueries",
    "queryIdentifier": "OsSysInfo.003",
    "data": [
      {
        "LogicalCPUCount": "8",
        "HyperthreadRatio": "8",
        "PhysicalMemoryMB": "32710.902343",
        "SQLServerStartTime": "05/04/2018 08:22:30",
        "AffinityTypeDesc": "AUTO",
        "VirtualMachineType": "0",
        "SocketCount": "1",
        "CoresPerSocket": "4",
        "NumaNodeCount": "1",
        "ContainerType": "0",
        "ContainerDescription": "NONE"
      }
    ],
    "query": "SELECT\n      cpu_count AS LogicalCPUCount,\n      hyperthread_ratio AS HyperthreadRatio,\n      physical_memory_kb/1024.0 AS PhysicalMemoryMB,\n      sqlserver_start_time AS SQLServerStartTime,\n      affinity_type_desc AS AffinityTypeDesc,\n      virtual_machine_type AS VirtualMachineType,\n      socket_count as SocketCount,\n      cores_per_socket as CoresPerSocket,\n      numa_node_count as NumaNodeCount,\n      container_type as ContainerType,\n      container_type_desc as ContainerDescription\n      FROM sys.dm_os_sys_info WITH(nolock)",
    "queryTimeInTicks": 0
  }
]
```
## <a name="frequently-asked-questions"></a>Perguntas frequentes

**Como os DBAs leem os arquivos de log da Auditoria Local?**
Esses arquivos de log são gravados no formato JSON. Cada linha será um objeto JSON que representa um trecho de telemetria carregado para a Microsoft. Os nomes dos campos devem ser autoexplicativos.

**O que acontece se o DBA desabilitar a Coleta de comentários sobre uso?**
Nenhum arquivo da Auditoria Local será gravado.

**O que acontece se não houver conectividade com a internet/o computador estiver protegido pelo firewall?**
Comentários sobre o uso do SQL Server 2016 não serão enviado à Microsoft. Ele ainda tentará gravar os logs de auditoria local, se estiver configurado corretamente.

**Como os DBAs desabilitam a Auditoria Local?**
Remova a entrada da chave do registro UserRequestedLocalAuditDirectory.

**Quem pode ler os arquivos de log da Auditoria Local?**
Qualquer pessoa em sua organização que tiver acesso ao Diretório da Auditoria Local.

**Como os DBAs gerenciam os arquivos de log gravados no diretório designado?**
Os DBAs precisarão gerenciar automaticamente a limpeza de arquivos no diretório para evitar o consumo de muito espaço em disco.

**Há um cliente ou ferramenta que posso usar para ler esta saída JSON?**
A saída pode ser lida com o Bloco de notas, o Visual Studio ou qualquer leitor JSON de sua escolha.
Você também pode ler o arquivo JSON e analisar os dados em uma instância do SQL Server 2016, conforme ilustrado abaixo. Para obter mais detalhes sobre como ler o arquivo JSON no SQL Server, visite [Importing JSON files into SQL Server using OPENROWSET (BULK) and OPENJSON (Transact-SQL)](http://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/10/07/bulk-importing-json-files-into-sql-server/)(Importar arquivos JSON para o SQL Server usando OPENROWSET (BULK) e OPENJSON (Transact-SQL)).

```Transact-SQL
DECLARE @JSONFile AS VARCHAR(MAX)

-- Read the JSON file into variable 
SELECT @JSONFile = BulkColumn 
FROM OPENROWSET (BULK 'C:\SQLCEIPAudit\MSSQLSERVER\2016-09-08.json', SINGLE_CLOB) MyFile 

-- Check if the JSON file has been read properly and if it's in a JSON format
SELECT 
    @JSONFile LocalAuditOutput, 
    ISJSON(@JSONFile) IsFileInJSONFormat

-- Get the query identifier, query and the data (output of the query)   
SELECT 
    sequence,
    queryIdentifier,
    query,
    data
FROM OPENJSON(@JSONFile) 
    WITH (sessionId VARCHAR(64)
         ,sequence INT
         ,queryIdentifier VARCHAR(128)
         ,query VARCHAR(MAX)
         ,data NVARCHAR(MAX) AS JSON)
-- Get specific details about the output of "DatabaseProperties.001" query  
SELECT 
    QueryIdentifier,
    DatabaseID,
    CompatibilityLevel,
    IsQueryStoreOn
FROM OPENJSON(@JSONFile) 
    WITH (sessionId VARCHAR(64)
         ,sequence INT
         ,queryIdentifier VARCHAR(128)
         ,query VARCHAR(MAX)
         ,data NVARCHAR(MAX) AS JSON) 
    CROSS APPLY OPENJSON(data) 
        WITH (   DatabaseID varchar(128) '$.database_id'
                ,CompatibilityLevel varchar(128) '$.compatibility_level'
                ,IsQueryStoreOn varchar(128) '$.QS'
             )
WHERE queryIdentifier = 'DatabaseProperties.001'
```

## <a name="see-also"></a>Consulte Também
[Auditoria Local da coleta de comentários sobre o uso do SSMS](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-telemetry-ssms)
