---
title: Suporte do SqlClient para LocalDB
description: Descreve o suporte do SqlClient para bancos de dados LocalDB.
ms.date: 08/15/2019
ms.assetid: cf796898-5575-46f2-ae6e-21e5aa8c4123
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 14cbe4ccf227c9462d2a2dc19fb42d913ca7bc5a
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451976"
---
# <a name="sqlclient-support-for-localdb"></a>Suporte do SqlClient para LocalDB

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

A partir do SQL Server nome do código Denali, uma versão leve do SQL Server, chamada LocalDB, estará disponível. Este tópico discute como se conectar a um banco de dados LocalDB.  
  
## <a name="remarks"></a>Remarks  
Para obter mais informações sobre o LocalDB, inclusive como instalá-lo e configurar sua instância do LocalDB, confira os Manuais Online do SQL Server.  
  
Para resumir o que você pode fazer com o LocalDB:  
  
- Crie e inicie instâncias do LocalDB com sqllocaldb. exe ou seu arquivo app. config.  
  
- Use sqlcmd.exe para adicionar e modificar bancos de dados em uma instância do LocalDB. Por exemplo, `sqlcmd -S (localdb)\myinst`.  
  
- Use a palavra-chave da cadeia de conexão `AttachDBFilename` para adicionar um banco de dados à instância do LocalDB. Ao usar `AttachDBFilename`, se você não especificar o nome do banco de dados com a palavra-chave da cadeia de conexão `Database`, o banco de dados será removido da instância do LocalDB quando o aplicativo for fechado.  
  
- Especifique uma instância do LocalDB em sua cadeia de conexão. Por exemplo, o nome da instância é `myInstance`, a cadeia de conexão inclui:  
  
```console
server=(localdb)\\myInstance  
```  
  
`User Instance=True` não é permitido ao se conectar a um banco de dados LocalDB.  
  
Você pode baixar o LocalDB de [Microsoft SQL Server o Feature Pack 2012](https://www.microsoft.com/download/en/details.aspx?id=29065). Se você for usar o sqlcmd. exe para modificar dados em sua instância de LocalDB, precisará do sqlcmd do SQL Server 2012, que também pode ser obtido do SQL Server Feature Pack 2012.  
  
## <a name="programmatically-create-a-named-instance"></a>Criar programaticamente uma instância nomeada  
Um aplicativo pode criar uma instância nomeada e especificar um banco de dados da seguinte maneira:  
  
- Especifique as instâncias de LocalDB a serem criadas no arquivo app. config, da seguinte maneira.  O número de versão da instância deve ser igual ao número de versão da sua instalação do LocalDB.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <configSections>  
        <section  
        name="system.data.localdb"  
        type="System.Data.LocalDBConfigurationSection,System.Data,Version=4.0.0.0,Culture=neutral,PublicKeyToken=b77a5c561934e089"/>  
      </configSections>  
      <system.data.localdb>  
        <localdbinstances>  
          <add name="myInstance" version="11.0" />  
        </localdbinstances>  
      </system.data.localdb>  
    </configuration>  
    ```  
  
- Especifique o nome da instância usando a palavra-chave da cadeia de conexão `server`.  O nome da instância especificado na palavra-chave da cadeia de conexão `server` deve corresponder ao nome especificado no arquivo app. config.  
  
- Use a palavra-chave da cadeia de conexão `AttachDBFilename` para especificar o. Arquivo MDF.  
  
## <a name="next-steps"></a>Próximas etapas
- [Recursos do SQL Server e ADO.NET](sql-server-features-adonet.md)
