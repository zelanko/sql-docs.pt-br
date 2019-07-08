---
title: Criar um banco de dados habilitado para FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], FILESTREAM-enabled databases
ms.assetid: 0fc16356-76f7-44b8-a58b-f0b7c43694ec
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d77a587d943cac4844b48304d03c58c837947477
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67580512"
---
# <a name="create-a-filestream-enabled-database"></a>Criar um banco de dados habilitado para FILESTREAM
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico mostra como criar um banco de dados que oferece suporte a FILESTREAM. Como o FILESTREAM usa um tipo especial de grupo de arquivos, ao criar o banco de dados, será preciso especificar a cláusula CONTAINS FILESTREAM para pelo menos um grupo de arquivos.  
  
 Um grupo de arquivos FILESTREAM pode conter mais de um arquivo. Para ver um exemplo de código que demonstra como criar um grupo de arquivos FILESTREAM que contém vários arquivos, consulte [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
### <a name="to-create-a-filestream-enabled-database"></a>Para criar um banco de dados habilitado para FILESTREAM  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique em **Nova Consulta** para exibir o Editor de Consultas.  
  
2.  Copie o código [!INCLUDE[tsql](../../includes/tsql-md.md)] do exemplo a seguir no Editor de Consultas. Esse código [!INCLUDE[tsql](../../includes/tsql-md.md)] cria um banco de dados habilitado para FILESTREAM chamado Arquivo.  
  
    > [!NOTE]  
    >  Para este script, o diretório C:\Data deve existir.  
  
3.  Para construir o banco de dados, clique em **Executar**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="example"></a>Exemplo  
 O exemplo de código a seguir cria um banco de dados chamado `Archive`. O banco de dados contém três grupos de arquivos: `PRIMARY`, `Arch1`e `FileStreamGroup1`. `PRIMARY` e `Arch1` são grupos de arquivos normais que não podem conter dados FILESTREAM. `FileStreamGroup1` é o grupo de arquivos `FILESTREAM` .  
  
 [!code-sql[FILESTREAM#FS_CreateDB](../../relational-databases/blob/codesnippet/tsql/create-a-filestream-enab_1.sql)]  
  
 Para um grupo de arquivos `FILESTREAM` , `FILENAME` faz referência a um caminho. O caminho até a última pasta deve existir e a última pasta não deve existir. Neste exemplo, `c:\data` deve existir. Entretanto, a subpasta `filestream1` não pode existir quando você executar a instrução `CREATE DATABASE` . Para saber mais sobre a sintaxe, consulte [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
 Após executar o exemplo anterior, um arquivo filestream.hdr e uma pasta $FSLOG devem aparecer na pasta c:\Data\filestream1. O arquivo filestream.hdr é um arquivo de cabeçalho para o contêiner FILESTREAM.  
  
> [!IMPORTANT]  
>  O arquivo filestream.hdr é um arquivo de sistema importante. Ele contém informações de cabeçalho FILESTREAM. Não remova nem modifique esse arquivo.  
  
 Em bancos de dados existentes, você pode usar a instrução [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) para adicionar um grupo de arquivos FILESTREAM.  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  
