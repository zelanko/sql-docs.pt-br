---
title: Constantes grandes são digitadas como tipos de valor grande nos modos de compatibilidade 90 ou posterior | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- binary constants
- CHARINDEX function
- constants
- character string constants
- PATINDEX function
ms.assetid: 6e309fa0-5fb9-45a1-9739-f13fae525bfe
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8c7aded5577e28d94f42e108e46bb8a9c3cd6020
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094086"
---
# <a name="large-constants-are-typed-as-large-value-types-in-90-or-later-compatibility-modes"></a>Constantes grandes são digitadas como tipos de valor grande no modo de compatibilidade 90 ou posterior
  O Supervisor de Atualização detectou a presença de constantes grandes. Constantes de cadeias de caracteres e constantes binárias maiores que 8.000 bytes são tratadas como tipos de dados de objeto grande no [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou em versões posteriores, caracteres grandes, Unicode e constantes binárias são digitadas como tipos do valor grande.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrição  
 Quando funções de cadeia de caracteres, como CHARINDEX e PATINDEX, são usadas com constantes de cadeia de caracteres ou constantes binárias que excedem 8.000 bytes, o [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] retorna o erro 8116, e o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou versões posteriores retorna o erro 8152.  
  
 No [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], as funções de cadeia de caracteres retornam o erro 8116 quando são usadas com tipos de dados `text`, `ntext` e `image`.  
  
 No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou em versões posteriores, as constantes grandes são tratadas como tipos de dados `varchar(max)`, `nvarchar(max)` e `varbinary(max)`, respectivamente. Esses tipos de dados são compatíveis com funções de cadeia de caracteres.  
  
 No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou em versões posteriores, funções de cadeia de caracteres, como CHARINDEX e PATINDEX, assumem a cadeia de caracteres que tem a sequência de caracteres com menos de 8.000 bytes. É pos isso que o erro 8152 é exibido para CHARINDEX e PATINDEX.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
