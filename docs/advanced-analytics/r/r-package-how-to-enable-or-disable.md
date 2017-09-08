---
title: Como habilitar ou desabilitar o gerenciamento de pacotes de R | Microsoft Docs
ms.custom: 
ms.date: 12/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e384893-04da-43f9-b100-bfe99888f085
caps.latest.revision: 7
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aac055d9a2337f1278d648fbcd17435afe1bd3b3
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="r-package---how-to-enable-or-disable"></a>Pacote de R – Como habilitar ou desabilitar

Por padrão, o gerenciamento de pacotes é desabilitado em uma instância do SQL Server, mesmo se o R Services for instalado. Para habilitar esse recurso há um processo de duas etapas que deve ser executado por um administrador de banco de dados: 

1. Habilitar o gerenciamento de pacotes na instância do SQL Server (uma vez por instância do SQL Server) 
2. Habilitar o gerenciamento de pacotes no banco de dados SQL (uma vez por banco de dados do SQL Server) 


Para desabilitar o recurso de gerenciamento de pacotes, fazer o processo inverso para remover as permissões e os pacotes do nível de banco de dados e, em seguida, remova as funções do servidor:
 
1. Desabilitar o gerenciamento de pacotes em cada banco de dados (uma vez por banco de dados) 
2. Desabilitar o gerenciamento de pacotes na instância do SQL Server (uma vez por instância) 

> [!IMPORTANT]
> Esse recurso está em desenvolvimento. Esteja ciente de que a sintaxe ou a funcionalidade poderá mudar em versões posteriores. 

### <a name="to-enable-package-management"></a>Para habilitar o gerenciamento de pacotes

Para habilitar ou desabilitar o gerenciamento de pacotes é necessário o utilitário de linha de comando **RegisterRExt.exe**, que é incluído com o pacote **RevoScaleR** instalado com o SQL Server R Services. o local padrão é:

`<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe` 
    
1. Abra um prompt de comandos com privilégios elevados e use o seguinte comando:

    `RegisterRExt.exe /installpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando cria os artefatos de nível de instância no computador SQL Server que são necessários para o gerenciamento de pacotes. 

2. Para adicionar gerenciamento de pacotes no nível de banco de dados, execute o seguinte comando em um prompt de comandos com privilégios elevados para cada banco de dados em que os pacotes devem ser instalados: 

    `RegisterRExt.exe /installpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]` 

    Este comando cria alguns artefatos de banco de dados, incluindo as seguintes funções de banco de dados que são necessárias para controlar permissões de usuário: **rpkgs-users**, **rpkgs-private**e **rpkgs-shared** 

### <a name="to-disable-package-management"></a>Para desabilitar o gerenciamento de pacotes 

1. Em um prompt de comandos com privilégios elevados, execute o comando a seguir para desabilitar o gerenciamento de pacotes no nível do banco de dados:

   `RegisterRExt.exe /uninstallpkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]` 

    Este comando removerá os artefatos de banco de dados relacionados ao gerenciamento de pacotes do banco de dados especificado.  O comando também removerá todos os pacotes do local do sistema de arquivos protegido no computador do SQL Server, que foram instalados em cada banco de dados.
    
    O comando deve ser executado uma vez para cada banco de dados no qual o gerenciamento de pacotes foi usado.
 
2. (Opcional) Para remover completamente o recurso de gerenciamento de pacotes da instância, depois que todos os bancos de dados foram limpos dos pacotes usando a etapa anterior, execute o seguinte comando em um prompt de comandos com privilégios elevados:

    `RegisterRExt.exe /uninstallpkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Este comando remove os artefatos de nível de instância usados pelo gerenciamento de pacotes da instância do SQL Server. 


## <a name="see-also"></a>Consulte também
[Gerenciamento de pacotes de R para SQL Server R Services](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)

