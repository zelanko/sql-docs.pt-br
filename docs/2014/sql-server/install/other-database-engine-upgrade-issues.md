---
title: Outros problemas de atualização de mecanismo de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], upgrading
ms.assetid: 78a1d8e8-fa97-476f-8777-84617d145340
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f247f9addde6baa949f3260d7a9d9f86ce0c5bff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093695"
---
# <a name="other-database-engine-upgrade-issues"></a>Outros problemas de atualização do Mecanismo de Banco de Dados
  Os problemas de atualização a seguir não podem ser detectados pela versão atual do Supervisor de Atualização. Revise os problemas listados abaixo para avaliar o impacto deles em seus sistemas.  
  
## <a name="multiple-database-engine-deprecated-features"></a>Vários recursos do Mecanismo de Banco de Dados removidos  
 As seguintes opções e instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] são removidas:  
  
-   Opções NO_LOG e TRUNCATE_ONLY do BACKUP LOG  
  
-   BACKUP TRANSACTION  
  
-   RESTORE TRANSACTION  
  
-   DUMP  
  
-   LOAD  
  
-   DBCC CONCURRENCYVIOLATION  
  
-   sp_addalias  
  
-   sp_addgroup  
  
-   sp_changegroup  
  
-   sp_dropgroup  
  
-   sp_helpgroup  
  
-   syssegments  
  
 O uso do protocolo VIA para conectar-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] é preterido.  
  
## <a name="new-data-types"></a>Novos tipos de dados  
 Os itens indicados a seguir serão tipos de sistema reservados. Renomeie os tipos conflitantes definidos pelo usuário antes ou depois da atualização.  
  
-   Geografia  
  
-   Geometry  
  
-   Datetime2  
  
-   HierarchyID  
  
## <a name="target-table-of-the-output-into-clause-cannot-have-any-defined-triggers"></a>Target Table da cláusula OUTPUT INTO não pode ter gatilhos definidos  
 SAÍDA em uma tabela de destino quando a tabela possui gatilhos habilitados não é suportado.  
  
## <a name="compile-time-error-for-udfs-when-the-target-of-an-output-into-clause-is-a-table"></a>Erro de tempo de compilação para UDFs quando o destino de uma cláusula OUTPUT INTO é uma tabela  
 As UDFs (funções definidas pelo usuário) não podem ser usadas para executar ações que modificam o estado do banco de dados. Por exemplo, uma UDF não pode realizar ações DDL (CREATE/ALTER/DROP) ou DML (INSERT/UPDATE/DELETE) em nenhum objeto, exceto em variáveis de tabelas.  
  
## <a name="merge-is-a-reserved-keyword"></a>MERGE é uma palavra-chave reservada  
 MERGE agora é uma palavra-chave completamente reservada. Os aplicativos não podem mais ter objetos (tabelas, colunas, etc.) chamados MERGE.  
  
## <a name="rename-cdc-schema"></a>Renomear esquema CDC  
 Há um nome de esquema chamado CDC. Esse nome de esquema não pode ser usado se **Change Data Capture** está habilitada para o banco de dados.  
  
 Você deve descartar o esquema CDC antes de habilitar **Change Data Capture** para o banco de dados. Isso pode ser feito antes ou depois da atualização. Para descartar o esquema, faça o seguinte:  
  
1.  Transfira os objetos de esquema CDC para um novo nome de esquema usando ALTER SCHEMA.  
  
2.  Verifique as permissões para os objetos no novo esquema.  
  
3.  Faça as modificações necessárias no aplicativo.  
  
4.  Descarte o esquema CDC usando DROP SCHEMA.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)  
  
  
