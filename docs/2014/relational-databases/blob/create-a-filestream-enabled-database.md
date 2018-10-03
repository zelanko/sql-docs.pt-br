---
title: Criar um banco de dados habilitado para FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], FILESTREAM-enabled databases
ms.assetid: 0fc16356-76f7-44b8-a58b-f0b7c43694ec
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4cd07bd559c1f21eb6ea055a6c132437a63a4b71
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48184646"
---
# <a name="create-a-filestream-enabled-database"></a>Criar um banco de dados habilitado para FILESTREAM
  Este tópico mostra como criar um banco de dados que oferece suporte a FILESTREAM. Como o FILESTREAM usa um tipo especial de grupo de arquivos, ao criar o banco de dados, será preciso especificar a cláusula CONTAINS FILESTREAM para pelo menos um grupo de arquivos.  
  
 Um grupo de arquivos FILESTREAM pode conter mais de um arquivo. Para ver um exemplo de código que demonstra como criar um grupo de arquivos FILESTREAM que contém vários arquivos, consulte [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql).  
  
### <a name="to-create-a-filestream-enabled-database"></a>Para criar um banco de dados habilitado para FILESTREAM  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique em **Nova Consulta** para exibir o Editor de Consultas.  
  
2.  Copie o [!INCLUDE[tsql](../../includes/tsql-md.md)] código cria um banco de dados habilitado para FILESTREAM chamado arquivo morto.  
  
    > [!NOTE]  
    >  Para este script, o diretório C:\Data deve existir.  
  
3.  Para construir o banco de dados, clique em **Executar**.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir cria um banco de dados chamado `Archive`. O banco de dados contém três grupos de arquivos: `PRIMARY`, `Arch1`e `FileStreamGroup1`. `PRIMARY` e `Arch1` são grupos de arquivos normais que não podem conter dados FILESTREAM. `FileStreamGroup1` é o grupo de arquivos `FILESTREAM` .  
  
```tsql  
CREATE DATABASE Archive   
ON  
PRIMARY ( NAME = Arch1,  
    FILENAME = 'c:\data\archdat1.mdf'),  
FILEGROUP FileStreamGroup1 CONTAINS FILESTREAM( NAME = Arch3,  
    FILENAME = 'c:\data\filestream1')  
LOG ON  ( NAME = Archlog1,  
    FILENAME = 'c:\data\archlog1.ldf')  
GO  
```  
  
 Para um grupo de arquivos `FILESTREAM` , `FILENAME` faz referência a um caminho. O caminho até a última pasta deve existir e a última pasta não deve existir. Neste exemplo, `c:\data` deve existir. Entretanto, a subpasta `filestream1` não pode existir quando você executar a instrução `CREATE DATABASE` . Para saber mais sobre a sintaxe, consulte [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql).  
  
 Após executar o exemplo anterior, um arquivo filestream.hdr e uma pasta $FSLOG devem aparecer na pasta c:\Data\filestream1. O arquivo filestream.hdr é um arquivo de cabeçalho para o contêiner FILESTREAM.  
  
> [!IMPORTANT]  
>  O arquivo filestream.hdr é um arquivo de sistema importante. Ele contém informações de cabeçalho FILESTREAM. Não remova nem modifique esse arquivo.  
  
 Em bancos de dados existentes, você pode usar a instrução [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) para adicionar um grupo de arquivos FILESTREAM.  
  
## <a name="see-also"></a>Consulte também  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
  
