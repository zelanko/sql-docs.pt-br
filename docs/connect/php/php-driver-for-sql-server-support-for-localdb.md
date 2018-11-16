---
title: Suporte para o LocalDB | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 40c6bbf04f0c1fc5f2b4e2e360a3fcce5a68c6f7
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600466"
---
# <a name="support-for-localdb"></a>Suporte ao LocalDB

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

O LocalDB é uma versão leve do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está disponível desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Este tópico descreve como conectar-se a um banco de dados em uma instância do LocalDB.

## <a name="remarks"></a>Remarks

Para obter mais informações sobre o LocalDB, inclusive como instalá-lo e configurar sua instância de LocalDB, consulte o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tópico dos Manuais Online sobre [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Express LocalDB.

Em suma, o LocalDB permite:

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

Se necessário, você pode criar uma instância do LocalDB com sqllocaldb.exe. Você também pode usar sqlcmd.exe para adicionar e modificar bancos de dados em uma instância do LocalDB. Por exemplo, `sqlcmd -S (localdb)\v11.0`. (Quando em execução no IIS, você precisa ser executado com a conta correta para obter os mesmos resultados que quando você executa na linha de comando; consulte [usando LocalDB com o IIS completo, parte 2: propriedade de instância](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-2-instance-ownership.aspx) para obter mais informações.)

Estas são as cadeias de conexão de exemplo usando o driver SQLSRV que se conectam a um banco de dados em um instância chamada myInstance nomeado de LocalDB:

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

Estas são as cadeias de conexão de exemplo usando o driver PDO_SQLSRV que se conectam a um banco de dados em um instância chamada myInstance nomeado de LocalDB:  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

Para obter instruções sobre como instalar o LocalDB, consulte o [documentação do LocalDB](../../database-engine/configure-windows/sql-server-2016-express-localdb.md). Se você usar sqlcmd.exe para modificar dados em sua instância de LocalDB, será necessário o [utilitário sqlcmd](../../tools/sqlcmd-utility.md).

## <a name="see-also"></a>Consulte Também

[Conectando-se ao servidor](../../connect/php/connecting-to-the-server.md)
