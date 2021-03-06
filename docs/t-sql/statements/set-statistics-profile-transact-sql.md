---
description: SET STATISTICS PROFILE (Transact-SQL)
title: SET STATISTICS PROFILE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PROFILE
- SET_STATISTICS_PROFILE_TSQL
- PROFILE_TSQL
- SET STATISTICS PROFILE
dev_langs:
- TSQL
helpviewer_keywords:
- profiles [SQL Server], displaying
- statements [SQL Server], profile information
- SET STATISTICS PROFILE statement
- STATISTICS PROFILE option
- statistical information [SQL Server], profiles
ms.assetid: c635e262-35fa-421a-aa6f-a1c30f351647
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1596dc3d6c191ea823c8382aa93a520e784be115
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541214"
---
# <a name="set-statistics-profile-transact-sql"></a>SET STATISTICS PROFILE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Exibe as informações de perfil de uma instrução. O STATISTICS PROFILE funciona com consultas ad hoc, exibições e procedimentos armazenados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
SET STATISTICS PROFILE { ON | OFF }  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>Comentários
 Quando STATISTICS PROFILE está como ON, cada consulta executada retorna seu conjunto de resultados regulares, seguido de um conjunto de resultados adicionais que exibem um perfil da execução de consulta.  
  
 O conjunto de resultados adicionais contém as colunas de SHOWPLAN_ALL da consulta e as colunas adicionais.  
  
|Nome da coluna|Descrição|  
|-----------------|-----------------|  
|**Linhas**|O número atual de linhas geradas por cada operador.|  
|**Executes**|Número de vezes que o operador foi executado|  
  
## <a name="permissions"></a>Permissões  
 Para usar SET STATISTICS PROFILE e exibir a saída, os usuários devem ter as seguintes permissões:  
  
-   Permissões adequadas para executar as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   A permissão de SHOWPLAN em todos os bancos de dados que são referenciados pelas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Para instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que não geram conjuntos de resultados STATISTICS PROFILE , serão necessárias somente as permissões apropriadas para executar as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que produzem conjuntos de resultados STATISTICS PROFILE, verifica tanto a permissão de execução de instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] e a permissão de SHOWPLAN deve ser bem-sucedida ou a instrução de execução [!INCLUDE[tsql](../../includes/tsql-md.md)] será anulada e nenhuma informação de Showplan será gerada.  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [SET STATISTICS TIME &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-time-transact-sql.md)   
 [SET STATISTICS IO &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-io-transact-sql.md)  
  
  
