---
title: Suporte para LocalDB | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f6da7f1aed956c8b2f5c71496c9c121f6006eabb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935954"
---
# <a name="support-for-localdb"></a>Suporte ao LocalDB

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

O LocalDB é uma versão leve [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do que está disponível desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o. Este tópico descreve como conectar-se a um banco de dados em uma instância do LocalDB.

## <a name="remarks"></a>Remarks

Para obter mais informações sobre o LocalDB, incluindo como instalar o LocalDB e configurar sua instância do LocalDB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte o tópico [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] nos manuais online sobre o Express LocalDB.

Em resumo, o LocalDB permite que você:

-   Usar **sqllocaldb.exe i** para descobrir o nome da instância padrão.

-   Usar a palavra-chave da cadeia de conexão **AttachDBFilename** para especificar o arquivo de banco de dados que o servidor deve anexar. Ao usar **AttachDBFilename**, se você não especificar o nome do banco de dados com a palavra-chave da cadeia de conexão **Database** , o banco de dados será removido da instância do LocalDB quando o aplicativo for fechado.

-   Especifique uma instância do LocalDB em sua cadeia de conexão. Por exemplo, aqui está um exemplo de cadeia de conexão SQLSRV:

    ```php
    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array( 'Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF','Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF'));
    ```

    A seguir está um exemplo de cadeia de conexão PDO_SQLSRV:  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

Se necessário, você pode criar uma instância do LocalDB com sqllocaldb.exe. Você também pode usar sqlcmd.exe para adicionar e modificar bancos de dados em uma instância do LocalDB. Por exemplo, `sqlcmd -S (localdb)\v11.0`. (Ao executar no IIS, você precisa executar sob a conta correta para obter os mesmos resultados que ao executar na linha de comando; consulte usando o [LocalDB com o IIS completo, parte 2: propriedade da instância](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-2-instance-ownership.aspx) para obter mais informações.)

Veja a seguir exemplos de cadeias de conexão usando o driver SQLSRV que se conecta a um banco de dados em uma instância nomeada do LocalDB chamada MyInstance:

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

Veja a seguir exemplos de cadeias de conexão usando o driver PDO_SQLSRV que se conecta a um banco de dados em uma instância nomeada do LocalDB chamada MyInstance:  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

Para obter instruções sobre como instalar o LocalDB, consulte a [documentação do LocalDB](../../database-engine/configure-windows/sql-server-2016-express-localdb.md). Se você usar sqlcmd. exe para modificar dados em sua instância de LocalDB, será necessário o [utilitário sqlcmd](../../tools/sqlcmd-utility.md).

## <a name="see-also"></a>Consulte Também

[Conectando-se ao servidor](../../connect/php/connecting-to-the-server.md)
