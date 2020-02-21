---
title: Suporte do SqlClient para LocalDB
description: Descreve o suporte SqlClient para bancos de dados LocalDB.
ms.date: 08/15/2019
ms.assetid: cf796898-5575-46f2-ae6e-21e5aa8c4123
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 819a92294fb3d316c172d8c3719bbf659bfa9f86
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75244004"
---
# <a name="sqlclient-support-for-localdb"></a>Suporte do SqlClient para LocalDB

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Do SQL Server code name Denali em diante, uma versão leve do SQL Server, chamada LocalDB, estará disponível. Este tópico descreve como conectar-se a um banco de dados do LocalDB.  
  
## <a name="remarks"></a>Comentários  
Para obter mais informações sobre o LocalDB, inclusive como instalá-lo e configurar sua instância do LocalDB, confira os Manuais Online do SQL Server.  
  
Para resumir o que você pode fazer com o LocalDB:  
  
- Crie e inicie instâncias do LocalDB com sqllocaldb.exe ou seu arquivo app.config.  
  
- Use sqlcmd.exe para adicionar e modificar bancos de dados em uma instância do LocalDB. Por exemplo, `sqlcmd -S (localdb)\myinst`.  
  
- Use a palavra-chave da cadeia de conexão `AttachDBFilename` para adicionar um banco de dados à instância do LocalDB. Ao usar `AttachDBFilename`, se você não especificar o nome do banco de dados com a palavra-chave da cadeia de conexão `Database`, o banco de dados será removido da instância do LocalDB quando o aplicativo for fechado.  
  
- Especifique uma instância do LocalDB em sua cadeia de conexão. Por exemplo, o nome da instância é `myInstance`, a cadeia de conexão incluiria:  
  
```console
server=(localdb)\\myInstance  
```  
  
`User Instance=True` não é permitido ao se conectar a um banco de dados LocalDB.  
  
Você pode baixar LocalDB do [Microsoft SQL Server 2012 Feature Pack](https://www.microsoft.com/download/en/details.aspx?id=29065). Se você usar sqlcmd.exe para modificar dados em sua instância LocalDB, precisará do sqlcmd do SQL Server 2012, que você também poderá obter do SQL Server 2012 Feature Pack.  
  
## <a name="programmatically-create-a-named-instance"></a>Criar programaticamente uma instância nomeada  
Um aplicativo pode criar uma instância nomeada e especificar um banco de dados da seguinte maneira:  
  
- Especifique as instâncias LocalDB a serem criadas no arquivo app.config, da maneira a seguir.  O número de versão da instância deve ser igual ao número de versão da sua instalação do LocalDB.  
  
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
  
- Especifique o nome da instância que usa a palavra-chave da cadeia de conexão `server`.  O nome da instância especificado na palavra-chave da cadeia de conexão `server` deve corresponder ao nome especificado no arquivo app.config.  
  
- Use a palavra-chave da cadeia de conexão `AttachDBFilename` para especificar o arquivo .MDF.  
  
## <a name="next-steps"></a>Próximas etapas
- [Recursos do SQL Server e ADO.NET](sql-server-features-adonet.md)
