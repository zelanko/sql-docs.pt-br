---
title: sp_xml_removedocument (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_xml_removedocument_TSQL
- sp_xml_removedocument
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xml_removedocument
ms.assetid: f9dca50a-8baf-4170-90bc-e72783ce5b73
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6219f18bee08d5c20431cb87a2cb30795c515d7a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950479"
---
# <a name="spxmlremovedocument-transact-sql"></a>sp_xml_removedocument (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Remove a representação interna do documento XML especificada pelo identificador de documento e invalida este último.  
  
> [!NOTE]  
>  Um documento analisado é armazenado no cache interno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O analisador MSXML (Msxmlsql.dll) usa um oitavo da memória total disponível para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para evitar a falta de memória, execute **sp_xml_removedocument** para liberar a memória.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_xml_removedocument hdoc  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdoc*  
 É o identificador do documento recém-criado. Um identificador que não é válido retorna um erro. *hdoc* é um inteiro.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou > 0 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove a representação interna de um documento XML. O identificador do documento é fornecido como entrada.  
  
```  
EXEC sp_xml_removedocument @hdoc;  
```  
  
## <a name="see-also"></a>Consulte também      
 <br>[(Transact-SQL) de procedimentos armazenados do sistema](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
 <br>[XML procedimentos armazenados (Transact-SQL)](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)
 <br>[sys.dm_exec_xml_handles (Transact-SQL)](../system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)
 <br>[sp_xml_preparedocument(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)
 <br>[OPENXML (Transact-SQL)](../../t-sql/functions/openxml-transact-sql.md)
  
  
