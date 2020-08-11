---
title: Habilitar ou desabilitar o gerenciamento de pacotes de R
description: Habilite o gerenciamento remoto de pacotes de R nos SQL Server 2016 R Services ou Serviços de Machine Learning do SQL Server (no banco de dados)
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 06/13/2019
ms.topic: how-to
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 1a18d56d1dcf0733f080da7cf8247421c669a4aa
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85757139"
---
# <a name="enable-or-disable-remote-package-management-for-sql-server"></a>Habilitar ou desabilitar o gerenciamento de pacotes para SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este artigo descreve como habilitar o gerenciamento remoto de pacotes de R de uma estação de trabalho cliente ou de um Machine Learning Server diferente. Após a habilitação do recurso de gerenciamento de pacotes no SQL Server, você pode usar comandos RevoScaleR em um cliente para instalar pacotes no SQL Server.

Por padrão, o recurso de gerenciamento de pacotes externo para SQL Server está desabilitado. Você deve executar um script separado para habilitar o recurso, conforme descrito na próxima seção.

## <a name="overview-of-process-and-tools"></a>Visão geral do processo e das ferramentas

Para habilitar ou desabilitar o gerenciamento de pacotes no SQL Server, use o utilitário de linha de comando **RegisterRExt.exe**, que é incluído com o pacote **RevoScaleR**.

[Habilitar](#bkmk_enable) esse recurso é um processo de duas etapas, exigindo um administrador de banco de dados: você habilita o gerenciamento de pacotes na instância do SQL Server (uma vez por instância do SQL Server) e, então, habilita o gerenciamento de pacotes no Banco de Dados SQL (uma vez por banco de dados do SQL Server).

[Desabilitar](#bkmk_disable) o recurso de gerenciamento de pacotes também requer várias etapas: você remove os pacotes de nível de banco de dados e as permissões (uma vez por banco de dados) e, em seguida, remove as funções do servidor (uma vez por instância).

## <a name="enable-package-management"></a><a name="bkmk_enable"></a> Habilitar o gerenciamento de pacotes

1. No SQL Server, abra um prompt de comandos com privilégios elevados e navegue até a pasta que contém o utilitário RegisterRExt.exe. A localização padrão é `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`.

2. Execute o seguinte comando, fornecendo os argumentos apropriados para seu ambiente:

    `RegisterRExt.exe /install pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando cria os objetos de nível de instância no computador SQL Server que são necessários para o gerenciamento de pacotes. Ele também reinicia a Barra inicial da instância.

    Se você não especificar uma instância, a instância padrão será usada. Se você não especificar um usuário, o contexto de segurança atual será usado. Por exemplo, o seguinte comando habilita o gerenciamento de pacotes na instância padrão, usando as credenciais do usuário que abriu o prompt de comando:

    `REgisterRExt.exe /install pkgmgmt`

3. Para adicionar o gerenciamento de pacotes a um banco de dados específico, execute o seguinte comando em um prompt de comandos com privilégios elevados:

    `RegisterRExt.exe /install pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    Este comando cria alguns artefatos de banco de dados, incluindo as seguintes funções de banco de dados que são usadas para controlar permissões de usuário: `rpkgs-users`, `rpkgs-private`e `rpkgs-shared`.

    Por exemplo, o comando a seguir habilita o gerenciamento de pacotes no banco de dados, na instância padrão. Se você não especificar um usuário, o contexto de segurança atual será usado.

    `RegisterRExt.exe /install pkgmgmt /database:TestDB`

4. Repita o comando para cada banco de dados em que os pacotes devem ser instalados.

5. Para verificar se as novas funções foram criadas com êxito, em SQL Server Management Studio, clique no banco de dados, expanda **Segurança**e expanda **Funções de Banco de Dados**.

    Você também pode executar uma consulta em sys.database_principals como a seguinte:

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

Após habilitar esse recurso, você pode usar a função RevoScaleR para instalar ou desinstalar pacotes de um cliente R remoto.

## <a name="disable-package-management"></a><a name="bkmk_disable"></a> Desabilitar o gerenciamento de pacotes

1. Em um prompt de comandos com privilégios elevados, execute o utilitário RegisterRExt novamente e desabilite o gerenciamento de pacotes no nível do banco de dados:

    `RegisterRExt.exe /uninstall pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    Este comando remove objetos de banco de dados relacionados ao gerenciamento de pacotes do banco de dados especificado. Ele também remove todos os pacotes que foram instalados da localização do sistema de arquivos protegida no computador do SQL Server.

2. Repita esse comando em cada banco de dados em que o gerenciamento de pacotes foi usado.

3.  (Opcional) Depois que todos os bancos de dados tiverem sido limpos dos pacotes usando a etapa anterior, execute o seguinte comando em um prompt de comandos com privilégios elevados:

    `RegisterRExt.exe /uninstall pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando remove o recurso de gerenciamento de pacotes da instância. Talvez seja necessário reiniciar manualmente o serviço do Launchpad mais uma vez para ver as alterações.

## <a name="next-steps"></a>Próximas etapas

+ [Usar o RevoScaleR para instalar pacotes de R](install-r-packages-with-revoscaler.md)
+ [Obter informações sobre o pacote do R](r-package-information.md)
+ [Dicas para usar pacotes de R](tips-for-using-r-packages.md)
