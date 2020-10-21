---
title: Configurar a coleta de dados de uso e diagnóstico do SQL Server em Linux
description: Descreve como os dados de uso e diagnóstico do cliente do SQL Server são coletados e configurados em Linux.
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 96c58159a020ba11708b12a4e5732438044b3291
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115719"
---
# <a name="configure-usage--diagnostic-data-collection-for-sql-server-on-linux"></a>Configurar a coleta de dados de uso e diagnóstico do SQL Server em Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Por padrão, o Microsoft SQL Server coleta informações sobre como os clientes estão usando o aplicativo. Especificamente, o SQL Server coleta informações sobre a experiência de instalação, uso e desempenho. Essas informações ajudam a Microsoft a melhorar o produto para melhor atender às necessidades do cliente. Por exemplo, a Microsoft coleta informações sobre quais tipos de códigos de erro os clientes costumam encontrar, para que possamos corrigir erros relacionados, melhorar nossa documentação sobre como usar o SQL Server e determinar se os recursos devem ser adicionados ao produto para melhor atender aos clientes.

Este documento fornece detalhes sobre quais tipos de informações são coletados e sobre como configurar o Microsoft SQL Server em Linux para enviar essas informações coletadas à Microsoft. O SQL Server 2017 inclui uma política de privacidade que explica as informações que coletamos e que não coletamos dos usuários. Para obter mais informações, confira a [política de privacidade](../sql-server/sql-server-privacy.md).

Especificamente, a Microsoft não envia nenhum dos seguintes tipos de informações por meio desse mecanismo:

- Qualquer valor das tabelas de usuário
- Qualquer credencial de logon ou outras informações de autenticação
- PII (Informações de Identificação Pessoal)

O SQL Server 2017 sempre coleta e envia informações sobre a experiência de instalação do processo de configuração para que possamos localizar e corrigir rapidamente quaisquer problemas de instalação que o cliente esteja enfrentando. O SQL Server 2017 pode ser configurado para não enviar informações (em uma base de instância por servidor) para a Microsoft por meio de **mssql-conf**. mssql-conf é um script de configuração que é instalado com o SQL Server 2017 para Red Hat Enterprise Linux, SUSE Linux Enterprise Server e Ubuntu.

> [!NOTE]
> Você só pode desabilitar o envio de informações para a Microsoft em versões pagas do SQL Server.

## <a name="disable-usage-and-diagnostic-data-collection"></a>Desabilitar a coleta de dados de diagnóstico e de uso

Essa opção permite alterar se o SQL Server envia a coleta de dados de diagnóstico e uso para a Microsoft ou não. Por padrão, esse valor é definido como true. Para alterar o valor, execute os seguintes comandos:

> [!IMPORTANT]
> Você não pode desligar a coleta de dados de diagnóstico e uso para edições gratuitas do SQL Server, Express e Developer.

### <a name="on-red-hat-suse-and-ubuntu"></a>No Red Hat, SUSE e Ubuntu

1. Execute o script mssql-conf como raiz com o comando **set** para **telemetry.customerfeedback**. O exemplo a seguir desativa a coleta de dados de diagnóstico e uso especificando **false**.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. Reinicie o serviço SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>No Docker
Para desabilitar a coleta de dados de diagnóstico e uso no Docker, você fazer o Docker [manter seus dados](./sql-server-linux-docker-container-deployment.md). 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. Adicione um arquivo `mssql.conf` com as linhas `[telemetry]` e `customerfeedback = false` no diretório de host:
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```

2. Executar a imagem de contêiner

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. Adicione um arquivo `mssql.conf` com as linhas `[telemetry]` e `customerfeedback = false` no diretório de host:

   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```

2. Executar a imagem de contêiner

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

::: moniker-end

## <a name="local-audit-for-sql-server-on-linux-usage-and-diagnostic-data-collection"></a>Auditoria Local para coleta de dados de diagnóstico e uso do SQL Server em Linux

O Microsoft SQL Server 2017 contém recursos habilitados para Internet que podem coletar e enviar à Microsoft informações sobre seu computador ou dispositivo ('informações padrão do computador"). O componente de Auditoria Local da coleta de Dados de Diagnóstico e Uso do SQL Server pode gravar os dados coletados pelo serviço em uma pasta designada, representando os dados (logs) que serão enviados à Microsoft. A finalidade da Auditoria Local é permitir que os clientes vejam todos os dados que a Microsoft coleta com esse recurso, para fins de conformidade, regulatórios ou de validação de privacidade.

No SQL Server em Linux, a Auditoria Local é configurável no nível da instância para o Mecanismo de Banco de Dados do SQL Server. Outros componentes do SQL Server e Ferramentas do SQL Server não têm a funcionalidade de Auditoria Local para a coleta de dados de diagnóstico e uso.

### <a name="enable-local-audit"></a>Habilitar a Auditoria Local

Essa opção habilita a Auditoria Local e permite que você defina o diretório em que os logs de auditoria local são criados.

1. Crie um diretório de destino para novos logs de Auditoria Local. O exemplo a seguir cria um diretório **/tmp/audit**:

   ```bash
   sudo mkdir /tmp/audit
   ```

2. Altere o proprietário e o grupo do diretório para o usuário **mssql**:

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

3. Execute o script mssql-conf como raiz com o comando **set** para **telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

4. Reinicie o serviço SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>No Docker
Para habilitar a auditoria local no Docker, você deve fazer o Docker [manter seus dados](./sql-server-linux-docker-container-deployment.md). 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. O diretório de destino para novos logs de Auditoria Local estará no contêiner. Crie um diretório de destino para novos logs de Auditoria Local no diretório de host em seu computador. O exemplo a seguir cria um novo diretório **/audit**:

   ```bash
   sudo mkdir <host directory>/audit
   ```

1. Adicione um arquivo `mssql.conf` com as linhas `[telemetry]` e `userrequestedlocalauditdirectory = <host directory>/audit` no diretório de host:
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```

1. Executar a imagem de contêiner

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. O diretório de destino para novos logs de Auditoria Local estará no contêiner. Crie um diretório de destino para novos logs de Auditoria Local no diretório de host em seu computador. O exemplo a seguir cria um novo diretório **/audit**:

   ```bash
   sudo mkdir <host directory>/audit
   ```

1. Adicione um arquivo `mssql.conf` com as linhas `[telemetry]` e `userrequestedlocalauditdirectory = <host directory>/audit` no diretório de host:
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```

1. Executar a imagem de contêiner

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o SQL Server em Linux, confira [Visão geral do SQL Server em Linux](sql-server-linux-overview.md).