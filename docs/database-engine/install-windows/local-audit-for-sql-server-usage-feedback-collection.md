---
title: Auditoria local da coleta de comentários sobre o uso do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-security
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Local Audit
ms.assetid: a0665916-7789-4f94-9086-879275802cf3
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f69dfadfb4de412794beba72f69b22fdc8a39287
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="local-audit-for-sql-server-usage-feedback-collection"></a>Auditoria Local da coleta de comentários sobre o uso do SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

## <a name="introduction"></a>Introdução

O Microsoft SQL Server contém recursos habilitados para Internet que podem coletar e enviar à Microsoft informações sobre seu computador ou dispositivo (“informações padrão do computador”). O componente de Auditoria Local da [Coleta de comentários sobre o uso do SQL Server](http://support.microsoft.com/kb/3153756) grava dados coletados pelo serviço em uma pasta designada, que representa os dados (logs) que serão enviados à Microsoft. A finalidade da Auditoria Local é permitir que os clientes vejam todos os dados que a Microsoft coleta com esse recurso, para fins de conformidade, regulatórios ou de validação de privacidade.  

A partir do SQL Server 2016 CU2, a Auditoria Local é configurável no nível da instância no Mecanismo de Banco de Dados do SQL Server e o SSAS (Analysis Services). No SQL Server 2016 CU4 e no SQL Server 2016 SP1, a Auditoria Local também está habilitada para o SQL Server Integration Services (SSIS). Outros componentes do SQL Server que são instalados durante a instalação e as ferramentas do SQL Server que são baixadas ou instaladas após a instalação não têm o recurso de Auditoria Local para coleta de comentários sobre uso. 

## <a name="prerequisites"></a>Prerequisites 

A seguir estão os pré-requisitos para habilitar a Auditoria Local em cada instância do SQL Server: 

1. A instância está corrigida para o SQL Server 2016 RTM CU2 ou posterior. 

1. O usuário deve ser um administrador do sistema ou ter uma função com acesso para adicionar e modificar a Chave do Registro, criar pastas, gerenciar a segurança das pastas e parar/iniciar um Serviço do Windows.  

## <a name="pre-configuration-steps-prior-to-turning-on-local-audit"></a>Etapas de pré-configuração antes de ativar a Auditoria Local 

Antes de ativar a Auditoria Local, um administrador do sistema deve:

1. Conhecer o nome da instância do SQL Server e a conta de logon do serviço de telemetria do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server. 

1. Configurar uma nova pasta para os arquivos de Auditoria Local.

1. Conceder permissões para a conta de logon do serviço de telemetria do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server.

1. Criar uma configuração de chave do registro para configurar o diretório de destino da Auditoria Local. 

    Para o Mecanismo de Banco de Dados e o Integration Services, crie a chave em *HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSSQL14.\<INSTANCENAME\>\\CPE*. 
    
    Para o Analysis Services, crie a chave em *HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSAS14.\<INSTANCENAME\>\\CPE*.

### <a name="get-the-sql-server-ceip-service-logon-account"></a>Obter a conta de logon de serviço do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server

Execute as seguintes etapas para obter a conta de logon do serviço de telemetria do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server
 
1. Inicie **Serviços** – clique no botão **Windows**  e digite *Services.msc*. 

2. Navegue até o serviço apropriado. Por exemplo, para o mecanismo de banco de dados, localize o **Serviço do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server \<nome da instância\>**. Para o Analysis Services, localize **Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server Analysis Services \<nome da instância\>**. Para o Integration Services, localize o **serviço 13 do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server Integration Services**.

3. Clique com o botão direito do mouse no serviço e escolha **Propriedades**. 

4. Clique na guia **Logon** . A conta de Logon está listada em **Esta Conta**. 

### <a name="configure-a-new-folder-for-the-local-audit-files"></a>Configurar uma nova pasta para os arquivos de Auditoria Local.    

Crie uma nova pasta (Diretório da Auditoria Local) em que a Auditoria Local gravará os logs. Por exemplo, o caminho completo para o Diretório da Auditoria Local para uma instância padrão do mecanismo de banco de dados seria: *C:\\SQLCEIPAudit\\MSSQLSERVER\\DB\\*. 
 
> Observação: configure o caminho do diretório da Auditoria Local fora do caminho de instalação do SQL Server para evitar que a funcionalidade de auditoria e a aplicação de patches causem problemas com o SQL Server.

  ||Decisão de design|Recomendação|  
  |------|-----------------|----------|  
  |![Caixa de seleção](../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Disponibilidade de espaço |Com uma carga de trabalho moderada com cerca de 10 bancos de dados, planeje para ter cerca de 2 MB de espaço em disco por dia por instância.|  
|![Caixa de seleção](../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Diretórios separados | Crie um diretório para cada instância. Por exemplo, use *C:\\SQLCEIPAudit\\MSSQLSERVER\\DB\\* para uma instância do SQL Server chamada `MSSQLSERVER`. Isso simplifica o gerenciamento de arquivos.
|![Caixa de seleção](../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Pastas separadas |Use uma pasta específica para cada serviço. Por exemplo, para um determinado nome de instância, tenha uma pasta para o mecanismo de banco de dados. Se uma instância do SSAS usar o mesmo nome de instância, crie uma pasta separada para o SSAS. Ter instâncias do Mecanismo de Banco de Dados e do Analysis Services configuradas para a mesma pasta fará com que a Auditoria Local grave no mesmo arquivo de log para as duas instâncias.| 
|![Caixa de seleção](../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Conceder permissões para a conta de logon do serviço de telemetria do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server|Habilite acesso para **Listar Conteúdo da Pasta**, **Ler** e **Gravar** à conta de logon do serviço de telemetria do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server|


### <a name="grant-permissions-to-the-sql-server-ciep-telemetry-service-logon-account"></a>Conceder permissões para a conta de logon do serviço de telemetria do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server
  
1. No **Explorador de Arquivos**, navegue até o local em que a nova pasta está localizada.  

1. Clique com o botão direito do mouse na nova pasta e escolha **Propriedades**. 

1. Na guia **Segurança**, clique em **Editar** e gerenciar Permissão.

1. Clique em **Adicionar** e digite as credenciais do Serviço de Telemetria do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server, por exemplo `NT Service\SQLTELEMETRY`.   

1. Clique em **Verificar Nomes** para validar o nome fornecido e clique em **OK**. 

1. Na caixa de diálogo **Permissão** , escolha a conta de logon ao Serviço de Telemetria do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server e clique em **Listar Conteúdo da Pasta**, **Ler** e **Gravar**.  

1. Clique em **OK** para aplicar as alterações de permissão imediatamente. 
  
### <a name="create-a-registry-key-setting-to-configure-local-audit-target-directory"></a>Criar uma configuração de chave do registro para configurar o diretório de destino da Auditoria Local.

1. Inicie o regedit.  

1. Navegue até o caminho do CPE apropriado. 

    Para o Mecanismo de Banco de Dados e o Integration Services, use *HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSSQL14.\<INSTANCENAME\>\\CPE*. 
    
    Para o Analysis Services, use *HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSAS14.\<INSTANCENAME\>\\CPE*.

1. Clique com o botão direito do mouse no caminho do CPE e escolha **Novo**. Clique em **Valor da Cadeia**.

1. Nomeie a nova chave do Registro `UserRequestedLocalAuditDirectory`. 
 
## <a name="turning-local-audit-on-or-off"></a>Ativando ou desativando a Auditoria Local

Depois de concluir as etapas de pré-configuração, você pode ativar a Auditoria Local. Para fazer isso, use uma conta de administrador do sistema ou com uma função semelhante com acesso para modificar chaves de registro para ativar ou desativar a Auditoria Local seguindo as etapas abaixo. 

1. Inicie o **regedit**.  

1. Navegue até o caminho do CPE apropriado. 

    Para o Mecanismo de Banco de Dados e o Integration Services, use *HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSSQL14.\<INSTANCENAME\>\\CPE*. 
    
    Para o Analysis Services, use *HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSAS14.\<INSTANCENAME\>\\CPE*.

1. Clique com o botão direito do mouse em **UserRequestedLocalAuditDirectory** e clique em *Modificar*. 

1. Para ativar a Auditoria Local, digite o caminho da Auditoria Local, por exemplo *C:\\SQLCEIPAudit\\MSSQLSERVER\\DB\\*.
 
    Para desativar a Auditoria Local, esvazie o valor em **UserRequestedLocalAuditDirectory**.

1. Feche o **regedit**. 

O Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server deve reconhecer a configuração da Auditoria Local imediatamente se o serviço já estiver em execução. Para iniciar o serviço do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server, o administrador do sistema ou alguém que tenha acesso para iniciar ou parar Serviços do Windows pode seguir as etapas abaixo: 

1. Inicie o aplicativo de Serviços clicando no botão do Windows e digite Services. 

1. Navegue até o serviço apropriado. 

    Para o Mecanismo de Banco de Dados, use **Serviço do Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server (\<NOMEDAINSTÂNCIA\>)**. 
    
    Para o Analysis Services, use **Programa de Aperfeiçoamento da Experiência do Usuário do SQL Server Analysis Services (\<NOMEDAINSTÂNCIA\>)**. 

1. Clique com o botão direito do mouse no serviço e escolha Reiniciar. 

1. Verifique se o status do serviço é **Executando**. 

A Auditoria Local produzirá um arquivo de log por dia. Os arquivos de log estarão na forma de `<YYYY-MM-DD>.json`. Por exemplo, *2016-07-12.json*. Se houver um arquivo existente para o dia no diretório designado, a Auditoria Local acrescentará a ele. Caso contrário, criará um novo arquivo para o dia. 

> Observação: após habilitar a Auditoria Local, pode levar até 5 minutos para que o arquivo de log seja gravado pela primeira vez. 

## <a name="maintenance"></a>Manutenção 

1. Para limitar o uso do espaço em disco pelos arquivos gravados pela Auditoria Local, configure uma política ou um trabalho regular para limpar o Diretório da Auditoria Local para remover arquivos antigos e desnecessários.  

2. Proteja o caminho do Diretório da Auditoria Local para que ele seja acessível apenas para as pessoas apropriadas. Observe que os arquivos de log contêm as informações descritas em [Como configurar o SQL Server 2016 para enviar comentários à Microsoft](http://support.microsoft.com/kb/3153756). O acesso a este arquivo deve impedir que a maioria dos membros de sua organização o leiam.  

## <a name="data-dictionary-of-local-audit-output-data-structure"></a>Dicionário de dados da estrutura de dados de saída da Auditoria Local 

- Os arquivos de log da Auditoria Local estão em JSON, contendo um conjunto de objetos (linhas) que representam pontos de dados que são enviados de volta para a Microsoft em **emitTime**.  

- Cada linha segue um esquema específico identificado por **schemaVersion**.   

- Cada linha é uma saída de uma sessão de serviços SQLCEIP identificada como **sessionID**.  

- As linhas são emitidas em sequência, identificadas por **sequence**. 

- Cada linha de ponto de dados contém a saída de um **queryIdentifier** que pode ser uma consulta T-SQL, uma sessão XE ou uma mensagem relacionada a um tipo de rastreamento, identificado como **traceName**.   

- **queryIdentifiers** são agrupados e sua versão é controlada em conjunto com **querySetVersion**. 

- **data** contêm a saída da execução da consulta correspondente que levou **queryTimeInTicks**. 

- **queryIdentifiers** para consultas T-SQL têm a definição da consulta T-SQL armazenada na consulta. 


| Hierarquia lógica de informações da Auditoria Local | Colunas relacionadas |
| ------ | -------|
| Cabeçalho | emitTime, schemaVersion 
| Computador | hostname, domainHash, sqmID, operatingSystem 
| Instância | instanceName, correlationID, clientVersion 
| Session | sessionID, traceName 
| Consulta | sequence, querySetVersion, queryIdentifier, query, queryTimeInTicks 
| data |  data 

### <a name="namevalue-pairs-definition-and-examples"></a>Definição e exemplos de pares nome/valor 

As colunas listadas abaixo representam a ordem da saída de arquivos da Auditoria Local. Hash unidirecional com SHA 256 é usado para valores mantidos em anonimato para um número de colunas abaixo.  

| Nome | Description | Valores de exemplo
|-------|--------| ----------|
|hostname | Nome do computador mantido em anonimato em que o SQL Server está instalado| de3b3769a63970b63981ab7a956401388962c986bfd39d371f5870d800627d11 
|domainHash| Hash de domínio mantido em anonimado do computador que hospeda a instância do SQL Server | de3b3769a63970b63981ab7a956401388962c986bfd39d371f5870d800627d11 
|sqmId |Identificador que representa o computador em que o SQL Server está instalado | 02AF58F5-753A-429C-96CD-3900E90DB990 
|NOMEDAINSTÂNCIA| Nome da instância do SQL Server mantido em anonimato| e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855 
|schemaVersion| Versão do esquema do SQLCEIP |  3 
|emitTime |Hora de emissão do ponto de dados em UTC | 2016-09-08T17:20:22.1124269Z 
|sessionID | Identificador da sessão para o serviço do SQLCEIP | 89decf9a-ad11-485c-94a7-fefb3a02ed86 
| correlationId | Espaço reservado para um identificador adicional | 0 
|sequence | Número de sequência de pontos de dados enviados dentro da sessão | 15 
| clientVersion | Versão da instância do SQL Server | 13.0.2161.3 ((SQL16_RTM_QFE-CU).160907-1223) 
| operatingSystem | A versão do sistema operacional em que a instância do SQL Server está instalada | Microsoft Windows Server 2012 R2 Datacenter 
| querySetVersion | Versão de um grupo de definições de consulta | 1.0.0.0 
|traceName | Categorias de rastreamentos: (SQLServerXeQueries, SQLServerPeriodicQueries, SQLServerOneSettingsException) | SQLServerPeriodicQueries 
|queryIdentifier | Um identificador da consulta | SQLServerProperties.002 
|data   | A saída das informações coletadas em queryIdentifier como uma saída de uma consulta T-SQL, sessão XE ou do aplicativo |   [{"Collation": "SQL_Latin1_General_CP1_CI_AS","SqlFTinstalled": "0" "SqlIntSec": "1","IsSingleUser": "0","SqlFilestreamMode": "0","SqlPbInstalled": "0","SqlPbNodeRole": "","SqlVersionMajor": "13","SqlVersionMinor": "0","SqlVersionBuild": "2161","ProductBuildType": "","ProductLevel": "RTM","ProductUpdateLevel": "CU2","ProductUpdateReference": "KB3182270","ProductRevision": "3","SQLEditionId": "-1534726760","IsClustered": "0","IsHadrEnabled": "0","SqlAdvAInstalled": "0","PacketReceived": "1210","Version": "Microsoft SQL Server 2016 (RTM-CU2) (KB3182270) - 13.0.2161.3 (X64) \n\tSep  7 2016 14:24:16 \n\tCopyright (c) Microsoft Corporation\n\tStandard Edition (64-bit) on Windows Server 2012 R2 Datacenter 6.3 \u003cX64\u003e (Build 9600: ) (Hypervisor)\n"}],
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
{
    "hostName": "de3b3769a63970b63981ab7a956401388962c986bfd39d371f5870d800627d11",
    "domainHash": "de3b3769a63970b63981ab7a956401388962c986bfd39d371f5870d800627d11",
    "sqmId": "02AF58F5-753A-429C-96CD-3900E90DB990",
    "instanceName": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
    "schemaVersion": "3",
    "emitTime": "2016-09-08T17:20:22.1124269Z",
    "sessionId": "89decf9a-ad11-485c-94a7-fefb3a02ed86",
    "correlationId": 0,
    "sequence": 15,
    "clientVersion": "13.0.2161.3 ((SQL16_RTM_QFE-CU).160907-1223)",
    "operatingSystem": "Microsoft Windows Server 2012 R2 Datacenter",
    "querySetVersion": "1.0.0.0",
    "traceName": "SQLServerPeriodicQueries",
    "queryIdentifier": "SQLServerProperties.002",
    "data": [
      {
        "Collation": "SQL_Latin1_General_CP1_CI_AS",
        "SqlFTinstalled": "0",
        "SqlIntSec": "1",
        "IsSingleUser": "0",
        "SqlFilestreamMode": "0",
        "SqlPbInstalled": "0",
        "SqlPbNodeRole": "",
        "SqlVersionMajor": "13",
        "SqlVersionMinor": "0",
        "SqlVersionBuild": "2161",
        "ProductBuildType": "",
        "ProductLevel": "RTM",
        "ProductUpdateLevel": "CU2",
        "ProductUpdateReference": "KB3182270",
        "ProductRevision": "3",
        "SQLEditionId": "-1534726760",
        "IsClustered": "0",
        "IsHadrEnabled": "0",
        "SqlAdvAInstalled": "0",
        "PacketReceived": "1210",
        "Version": "Microsoft SQL Server 2016 (RTM-CU2) (KB3182270) - 13.0.2161.3 (X64) \n\tSep  7 2016 14:24:16 \n\tCopyright (c) Microsoft Corporation\n\tStandard Edition (64-bit) on Windows Server 2012 R2 Datacenter 6.3 \u003cX64\u003e (Build 9600: ) (Hypervisor)\n"
      }
    ],
    "query": "SELECT\n      SERVERPROPERTY(\u0027Collation\u0027) AS [Collation],\n      SERVERPROPERTY(\u0027IsFullTextInstalled\u0027) AS [SqlFTinstalled],\n      SERVERPROPERTY(\u0027IsIntegratedSecurityOnly\u0027) AS [SqlIntSec],\n      SERVERPROPERTY(\u0027IsSingleUser\u0027) AS [IsSingleUser],\n      SERVERPROPERTY (\u0027FileStreamEffectiveLevel\u0027) AS [SqlFilestreamMode],\n      SERVERPROPERTY(\u0027IsPolybaseInstalled\u0027) AS [SqlPbInstalled],\n      SERVERPROPERTY(\u0027PolybaseRole\u0027) AS [SqlPbNodeRole],\n      SERVERPROPERTY(\u0027ProductMajorVersion\u0027) AS [SqlVersionMajor],\n      SERVERPROPERTY(\u0027ProductMinorVersion\u0027) AS [SqlVersionMinor],\n      SERVERPROPERTY(\u0027ProductBuild\u0027) AS [SqlVersionBuild],\n      SERVERPROPERTY(\u0027ProductBuildType\u0027) AS ProductBuildType,\n      SERVERPROPERTY(\u0027ProductLevel\u0027) AS ProductLevel,\n      SERVERPROPERTY(\u0027ProductUpdateLevel\u0027) AS ProductUpdateLevel,\n      SERVERPROPERTY(\u0027ProductUpdateReference\u0027) AS ProductUpdateReference,\n      RIGHT(CAST(SERVERPROPERTY(\u0027ProductVersion\u0027) AS NVARCHAR(30)),CHARINDEX(\u0027.\u0027, REVERSE(CAST(SERVERPROPERTY(\u0027ProductVersion\u0027) AS NVARCHAR(30)))) - 1) AS ProductRevision,\n      SERVERPROPERTY(\u0027EditionID\u0027) AS SQLEditionId,\n      SERVERPROPERTY(\u0027IsClustered\u0027) AS IsClustered,\n      SERVERPROPERTY(\u0027IsHadrEnabled\u0027) AS IsHadrEnabled,\n      SERVERPROPERTY(\u0027IsAdvancedAnalyticsInstalled\u0027) AS [SqlAdvAInstalled],\n      @@PACK_RECEIVED AS PacketReceived,\n      @@VERSION AS Version",
    "queryTimeInTicks": 0
  } ,
  {
    "hostName": "de3b3769a63970b63981ab7a956401388962c986bfd39d371f5870d800627d11",
    "domainHash": "de3b3769a63970b63981ab7a956401388962c986bfd39d371f5870d800627d11",
    "sqmId": "02AF58F5-753A-429C-96CD-3900E90DB990",
    "instanceName": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
    "schemaVersion": "3",
    "emitTime": "2016-09-08T17:20:24.9819144Z",
    "sessionId": "89decf9a-ad11-485c-94a7-fefb3a02ed86",
    "correlationId": 0,
    "sequence": 61,
    "clientVersion": "13.0.2161.3 ((SQL16_RTM_QFE-CU).160907-1223)",
    "operatingSystem": "Microsoft Windows Server 2012 R2 Datacenter",
    "querySetVersion": "1.0.0.0",
    "traceName": "SQLServerPeriodicQueries",
    "queryIdentifier": "ExternalScriptStats.001",
    "data": [
      {
        "counter_name": "Total Executions                                                                                                                ",
        "cntr_value": "0"
      },
      {
        "counter_name": "Parallel Executions                                                                                                             ",
        "cntr_value": "0"
      },
      {
        "counter_name": "Streaming Executions                                                                                                            ",
        "cntr_value": "0"
      },
      {
        "counter_name": "SQL CC Executions                                                                                                               ",
        "cntr_value": "0"
      },
      {
        "counter_name": "Implied Auth. Logins                                                                                                            ",
        "cntr_value": "0"
      },
      {
        "counter_name": "Total Execution Time (ms)                                                                                                       ",
        "cntr_value": "0"
      },
      {
        "counter_name": "Execution Errors                                                                                                                ",
        "cntr_value": "0"
      }
    ],  
    "query": "select counter_name, cntr_value from sys.dm_os_performance_counters where object_name like \u0027%External Scripts%\u0027",
    "queryTimeInTicks": 155834
  } 
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

