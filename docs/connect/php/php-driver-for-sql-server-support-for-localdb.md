---
title: Driver do PHP para SQL Server Support for LocalDB | Microsoft Docs
ms.custom: 
ms.date: 02/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: abf75fb674ea8da86c84c3605dadef61db8b3913
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="php-driver-for-sql-server-support-for-localdb"></a>Driver do PHP para o suporte do SQL Server para LocalDB

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

A partir do [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)], uma versão leve do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], denominada LocalDB, estarão disponíveis. Este tópico descreve como conectar-se a um banco de dados em uma instância do LocalDB.

## <a name="remarks"></a>Comentários

Para obter mais informações sobre o LocalDB, inclusive como instalá-lo e configurar sua instância LocalDB, consulte o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tópico dos Manuais Online em [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Express LocalDB.

Para resumir, o LocalDB permite:

-   Usar **sqllocaldb.exe i** para descobrir o nome da instância padrão.

-   Usar a palavra-chave da cadeia de conexão **AttachDBFilename** para especificar o arquivo de banco de dados que o servidor deve anexar. Ao usar **AttachDBFilename**, se você não especificar o nome do banco de dados com a palavra-chave da cadeia de conexão **Database** , o banco de dados será removido da instância do LocalDB quando o aplicativo for fechado.

-   Especifique uma instância de LocalDB em sua cadeia de conexão. Por exemplo, aqui está uma cadeia de caracteres de conexão do exemplo SQLSRV:

    ```php
    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array( 'Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF','Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF'));
    ```

    Em seguida, é uma cadeia de caracteres de conexão do exemplo PDO_SQLSRV:  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

Se necessário, você pode criar uma instância do LocalDB com sqllocaldb.exe. Você também pode usar sqlcmd.exe para adicionar e modificar bancos de dados em uma instância do LocalDB. Por exemplo, `sqlcmd -S (localdb)\v11.0`. (Quando em execução no IIS, você precisa executar sob a conta correta para obter os mesmos resultados que quando você executar a linha de comando; consulte [usando LocalDB com o IIS completo, parte 2: propriedade de instância](http://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-2-instance-ownership.aspx) para obter mais informações.)

A seguir estão as cadeias de conexão de exemplo usando o driver SQLSRV que se conectam a um banco de dados em um instância chamada myInstance nomeado de LocalDB:

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

A seguir estão as cadeias de conexão de exemplo usando o driver PDO_SQLSRV que se conectam a um banco de dados em um instância chamada myInstance nomeado de LocalDB:  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

Você pode baixar o LocalDB do [página do SQL Server 2012 feature pack](http://go.microsoft.com/fwlink/?LinkID=236805), ou o [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Express edition. Se você usar sqlcmd.exe para modificar dados em sua instância de LocalDB, será necessário sqlcmd de [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)], que pode ser obtido do download Utilitários de linha de comando no [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] página Feature Pack.

## <a name="see-also"></a>Consulte também

[Conectando-se ao servidor](../../connect/php/connecting-to-the-server.md)
