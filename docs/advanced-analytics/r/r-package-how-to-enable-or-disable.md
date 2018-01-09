---
title: Habilitar ou desabilitar o gerenciamento de pacotes de R para o SQL Server | Microsoft Docs
ms.custom: 
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e384893-04da-43f9-b100-bfe99888f085
caps.latest.revision: "7"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 3c3dab54416d680e0d021a2edf9fbe33d5a0d81f
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="enable-or-disable-r-package-management-for-sql-server"></a>Habilitar ou desabilitar o gerenciamento de pacotes de R para o SQL Server

Este artigo descreve um novo recurso de gerenciamento de pacote no SQL Server de 2017, projetado para permitir que o administrador de banco de dados controlar a instalação de pacote na instância usando o T-SQL em vez de R.

Após que o pacote gerenciamento frature está habilitado, você também pode usar comandos de R para instalar os pacotes em um gerenciamento de registros agrupados databae um cliente remoto.

> [!NOTE]
> Por padrão, o recurso de gerenciamento do pacote externo para o SQL Server está desabilitado, mesmo se os recursos de aprendizado de máquina foram instalados. 

## <a name="enable-package-management"></a>Habilitar o gerenciamento de pacote

Para [habilitar](#bkmk_enable) esse recurso é um processo de duas etapas, exigindo que um administrador de banco de dados:

1.  Habilitar o gerenciamento de pacotes na instância do SQL Server (uma vez por instância do SQL Server)

2.  Habilitar o gerenciamento de pacotes no banco de dados SQL (uma vez por banco de dados do SQL Server)

Para [desabilitar](#bkmk_disable) o recurso de gerenciamento de pacote, reverter o processo para remover pacotes de nível de banco de dados e permissões e, em seguida, remova as funções do servidor:

1.  Desabilitar o gerenciamento de pacotes em cada banco de dados (uma vez por banco de dados)

2.  Desabilitar o gerenciamento de pacotes na instância do SQL Server (uma vez por instância)

## <a name="bkmk_enable"></a>Habilitar o gerenciamento de pacote

Para habilitar ou desabilitar o gerenciamento de pacote, use o utilitário de linha de comando **RegisterRExt.exe**, que é incluído com o **RevoScaleR** pacote.

1. Abra um prompt de comando com privilégios elevados e navegue até a pasta que contém o utilitário, RegisterRExt.exe. O local padrão é `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`.

2. Execute o comando a seguir, fornecendo argumentos apropriados para seu ambiente:

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando cria objetos de nível de instância no computador do SQL Server que são necessários para o gerenciamento de pacotes. Ele também reinicia a barra inicial para a instância.

    Se você não especificar uma instância, a instância padrão será usada. Se você não especificar um usuário, o contexto de segurança atual será usado. Por exemplo, o comando a seguir habilita o gerenciamento de pacotes na instância no caminho do RegisterRExt.exe, usando as credenciais do usuário que abriu o prompt de comando:

    `REgisterRExt.exe /installpkgmgmt`

2.  Para adicionar o gerenciamento de pacotes para um banco de dados específico, execute o seguinte comando em um prompt de comando elevado:

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    Este comando cria alguns artefatos do banco de dados, incluindo as seguintes funções de banco de dados que são usadas para controlar permissões de usuário: `rpkgs-users`, `rpkgs-private`, e `rpkgs-shared`.

    Por exemplo, o comando a seguir permite o gerenciamento de pacote no banco de dados na instância onde RegisterRExt é executado. Se você não especificar um usuário, o contexto de segurança atual será usado. 

    `RegisterRExt.exe /installpkgmgmt /database:TestDB`

3. Repita o comando para cada banco de dados em que os pacotes devem ser instalados.

4.  Para verificar se as novas funções foram criadas com êxito, no SQL Server Management Studio, clique em banco de dados, expanda **segurança**e expanda **funções de banco de dados**.

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

4.  Depois que o recurso foi habilitado, você pode se conectar ao servidor e instalar ou sincronizar os pacotes remotamente, usando os comandos de R. Para obter um exemplo de como isso funciona, consulte [instalar outros pacotes no SQL Server](install-additional-r-packages-on-sql-server.md).

## <a name="bkmk_disable"></a>Desabilitar o gerenciamento de pacote

1.  Em um prompt de comando com privilégios elevados, execute o utilitário RegisterRExt novamente e desabilitar o pacote de gerenciamento no nível do banco de dados:

    `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    Este comando remove objetos de banco de dados relacionados ao gerenciamento de pacotes do banco de dados especificado. Ele também remove todos os pacotes que foram instalados a partir do local de sistema de arquivos protegidos no computador do SQL Server.

2. Execute este comando uma vez para cada banco de dados onde o gerenciamento de pacotes foi usado. 

3.  (Opcional) Depois que todos os bancos de dados foi limpo de pacotes usando a etapa anterior, execute o seguinte comando em um prompt de comando elevado:

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando remove o recurso de gerenciamento de pacote da instância. Talvez seja necessário reiniciar manualmente o serviço Launchpad mais uma vez para ver as alterações.

## <a name="see-also"></a>Consulte também

[Gerenciamento de pacotes R para SQL Server](r-package-management-for-sql-server-r-services.md)
