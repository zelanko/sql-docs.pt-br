---
title: COM CHANGE_TRACKING_CONTEXT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- WITH_CHANGE_TRACKING_CONTEXT_TSQL
- WITH CHANGE_TRACKING_CONTEXT
dev_langs:
- TSQL
helpviewer_keywords:
- WITH CHANGE_TRACKING_CONTEXT
- change tracking [SQL Server], WITH CHANGE_TRACKING_CONTEXT
ms.assetid: 885e33a1-602a-4b94-8380-a63ac935a683
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: aa900fcf6bd142c5f3d5eddde85df0a41419efa1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85752822"
---
# <a name="with-change_tracking_context-transact-sql"></a>WITH CHANGE_TRACKING_CONTEXT (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Ativa o contexto de uma alteração a ser especificada, como uma ID de originador, quando os dados são alterados. Por exemplo, ao usar o controle de alterações, um aplicativo pode tentar fazer diferenciações entre as alterações que foram feitas pelo próprio aplicativo e as alterações feitas nos dados fora do aplicativo.  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
WITH CHANGE_TRACKING_CONTEXT ( context )  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *contexto*  
 São as informações contextuais fornecidas pelo aplicativo chamador e armazenadas com as informações de controle de alterações da alteração. o *contexto* é **varbinary (128)**.  
  
 O valor pode ser uma constante ou uma variável, mas não pode ser NULL.  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte define o contexto de controle de alterações de uma alteração de dados.  
  
```  
WITH CHANGE_TRACKING_CONTEXT ( context )  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de Controle de Alterações &#40;&#41;de Transact-SQL](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [&#41;CHANGEtable &#40;Transact-SQL](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [Controle de alterações de dados &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
