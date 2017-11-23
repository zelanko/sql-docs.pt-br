---
title: Habilitar ou desabilitar o gerenciamento de pacotes de R para o SQL Server | Microsoft Docs
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e384893-04da-43f9-b100-bfe99888f085
caps.latest.revision: "7"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fd19bc25e1e4602a54bf89e18c8959a282552f63
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="enable-or-disable-r-package-management-for-sql-server"></a>Habilitar ou desabilitar o gerenciamento de pacotes de R para o SQL Server

Este artigo descreve o processo de habilitar ou desabilitar o novo recurso de gerenciamento de pacote no SQL Server 2017. Esse recurso permite que o administrador de banco de dados controlar a instalação de pacote na instância. O recurso depende de novas funções de banco de dados para conceder aos usuários a capacidade de instalar os pacotes de R precisarem ou compartilhar pacotes com outros usuários.

Por padrão, o recurso de gerenciamento do pacote externo para o SQL Server está desabilitado, mesmo se os recursos de aprendizado de máquina foram instalados.

Para [habilitar](#bkmk_enable) esse recurso é um processo de duas etapas e requer a Ajuda de um administrador de banco de dados:

1.  Habilitar o gerenciamento de pacotes na instância do SQL Server (uma vez por instância do SQL Server)

2.  Habilitar o gerenciamento de pacotes no banco de dados SQL (uma vez por banco de dados do SQL Server)

Para [desabilitar](#bkmk_disable) o recurso de gerenciamento de pacote, reverter o processo para remover pacotes de nível de banco de dados e permissões e, em seguida, remova as funções do servidor:

1.  Desabilitar o gerenciamento de pacotes em cada banco de dados (uma vez por banco de dados)

2.  Desabilitar o gerenciamento de pacotes na instância do SQL Server (uma vez por instância)

## <a name="bkmk_enable"></a>Habilitar o gerenciamento de pacote

Para habilitar ou desabilitar o gerenciamento de pacote requer que o utilitário de linha de comando **RegisterRExt.exe**, que é incluído com o **RevoScaleR** pacote.

1. Abra um prompt de comando com privilégios elevados e navegue até a pasta que contém o utilitário, RegisterRExt.exe. O local padrão é `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`.

2. Execute o comando a seguir, fornecendo argumentos apropriado para seu ambiente:

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando cria objetos de nível de instância no computador do SQL Server que são necessários para o gerenciamento de pacotes. Ele também reinicia a barra inicial para a instância.

    Se você não especificar uma instância, a instância padrão será usada.

    Se você não especificar um usuário, o contexto de segurança atual será usado.

2.  Para adicionar o gerenciamento de pacotes no nível do banco de dados, execute o seguinte comando em um prompt de comando elevado:

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    Este comando cria alguns artefatos do banco de dados, incluindo as seguintes funções de banco de dados que são usadas para controlar permissões de usuário: `rpkgs-users`, `rpkgs-private`, e `rpkgs-shared`.

    Se você não especificar um usuário, o contexto de segurança atual será usado.

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

4.  Depois que o recurso foi habilitado, qualquer usuário com as permissões apropriadas pode usar o [criar biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrução T-SQL para adicionar pacotes. Para obter um exemplo de como isso funciona, consulte [instalar outros pacotes no SQL Server](install-additional-r-packages-on-sql-server.md).

## <a name="bkmk_disable"></a>Desabilitar o gerenciamento de pacote

1.  Em um prompt de comandos com privilégios elevados, execute o comando a seguir para desabilitar o gerenciamento de pacotes no nível do banco de dados:

    `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    Execute este comando uma vez para cada banco de dados onde o gerenciamento de pacotes foi usado. Este comando removerá os objetos de banco de dados relacionados ao gerenciamento de pacotes do banco de dados especificado. Ela também removerá todos os pacotes que foram instalados a partir do local de sistema de arquivos protegidos no computador do SQL Server.

2.  (Opcional) Depois que todos os bancos de dados foi limpo de pacotes usando a etapa anterior, execute o seguinte comando em um prompt de comando elevado:

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando remove o recurso de gerenciamento de pacote da instância.

## <a name="see-also"></a>Consulte também

[Gerenciamento de pacotes R para SQL Server](r-package-management-for-sql-server-r-services.md)
