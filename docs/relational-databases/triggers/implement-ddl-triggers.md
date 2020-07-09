---
title: Implementar gatilhos DDL | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- DDL triggers, implementing
ms.assetid: f44e5340-1d18-40e9-828e-0ffcca091ae3
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8466ffbe1327647f01a6da275cba843b0502a6bd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750111"
---
# <a name="implement-ddl-triggers"></a>Implementar gatilhos DDL
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Este tópico fornece informações para ajudá-lo a criar gatilhos DDL, modificar gatilhos DDL e desabilitar ou cancelar gatilhos DDL.  
  
## <a name="creating-ddl-triggers"></a>Criando gatilhos DDL  
 Os gatilhos DDL são criados usando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TRIGGER para gatilhos DDL.  
  
 **Para criar um gatilho DDL**  
  
-   [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
> [!IMPORTANT]  
>  A habilidade de retornar conjuntos de resultados de gatilhos será removida em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os gatilhos que retornam conjuntos de resultados podem causar um comportamento inesperado em aplicativos que não são projetados para trabalhar com eles. Evite retornar conjuntos de resultados de gatilhos em novos trabalhos de desenvolvimento e planeje a modificação de aplicativos que atualmente fazem isso. Para impedir que os gatilhos retornem conjuntos de resultados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], defina a [Opção disallow results from triggers](../../database-engine/configure-windows/disallow-results-from-triggers-server-configuration-option.md) como 1. A configuração padrão dessa opção será 1 em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="modifying-ddl-triggers"></a>Modificando gatilhos DDL  
 Para modificar a definição de um gatilho DDL, você pode cancelar e recriar o gatilho ou redefinir o gatilho existente em uma única etapa.  
  
 Se você alterar o nome de um objeto referenciado por um gatilho DDL, modifique o gatilho para que seu texto reflita o novo nome. Portanto, antes de renomear um objeto, exiba primeiramente as dependências do objeto para determinar se algum gatilho foi afetado pela mudança proposta.  
  
 Um gatilho também pode ser modificado para codificar sua definição.  
  
 **Para modificar um gatilho**  
  
-   [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
 **Para exibir as dependências de um gatilho**  
  
-   [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
-   [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)  
  
-   [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)  
  
## <a name="disabling-and-dropping-ddl-triggers"></a>Desabilitando e cancelando gatilhos DDL  
 Quando um gatilho DDL não é mais necessário, pode ser desabilitado ou excluído.  
  
 Ao desabilitar um gatilho DDL, você não o cancela. O gatilho ainda existe como um objeto no banco de dados atual. Porém, o gatilho não será acionado quando qualquer instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] , em que ele tenha sido programado, for executada. Os gatilhos DDL desabilitados podem ser habilitados novamente. A habilitação de um gatilho DDL faz com que ele seja acionado da mesma maneira que era ao ser criado originalmente. Quando os gatilhos DDL são criados, eles são habilitados por padrão.  
  
 Quando um gatilho DDL é excluído, ele é cancelado do banco de dados atual. Quaisquer objetos ou dados que servem de escopo para o gatilho DDL não são afetados.  
  
 **Para desabilitar um gatilho DDL**  
  
-   [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)  
  
-   [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
 **Para habilitar um gatilho DDL**  
  
-   [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)  
  
-   [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
 **Para excluir um gatilho DDL**  
  
-   [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)  
  
  
