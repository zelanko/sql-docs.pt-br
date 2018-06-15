---
title: DROP ASSEMBLY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP ASSEMBLY
- DROP_ASSEMBLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing assemblies
- DROP ASSEMBLY statement
- deleting assemblies
- assemblies [CLR integration], removing
- dropping assemblies
- WITH NO DEPENDENTS option
ms.assetid: 452d181a-a8e6-44a3-975d-29966d01b18d
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 294326cda14b6027f067bd18a2f659dfc8e0e8e0
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
ms.locfileid: "33700659"
---
# <a name="drop-assembly-transact-sql"></a>DROP ASSEMBLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove um assembly e todos os seus arquivos associados do banco de dados atual. Os assemblies são criados usando [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md) e modificados usando [ALTER ASSEMBLY](../../t-sql/statements/alter-assembly-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DROP ASSEMBLY [ IF EXISTS ] assembly_name [ ,...n ]  
[ WITH NO DEPENDENTS ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *IF EXISTS*  
 **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Descarta condicionalmente o assembly somente se ele já existir.  
  
 *assembly_name*  
 É o nome do assembly que você deseja descartar.  
  
 WITH NO DEPENDENTS  
 Se for especificado, descartará somente o *assembly_name* e nenhum dos assemblies dependentes referenciados pelo assembly. Se não for especificado, DROP ASSEMBLY descartará o *assembly_name* e todos os assemblies dependentes.  
  
## <a name="remarks"></a>Remarks  
 O descarte de um assembly remove o mesmo e todos os seus arquivos associados, tais como código fonte e arquivos de depuração, do banco de dados  
  
 Se WITH NO DEPENDENTS não for especificado, DROP ASSEMBLY descartará o *assembly_name* e todos os assemblies dependentes. Se houver falha em uma tentativa de descarte de quaisquer assemblies dependentes, DROP ASSEMBLY retornará um erro.  
  
 DROP ASSEMBLY retornará um erro se o assembly for referenciado por outro assembly que exista no banco de dados ou se for usado por funções CLR (Common Language Runtime), procedimentos armazenados, disparadores, tipos definidos pelo usuário ou agregações no banco de dados atual.  
  
 DROP ASSEMBLY não interfere em nenhum código que faça referência ao assembly que está atualmente em execução. Entretanto, depois que DROP ASSEMBLY for executado, quaisquer tentativas de invocar o código do assembly falharão.  
  
## <a name="permissions"></a>Permissões  
 Requer propriedade do assembly ou permissão CONTROL no mesmo.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir assume que o assembly `HelloWorld` já está criado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
DROP ASSEMBLY Helloworld ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Obtendo informações sobre assemblies](../../relational-databases/clr-integration/assemblies-getting-information.md)  
  
  
