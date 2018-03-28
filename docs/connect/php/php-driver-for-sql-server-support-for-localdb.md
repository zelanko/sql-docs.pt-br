---
title: Suporte para o LocalDB | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.reviewer: ''
ms.suite: sql
ms.prod_service: drivers
ms.component: php
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9315847a8e36520b360d16681ffe5b00f08d6975
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="support-for-localdb"></a>Suporte para o LocalDB

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

O LocalDB é uma versão leve do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] que está disponível desde o [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]. Este tópico descreve como conectar-se a um banco de dados em uma instância do LocalDB.

## <a name="remarks"></a>Remarks

Para obter mais informações sobre o LocalDB, inclusive como instalá-lo e configurar sua instância LocalDB, consulte o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tópico dos Manuais Online em [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Express LocalDB.

Em suma, o LocalDB permite:

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

Para obter instruções sobre como instalar o LocalDB, consulte o [LocalDB documentação](../../database-engine/configure-windows/sql-server-2016-express-localdb.md). Se você usar sqlcmd.exe para modificar dados em sua instância de LocalDB, será necessário o [utilitário sqlcmd](../../tools/sqlcmd-utility.md).

## <a name="see-also"></a>Consulte também

[Conectando-se ao servidor](../../connect/php/connecting-to-the-server.md)
