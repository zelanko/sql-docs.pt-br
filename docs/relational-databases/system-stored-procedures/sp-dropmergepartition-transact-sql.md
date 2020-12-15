---
description: sp_dropmergepartition (Transact-SQL)
title: sp_dropmergepartition (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergepartition_TSQL
- sp_dropmergepartition
helpviewer_keywords:
- sp_dropmergepartition
ms.assetid: 1be511c1-79ff-4947-9379-78d83b7b8945
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 850130a686a114d2e7a8bafaea8b0133d40215cd
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472727"
---
# <a name="sp_dropmergepartition-transact-sql"></a>sp_dropmergepartition (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Remove uma partição para um filtro de linha com parâmetros de uma publicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador. Esse procedimento armazenado também remove o trabalho de instantâneo correspondente e arquivos de instantâneo para a partição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropmergepartition [ @publication = ] 'publication'  
        , [ @suser_sname = ] 'suser_sname'  
        , [ @host_name = ] 'host_name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication] = 'publication'` É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @suser_sname = ] 'suser_sname'` É o valor da função [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) no Assinante usado para definir a partição. *SUSER_SNAME* é **sysname**, sem padrão.  
  
`[ @host_name = ] 'host_name'` É o valor da função [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) no Assinante usado para definir a partição. *HOST_NAME* é **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_dropmergepartition** é usado na replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_dropmergepartition**.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar partições para uma publicação de mesclagem com filtros parametrizados](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)  
  
  
