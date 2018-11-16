---
title: Comentários do cliente para o SQL Server no Linux | Microsoft Docs
description: Descreve como os comentários do cliente do SQL Server é coletado e configurado no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 06/22/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 003fc3496a68f0437dc2c7d313179da1f37a9c7b
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51669055"
---
# <a name="customer-feedback-for-sql-server-on-linux"></a>Comentários do cliente para o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Por padrão, o Microsoft SQL Server coleta informações sobre como os clientes estão usando o aplicativo. Especificamente, o SQL Server coleta informações sobre a experiência de instalação, uso e desempenho. Essas informações ajudam a Microsoft a melhorar o produto para melhor atender às necessidades do cliente. Por exemplo, a Microsoft coleta informações sobre quais tipos de códigos de erro os clientes costumam encontrar, para que possamos corrigir erros relacionados, melhorar nossa documentação sobre como usar o SQL Server e determinar se os recursos devem ser adicionados ao produto para melhor atender aos clientes.

Este documento fornece detalhes sobre quais tipos de informações são coletados e sobre como configurar o Microsoft SQL Server no Linux para enviar ou coletados informações à Microsoft. SQL Server 2017 inclui uma declaração de privacidade que explica quais informações fazemos e não coletar de usuários. Para obter mais informações, consulte o [declaração de privacidade](https://go.microsoft.com/fwlink/?LinkID=868444).

Especificamente, a Microsoft não envia nenhum dos seguintes tipos de informações por meio desse mecanismo:

- Qualquer valor das tabelas de usuário
- Qualquer credencial de logon ou outras informações de autenticação
- Informações de Identificação Pessoal (PII)

O SQL Server 2017 sempre coleta e envia informações sobre a experiência de instalação do processo de configuração para que possamos localizar e corrigir rapidamente quaisquer problemas de instalação que o cliente esteja enfrentando. SQL Server 2017 pode ser configurado para não enviar à Microsoft por meio de informações (em uma base de instância por servidor) **mssql-conf**. MSSQL-conf é um script de configuração que é instalado com o SQL Server 2017 para Red Hat Enterprise Linux, SUSE Linux Enterprise Server e Ubuntu.

> [!NOTE]
> Você só pode desabilitar o envio de informações para a Microsoft em versões pagas do SQL Server.

## <a name="disable-customer-feedback"></a>Desabilitar comentários dos clientes

Essa opção permite alterar se o SQL Server envia comentários à Microsoft ou não. Por padrão, esse valor é definido como true. Para alterar o valor, execute os seguintes comandos:

> [!IMPORTANT]
> Você pode desligar os comentários dos clientes gratuitamente edições do SQL Server, Express e Developer.

### <a name="on-red-hat-suse-and-ubuntu"></a>No Red Hat, SUSE e Ubuntu

1. Execute o script mssql-conf como raiz com o **definir** comando **telemetry.customerfeedback**. O exemplo a seguir desativa os comentários dos clientes, especificando **falsos**.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. Reinicie o serviço do SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>No Docker
Para desabilitar os comentários dos clientes no docker, você deve ter o Docker [persistir seus dados](sql-server-linux-configure-docker.md). 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. Adicionar um `mssql.conf` arquivo com as linhas `[telemetry]` e `customerfeedback = false` no diretório do host:
 
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

1. Adicionar um `mssql.conf` arquivo com as linhas `[telemetry]` e `customerfeedback = false` no diretório do host:

   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```

2. Executar a imagem de contêiner

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
   ```

::: moniker-end

## <a name="local-audit-for-sql-server-on-linux-usage-feedback-collection"></a>Auditoria local para o SQL Server na coleta de comentários de uso do Linux

Microsoft SQL Server 2017 contém recursos habilitados para Internet que podem coletar e enviar à Microsoft informações sobre seu computador ou dispositivo ("informações padrão do computador"). O componente de auditoria Local da coleta de comentários de uso do SQL Server pode gravar os dados coletados pelo serviço em uma pasta designada, que representa os dados (logs) que serão enviados à Microsoft. A finalidade da Auditoria Local é permitir que os clientes vejam todos os dados que a Microsoft coleta com esse recurso, para fins de conformidade, regulatórios ou de validação de privacidade.

No SQL Server no Linux, auditoria Local é configurável no nível de instância para o mecanismo de banco de dados do SQL Server. Outros componentes do SQL Server e ferramentas do SQL Server não tem a capacidade de auditoria Local para coleta de comentários de uso.

### <a name="enable-local-audit"></a>Habilitar a auditoria Local

Essa opção habilita a auditoria Local e permite que você defina o diretório onde os logs de auditoria Local são criados.

1. Crie um diretório de destino para novos logs de auditoria Local. O exemplo a seguir cria um novo **auditoria/tmp/** diretório:

   ```bash
   sudo mkdir /tmp/audit
   ```

2. Alterar o proprietário e o grupo do diretório para o **mssql** usuário:

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

3. Execute o script mssql-conf como raiz com o **definir** comando **telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

4. Reinicie o serviço do SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>No Docker
Para habilitar a auditoria Local no docker, você deve ter o Docker [persistir seus dados](sql-server-linux-configure-docker.md). 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. O diretório de destino para novos logs de auditoria Local será no contêiner. Crie um diretório de destino para novos logs de auditoria Local no diretório em sua máquina host. O exemplo a seguir cria um novo **/auditoria** diretório:

   ```bash
   sudo mkdir <host directory>/audit
   ```

1. Adicionar um `mssql.conf` arquivo com as linhas `[telemetry]` e `userrequestedlocalauditdirectory = <host directory>/audit` no diretório do host:
 
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

1. O diretório de destino para novos logs de auditoria Local será no contêiner. Crie um diretório de destino para novos logs de auditoria Local no diretório em sua máquina host. O exemplo a seguir cria um novo **/auditoria** diretório:

   ```bash
   sudo mkdir <host directory>/audit
   ```

1. Adicionar um `mssql.conf` arquivo com as linhas `[telemetry]` e `userrequestedlocalauditdirectory = <host directory>/audit` no diretório do host:
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```

1. Executar a imagem de contêiner

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
   ```

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o SQL Server no Linux, consulte o [visão geral do SQL Server no Linux](sql-server-linux-overview.md).
