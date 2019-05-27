---
title: Acessar dados FILESTREAM com Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], Transact-SQL
ms.assetid: a6bf0ce7-7e5e-4a07-8917-ee526c9d0a05
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 067f14e857addc5f43a0b17d81d554997adbc09f
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66010437"
---
# <a name="access-filestream-data-with-transact-sql"></a>Acessar dados FILESTREAM com Transact-SQL
  Este tópico descreve como usar as instruções INSERT, UPDATE e DELETE do [!INCLUDE[tsql](../../includes/tsql-md.md)] para gerenciar dados FILESTREAM.  
  
> [!NOTE]  
>  Os exemplos citados neste tópico exigem o banco de dados e a tabela habilitados para FILESTREAM criados em [Criar um banco de dados habilitado para FILESTREAM](create-a-filestream-enabled-database.md) e [Criar uma tabela para armazenar dados de FILESTREAM](create-a-table-for-storing-filestream-data.md).  
  
##  <a name="ins"></a> Inserindo uma linha contendo dados de FILESTREAM  
 Para adicionar uma linha a uma tabela que suporte dados de FILESTREAM, use a instrução INSERT de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Ao inserir dados em uma coluna FILESTREAM, você pode inserir NULL ou um valor `varbinary(max)`.  
  
### <a name="inserting-null"></a>Inserindo NULL  
 O exemplo a seguir mostra como inserir `NULL`. Quando o valor de FILESTREAM for `NULL`, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não criará um arquivo no sistema de arquivos.  
  
 [!code-sql[FILESTREAM#FS_InsertNULL](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_insertnull)]  
  
### <a name="inserting-a-zero-length-record"></a>Inserindo um registro de comprimento zero  
 O exemplo a seguir mostra como usar `INSERT` para criar um registro com comprimento zero, o que é útil quando você quer obter um identificador de arquivo, mas manipulará o arquivo usando APIs de Win32.  
  
 [!code-sql[FILESTREAM#FS_InsertZero](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_insertzero)]  
  
### <a name="creating-a-data-file"></a>Criando um arquivo de dados  
 O exemplo a seguir mostra como usar o objeto `INSERT` para criar um arquivo que contenha dados. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] converte a cadeia de caracteres `Seismic Data` para um valor `varbinary(max)` . O FILESTREAM criará o arquivo Windows se ele ainda não existir. Depois, os dados serão adicionados ao arquivo de dados.  
  
 [!code-sql[FILESTREAM#FS_InsertData](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_insertdata)]  
  
 Quando você seleciona todos os dados do `Archive`.`dbo.Records` Quando você seleciona todos os dados da tabela, os resultados são semelhantes aos exibidos na tabela a seguir. Porém, a coluna `Id` conterá GUIDs diferente.  
  
|ID|SerialNumber|Retomar|  
|--------|------------------|------------|  
|`C871B90F-D25E-47B3-A560-7CC0CA405DAC`|`1`|`NULL`|  
|`F8F5C314-0559-4927-8FA9-1535EE0BDF50`|`2`|`0x`|  
|`7F680840-B7A4-45D4-8CD5-527C44D35B3F`|`3`|`0x536569736D69632044617461`|  
  
##  <a name="upd"></a> Atualizando dados de FILESTREAM  
 Você pode usar o [!INCLUDE[tsql](../../includes/tsql-md.md)] para atualizar os dados no arquivo do sistema de arquivos; não é recomendável fazer isso quando houver grandes quantidades de fluxo de dados em um arquivo.  
  
 O exemplo a seguir substitui qualquer texto no registro do arquivo pelo texto `Xray 1`.  
  
 [!code-sql[FILESTREAM#FS_UpdateData](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_updatedata)]  
  
##  <a name="del"></a> Excluindo dados de FILESTREAM  
 Ao excluir uma linha que contém um campo de FILESTREAM, você também exclui seus arquivos subjacentes do sistema de arquivos. O único modo de excluir uma linha, e portanto o arquivo, é usar a instrução DELETE do [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
 O exemplo a seguir mostra como excluir uma linha e seus arquivos associados do sistema de arquivos.  
  
 [!code-sql[FILESTREAM#FS_DeleteData](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_deletedata)]  
  
 Quando você selecionar todos os dados da tabela `dbo.Archive` , a linha será excluída. Não é mais possível usar o arquivo associado.  
  
> [!NOTE]  
>  Os arquivos subjacentes são removidos pelo coletor de lixo do FILESTREAM.  
  
## <a name="see-also"></a>Consulte também  
 [Habilitar e configurar FILESTREAM](enable-and-configure-filestream.md)   
 [Evitar conflitos com operações de banco de dados em aplicativos de FILESTREAM](avoid-conflicts-with-database-operations-in-filestream-applications.md)  
  
  
