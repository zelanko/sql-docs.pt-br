---
title: Suporte do driver PHP para LocalDB
description: Saiba como os drivers da Microsoft para PHP para SQL Server são compatíveis com conexões com instâncias de banco de dados LocalDB.
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47bcfa16712e0ef227da7c7ae53de14aa42deacb
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726750"
---
# <a name="support-for-localdb"></a>Suporte ao LocalDB

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

O LocalDB é uma versão leve do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está disponível desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Este tópico descreve como conectar-se a um banco de dados em uma instância do LocalDB.

## <a name="remarks"></a>Comentários

Para obter mais informações sobre o LocalDB, inclusive como instalá-lo e configurar a instância dele, confira os tópico Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Express LocalDB.

Em suma, o LocalDB permite:

-   Usar **sqllocaldb.exe i** para descobrir o nome da instância padrão.

-   Usar a palavra-chave da cadeia de conexão **AttachDBFilename** para especificar o arquivo de banco de dados que o servidor deve anexar. Ao usar **AttachDBFilename**, se você não especificar o nome do banco de dados com a palavra-chave da cadeia de conexão **Database** , o banco de dados será removido da instância do LocalDB quando o aplicativo for fechado.

-   Especifique uma instância do LocalDB em sua cadeia de conexão. Por exemplo, veja um exemplo de cadeia de conexão SQLSRV:

    ```php
    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array( 'Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF','Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF'));
    ```

    Veja abaixo um exemplo de cadeia de conexão PDO_SQLSRV:  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

Se necessário, você pode criar uma instância do LocalDB com sqllocaldb.exe. Você também pode usar sqlcmd.exe para adicionar e modificar bancos de dados em uma instância do LocalDB. Por exemplo, `sqlcmd -S (localdb)\v11.0`. (Ao executar no IIS, você precisa executar no âmbito da conta correta para obter os mesmos resultados que quando você executa na linha de comando; confira [Usar o LocalDB com o IIS Completo, Parte 2: propriedade da instância](/archive/blogs/sqlexpress/using-localdb-with-full-iis-part-2-instance-ownership) para obter mais informações.)

Os seguintes exemplos são cadeias de conexão que usam o driver SQLSRV que se conecta a um banco de dados em uma instância nomeada do LocalDB chamada myInstance:

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

Os seguintes exemplos são cadeias de conexão que usam o driver PDO_SQLSRV que se conecta a um banco de dados em uma instância nomeada do LocalDB chamada myInstance:  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

Para obter instruções sobre como instalar o LocalDB, confira a [documentação do LocalDB](../../database-engine/configure-windows/sql-server-express-localdb.md). Se você usar sqlcmd.exe para modificar os dados em sua instância do LocalDB, precisará do [utilitário do sqlcmd](../../tools/sqlcmd-utility.md).

## <a name="see-also"></a>Consulte Também

[Conectando-se ao servidor](../../connect/php/connecting-to-the-server.md)