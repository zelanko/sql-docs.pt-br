---
title: Habilitar ou desabilitar o gerenciamento remoto do pacote do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/20/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 5b0039736102af09fe12e296c85cd57a83509a6b
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2018
---
# <a name="enable-or-disable-remote-package-management-for-sql-server"></a>Habilitar ou desabilitar o gerenciamento remoto do pacote do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve como habilitar o gerenciamento de pacotes de R de uma instância remota do servidor de aprendizado de máquina. Após a habilitação do recurso de gerenciamento de pacote, você pode usar comandos de RevoScaleR para instalar os pacotes em um banco de dados de um cliente remoto.

> [!NOTE]
> Atualmente há suporte para gerenciamento de bibliotecas de R; suporte para Python em nossos planos.

Por padrão, o recurso de gerenciamento do pacote externo para o SQL Server está desabilitado, mesmo se os recursos de aprendizado de máquina foram instalados. Você deve executar um script separado para habilitar o recurso conforme descrito na próxima seção.

## <a name="overview-of-process-and-tools"></a>Visão geral do processo e ferramentas

Para habilitar ou desabilitar o gerenciamento de pacote, use o utilitário de linha de comando **RegisterRExt.exe**, que é incluído com o **RevoScaleR** pacote.

[Habilitando](#bkmk_enable) esse recurso é um processo de duas etapas, exigindo que um administrador de banco de dados: habilitar o gerenciamento de pacote na instância do SQL Server (uma vez por instância do SQL Server) e, em seguida, habilitar o gerenciamento de pacote no banco de dados SQL (uma vez por SQL Server banco de dados).

[Desabilitando](#bkmk_disable) o recurso de pacote de gerenciamento também requer etapas multipel: remover pacotes de nível de banco de dados e permissões (uma vez por banco de dados) e, em seguida, remova as funções do servidor (uma vez por instância).

## <a name="bkmk_enable"></a> Habilitar o gerenciamento de pacote

1. Abra um prompt de comando com privilégios elevados e navegue até a pasta que contém o utilitário, RegisterRExt.exe. O local padrão é `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`.

2. Execute o comando a seguir, fornecendo argumentos apropriados para seu ambiente:

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando cria objetos de nível de instância no computador do SQL Server que são necessários para o gerenciamento de pacotes. Ele também reinicia a barra inicial para a instância.

    Se você não especificar uma instância, a instância padrão será usada. Se você não especificar um usuário, o contexto de segurança atual será usado. Por exemplo, o comando a seguir habilita o gerenciamento de pacotes na instância no caminho do RegisterRExt.exe, usando as credenciais do usuário que abriu o prompt de comando:

    `REgisterRExt.exe /installpkgmgmt`

3. Para adicionar o gerenciamento de pacotes para um banco de dados específico, execute o seguinte comando em um prompt de comando elevado:

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    Este comando cria alguns artefatos do banco de dados, incluindo as seguintes funções de banco de dados que são usadas para controlar permissões de usuário: `rpkgs-users`, `rpkgs-private`, e `rpkgs-shared`.

    Por exemplo, o comando a seguir permite o gerenciamento de pacote no banco de dados na instância onde RegisterRExt é executado. Se você não especificar um usuário, o contexto de segurança atual será usado.

    `RegisterRExt.exe /installpkgmgmt /database:TestDB`

4. Repita o comando para cada banco de dados em que os pacotes devem ser instalados.

5. Para verificar se as novas funções foram criadas com êxito, no SQL Server Management Studio, clique em banco de dados, expanda **segurança**e expanda **funções de banco de dados**.

    Você também pode executar uma consulta em sys. database_principals como o seguinte:

    ```SQL
    SELECT pr.principal_id, pr.name, pr.type_desc,   
        pr.authentication_type_desc, pe.state_desc,   
        pe.permission_name, s.name + '.' + o.name AS ObjectName  
    FROM sys.database_principals AS pr  
    JOIN sys.database_permissions AS pe  
        ON pe.grantee_principal_id = pr.principal_id  
    JOIN sys.objects AS o  
        ON pe.major_id = o.object_id  
    JOIN sys.schemas AS s  
        ON o.schema_id = s.schema_id;
    ```

Depois de habilitar esse recurso, você pode usar a função de RevoScaleR para instalar ou desinstalar os pacotes de um cliente remoto do R.

## <a name="bkmk_disable"></a> Desabilitar o gerenciamento de pacote

1. Em um prompt de comando com privilégios elevados, execute o utilitário RegisterRExt novamente e desabilitar o pacote de gerenciamento no nível do banco de dados:

    `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    Este comando remove objetos de banco de dados relacionados ao gerenciamento de pacotes do banco de dados especificado. Ele também remove todos os pacotes que foram instalados a partir do local de sistema de arquivos protegidos no computador do SQL Server.

2. Repita esse comando em cada banco de dados onde o gerenciamento de pacotes foi usado.

3.  (Opcional) Depois que todos os bancos de dados foi limpo de pacotes usando a etapa anterior, execute o seguinte comando em um prompt de comando elevado:

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando remove o recurso de gerenciamento de pacote da instância. Talvez seja necessário reiniciar manualmente o serviço Launchpad mais uma vez para ver as alterações.

