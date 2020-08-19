---
description: DBCC CHECKCATALOG (Transact-SQL)
title: DBCC CHECKCATALOG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC_CHECKCATALOG_TSQL
- DBCC CHECKCATALOG
- CHECKCATALOG_TSQL
- CHECKCATALOG
dev_langs:
- TSQL
helpviewer_keywords:
- catalogs [SQL Server], consistency checks
- checking catalog consistency
- DBCC CHECKCATALOG statement
- integrity [SQL Server], catalogs
- consistency [SQL Server], catalogs
ms.assetid: 8076eb4e-f049-44bf-9a35-45cdd6ef0105
author: pmasl
ms.author: umajay
ms.openlocfilehash: 345b555a5cb69adec2c506fb6b40eafbaf3ee62d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459913"
---
# <a name="dbcc-checkcatalog-transact-sql"></a>DBCC CHECKCATALOG (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Verifica a consistência do catálogo dentro do banco de dados especificado. O banco de dados deve estar online.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DBCC CHECKCATALOG   
[   
    (   
    database_name | database_id | 0  
    )  
]  
    [ WITH NO_INFOMSGS ]   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *database_name* | *database_id* | 0  
 É o nome ou ID do banco de dados para o qual verificar consistência do catálogo. Se não for especificado ou se 0 for especificado, o banco de dados atual será usado. Os nomes de banco de dados precisam estar em conformidade com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 WITH NO_INFOMSGS  
 Suprime todas as mensagens informativas.  
  
## <a name="remarks"></a>Comentários  
Depois que o comando DBCC CATALOG termina, uma mensagem é gravada no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o comando DBCC for executado com êxito, a mensagem indicará uma conclusão bem-sucedida e o tempo de execução do comando. Se o comando DBCC parar antes de concluir a verificação devido a um erro, a mensagem indicará que o comando foi finalizado, um valor de estado e a duração da execução do comando. A tabela a seguir lista e descreve os valores de estado que podem ser incluídos na mensagem.
  
|Estado|Descrição|  
|-----------|-----------------|  
|0|O número do erro 8930 foi gerado. Isso indica um dano de metadados que provocou a finalização do comando DBCC.|  
|1|O erro número 8967 foi gerado. Ocorreu um erro interno de DBCC.|  
|2|Ocorreu uma falha durante o reparo do banco de dados em modo de emergência.|  
|3|Isso indica um dano de metadados que provocou a finalização do comando DBCC.|  
|4|Uma declaração ou violação de acesso foi detectada.|  
|5|Ocorreu um erro desconhecido que finalizou o comando DBCC.|  
  
DBCC CHECKCATALOG executa vários testes de consistência entre tabelas de metadados do sistema. DBCC CHECKCATALOG usa um instantâneo do banco de dados interno para fornecer a consistência transacional necessária ao executar essas verificações. Para obter mais informações, confira [Exibir o tamanho do arquivo esparso de um instantâneo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md) e a seção "Uso de instantâneo de banco de dados interno do DBCC" em [DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md).
Se um instantâneo não puder ser criado, DBCC CHECKCATALOG obterá um bloqueio de banco de dados exclusivo para adquirir a consistência exigida. Se qualquer inconsistência for detectada, não poderá ser reparada e o banco de dados deverá ser restaurado a partir de um backup.
  
> [!NOTE]  
> A execução de DBCC CHECKCATALOG no **tempdb** não realiza nenhuma verificação. Isso ocorre porque, por motivos de desempenho, os instantâneos do banco de dados não estão disponíveis no **tempdb**. Isso significa que não é possível obter a consistência transacional exigida. Recicle o servidor para resolver problemas de metadados do **tempdb**.  
  
> [!NOTE]  
> DBCC CHECKCATALOG não verifica dados FILESTREAM. FILESTREAM armazena BLOBS (objetos binários grandes) no sistema de arquivos.  
  
DBCC CHECKCATALOG também é executado como parte do [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md).
  
## <a name="result-sets"></a>Conjuntos de resultados  
Se nenhum banco de dados for especificado, DBCC CHECKCATALOG retornará:
  
```
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
Se [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] for especificado como nome do banco de dados, DBCC CHECKCATALOG retornará:
  
```
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de servidor fixa **sysadmin** ou à função de banco de dados fixa **db_owner**.  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir verifica a integridade do catálogo no banco de dados atual e no banco de dados `AdventureWorks`.
  
```sql
-- Check the current database.  
DBCC CHECKCATALOG;  
GO  
-- Check the AdventureWorks2012 database.  
DBCC CHECKCATALOG (AdventureWorks2012);  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)
  
