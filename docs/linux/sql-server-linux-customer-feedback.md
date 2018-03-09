---
title: "Comentários do cliente para o SQL Server no Linux | Microsoft Docs"
description: "Descreve como os comentários do cliente do SQL Server são coletados e configurado no Linux."
author: annashres
ms.author: anshrest
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: 25772bd0ad7b2994e732e97fd264bef0e951eea9
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2018
---
# <a name="customer-feedback-for-sql-server-on-linux"></a>Comentários do cliente para o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Por padrão, o Microsoft SQL Server coleta informações sobre como os clientes estão usando o aplicativo. Especificamente, o SQL Server coleta informações sobre a experiência de instalação, uso e desempenho. Essas informações ajudam a Microsoft a melhorar o produto para melhor atender às necessidades do cliente. Por exemplo, a Microsoft coleta informações sobre quais tipos de códigos de erro os clientes costumam encontrar, para que possamos corrigir erros relacionados, melhorar nossa documentação sobre como usar o SQL Server e determinar se os recursos devem ser adicionados ao produto para melhor atender aos clientes.

Este documento fornece detalhes sobre quais tipos de informações são coletados e como configurar o Microsoft SQL Server no Linux para enviar ou coletados informações à Microsoft. SQL Server 2017 inclui uma declaração de privacidade que explica quais informações fazemos e não coletar de usuários. Leia a declaração de privacidade.

Especificamente, a Microsoft não envia nenhum dos seguintes tipos de informações por meio desse mecanismo:

- Qualquer valor das tabelas de usuário
- Qualquer credencial de logon ou outras informações de autenticação
- Informações de Identificação Pessoal (PII)

O SQL Server 2017 sempre coleta e envia informações sobre a experiência de instalação do processo de configuração para que possamos localizar e corrigir rapidamente quaisquer problemas de instalação que o cliente esteja enfrentando. 2017 do SQL Server pode ser configurado para não enviar à Microsoft por meio de informações (em uma base de instância por servidor) **mssql conf**. MSSQL conf é um script de configuração que é instalado com o SQL Server 2017 para Red Hat Enterprise Linux, SUSE Linux Enterprise Server e Ubuntu.

> [!NOTE]
> Você só pode desabilitar o envio de informações para a Microsoft em versões pagas do SQL Server.

## <a name="disable-customer-feedback"></a>Desabilitar comentários do cliente

Esta opção lhe permite alterar se o SQL Server envia comentários à Microsoft ou não. Por padrão, esse valor é definido como true. Para alterar o valor, execute os seguintes comandos:

### <a name="on-red-hat-suse-and-ubuntu"></a>No Red Hat, SUSE e Ubuntu

1. Execute o script mssql conf como raiz com o **definir** comando **telemetry.customerfeedback**. O exemplo a seguir desativa os comentários dos clientes, especificando **false**.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. Reinicie o serviço do SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>No Docker
Para desabilitar os comentários dos clientes no docker, você deve ter Docker [persistir os dados](sql-server-linux-configure-docker.md). 

1. Adicionar uma `mssql.conf` arquivo com as linhas `[telemetry]` e `customerfeedback = false` no diretório do host:
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```
2. Executar a imagem de contêiner
   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```
   
## <a name="local-audit-for-sql-server-on-linux-usage-feedback-collection"></a>Auditoria de local para o SQL Server na coleção de comentários do uso do Linux

2017 do Microsoft SQL Server contém recursos habilitados para Internet que podem coletar e enviar à Microsoft informações sobre seu computador ou dispositivo ("informações padrão do computador"). O componente de auditoria Local da coleção de comentários sobre o uso de SQL Server pode gravar dados coletados pelo serviço para uma pasta designada, que representa os dados (logs) que serão enviados à Microsoft. A finalidade da Auditoria Local é permitir que os clientes vejam todos os dados que a Microsoft coleta com esse recurso, para fins de conformidade, regulatórios ou de validação de privacidade.

No SQL Server no Linux, o Local de auditoria é configurável no nível de instância para o mecanismo de banco de dados do SQL Server. Outros componentes do SQL Server e as ferramentas do SQL Server não tem capacidade de auditoria Local para a coleção de comentários de uso.

### <a name="enable-local-audit"></a>Habilitar auditoria Local

Essa opção habilita a auditoria Local e permite que você defina o diretório onde os logs de auditoria Local são criados.

1. Crie um diretório de destino para novos logs de auditoria Local. O exemplo a seguir cria um novo **/tmp/auditoria** diretório:

   ```bash
   sudo mkdir /tmp/audit
   ```

1. Alterar o proprietário e o grupo do diretório para o **mssql** usuário:

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

1. Execute o script mssql conf como raiz com o **definir** comando **telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

1. Reinicie o serviço do SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>No Docker
Para habilitar a auditoria Local no docker, você deve ter Docker [persistir os dados](sql-server-linux-configure-docker.md). 

1. O diretório de destino para novos logs de auditoria Local será no contêiner. Crie um diretório de destino para novos logs de auditoria Local no diretório de host no seu computador. O exemplo a seguir cria um novo **/auditoria** diretório:

   ```bash
   sudo mkdir <host directory>/audit
   ```

   
1. Adicionar uma `mssql.conf` arquivo com as linhas `[telemetry]` e `userrequestedlocalauditdirectory = <host directory>/audit` no diretório do host:
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```
2. Executar a imagem de contêiner
   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```
   
## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o SQL Server no Linux, consulte o [visão geral do SQL Server no Linux](sql-server-linux-overview.md).
