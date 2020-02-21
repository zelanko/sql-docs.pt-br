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
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67935954"
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

Se necessário, você pode criar uma instância do LocalDB com sqllocaldb.exe. Você também pode usar sqlcmd.exe para adicionar e modificar bancos de dados em uma instância do LocalDB. Por exemplo, `sqlcmd -S (localdb)\v11.0`. (Ao executar no IIS, você precisa executar no âmbito da conta correta para obter os mesmos resultados que quando você executa na linha de comando; confira [Usar o LocalDB com o IIS Completo, Parte 2: propriedade da instância](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-2-instance-ownership.aspx) para obter mais informações.)

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

Para obter instruções sobre como instalar o LocalDB, confira a [documentação do LocalDB](../../database-engine/configure-windows/sql-server-2016-express-localdb.md). Se você usar sqlcmd.exe para modificar os dados em sua instância do LocalDB, precisará do [utilitário do sqlcmd](../../tools/sqlcmd-utility.md).

## <a name="see-also"></a>Consulte Também

[Conectando-se ao servidor](../../connect/php/connecting-to-the-server.md)
