---
title: Habilitar ou desabilitar o gerenciamento remoto de pacotes de R
description: Habilitar o gerenciamento remoto de pacotes de R em SQL Server 2016 R Services ou SQL Server Serviços de Machine Learning (no banco de dados)
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 260109e978c8997622f24c41341e11f1e2efa7cc
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715628"
---
# <a name="enable-or-disable-remote-package-management-for-sql-server"></a>Habilitar ou desabilitar o gerenciamento de pacotes remoto para SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve como habilitar o gerenciamento remoto de pacotes R de uma estação de trabalho cliente ou de um Machine Learning Server diferente. Depois que o recurso gerenciamento de pacotes tiver sido habilitado no SQL Server, você poderá usar comandos RevoScaleR em um cliente para instalar pacotes no SQL Server.

> [!NOTE]
> Há suporte para o gerenciamento de bibliotecas de R no momento; o suporte para Python está no roteiro.

Por padrão, o recurso de gerenciamento de pacotes externo para SQL Server está desabilitado. Você deve executar um script separado para habilitar o recurso, conforme descrito na próxima seção.

## <a name="overview-of-process-and-tools"></a>Visão geral do processo e das ferramentas

Para habilitar ou desabilitar o gerenciamento de pacotes no SQL Server, use o utilitário de linha de comando **RegisterRExt. exe**, que está incluído no pacote **RevoScaleR** .

[Habilitar](#bkmk_enable) esse recurso é um processo de duas etapas, exigindo um administrador de banco de dados: você habilita o gerenciamento de pacotes na instância de SQL Server (uma vez por SQL Server instância) e, em seguida, habilita o gerenciamento de pacotes no banco de dados SQL (uma vez por SQL Server banco de dados ).

A [desabilitação](#bkmk_disable) do recurso de gerenciamento de pacotes também requer etapas do multipel: você remove os pacotes de nível de banco de dados e as permissões (uma vez por banco de dados) e, em seguida, remove as funções do servidor (uma vez por instância).

## <a name="bkmk_enable"></a>Habilitar o gerenciamento de pacotes

1. Em SQL Server, abra um prompt de comando com privilégios elevados e navegue até a pasta que contém o utilitário RegisterRExt. exe. O local padrão é `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`.

2. Execute o comando a seguir, fornecendo os argumentos apropriados para o seu ambiente:

    `RegisterRExt.exe /install pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Esse comando cria objetos em nível de instância no computador SQL Server que são necessários para o gerenciamento de pacotes. Ele também reinicia a barra inicial da instância.

    Se você não especificar uma instância, a instância padrão será usada. Se você não especificar um usuário, o contexto de segurança atual será usado. Por exemplo, o comando a seguir habilita o gerenciamento de pacotes na instância no caminho do RegisterRExt. exe, usando as credenciais do usuário que abriu o prompt de comando:

    `REgisterRExt.exe /install pkgmgmt`

3. Para adicionar o gerenciamento de pacotes a um banco de dados específico, execute o seguinte comando em um prompt de comando elevado:

    `RegisterRExt.exe /install pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    Este comando cria alguns artefatos de banco de dados, incluindo as seguintes funções de banco de dados que `rpkgs-users`são `rpkgs-private`usadas para `rpkgs-shared`controlar permissões de usuário:, e.

    Por exemplo, o comando a seguir habilita o gerenciamento de pacotes no banco de dados, na instância em que RegisterRExt é executado. Se você não especificar um usuário, o contexto de segurança atual será usado.

    `RegisterRExt.exe /install pkgmgmt /database:TestDB`

4. Repita o comando para cada banco de dados em que os pacotes devem ser instalados.

5. Para verificar se as novas funções foram criadas com êxito, em SQL Server Management Studio, clique no banco de dados, expanda **segurança**e expanda **funções de banco de dados**.

    Você também pode executar uma consulta em sys. database_principals, como o seguinte:

    ```sql
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

Depois de habilitar esse recurso, você pode usar a função RevoScaleR para instalar ou desinstalar pacotes de um cliente R remoto.

## <a name="bkmk_disable"></a>Desabilitar o gerenciamento de pacotes

1. Em um prompt de comandos com privilégios elevados, execute o utilitário RegisterRExt novamente e desabilite o gerenciamento de pacotes no nível do banco de dados:

    `RegisterRExt.exe /uninstall pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    Este comando remove objetos de banco de dados relacionados ao gerenciamento de pacotes do banco de dados especificado. Ele também remove todos os pacotes que foram instalados do local do sistema de arquivos protegido no computador SQL Server.

2. Repita esse comando em cada banco de dados em que o gerenciamento de pacotes foi usado.

3.  Adicional Depois que todos os bancos de dados tiverem sido limpos dos pacotes usando a etapa anterior, execute o seguinte comando em um prompt de comando elevado:

    `RegisterRExt.exe /uninstall pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando Remove o recurso de gerenciamento de pacotes da instância do. Talvez seja necessário reiniciar manualmente o serviço Launchpad mais uma vez para ver as alterações.

## <a name="next-steps"></a>Próximas etapas

+ [Usar o RevoScaleR para instalar novos pacotes de R](use-revoscaler-to-manage-r-packages.md)
+ [Dicas para instalar pacotes de R](packages-installed-in-user-libraries.md)
+ [Pacotes padrão](../package-management/default-packages.md)
