---
title: SET FIPS_FLAGGER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FIPS_FLAGGER
- SET_FIPS_FLAGGER_TSQL
- FIPS_FLAGGER_TSQL
- SET FIPS_FLAGGER
dev_langs:
- TSQL
helpviewer_keywords:
- SET FIPS_FLAGGER statement
- FIPS 127-2 standard
- FIPS_FLAGGER option
ms.assetid: e82f6bee-6cf6-4061-be22-9ad2e8e9d3d6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ece506e0c34f14d827e4562b8c2fcece5de1290d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="set-fipsflagger-transact-sql"></a>SET FIPS_FLAGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Especifica a verificação de conformidade com o padrão FIPS 127-2. Baseia-se no padrão ISO. Para obter informações sobre a conformidade com FIPS do SQL Server, consulte [como usar o SQL Server 2016 no modo FIPS 140-2-compatível com](https://support.microsoft.com/help/4014354/how-to-use-sql-server-2016-in-fips-140-2-compliant-mode). 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SET FIPS_FLAGGER ( 'level' |  OFF )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *nível* **'**  
 É o nível de conformidade em relação ao padrão FIPS 127-2, segundo o qual todas as operações de banco de dados são verificadas. Se uma operação de banco de dados está em conflito com o nível de padrões ISO escolhido, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera um aviso.  
  
 *nível de* deve ser um dos valores a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|ENTRY|Verificação dos padrões com relação à conformidade do nível de entrada do ISO.|  
|FULL|Verificação dos padrões com relação à conformidade total com o ISO.|  
|INTERMEDIATE|Verificação dos padrões com relação à conformidade do nível intermediário do ISO.|  
|OFF|Nenhum padrão é verificado.|  
  
## <a name="remarks"></a>Comentários  
 A configuração de `SET FIPS_FLAGGER` está definida no momento da análise e não em execução ou tempo de execução. Configuração no momento da análise significa que se a instrução SET estiver presente no lote ou procedimento armazenado, ele entra em vigor, independentemente se a execução de código realmente atinge esse ponto; e o `SET` declaração entra em vigor antes de qualquer instrução ser executada. Por exemplo, mesmo se o `SET` instrução está em um `IF...ELSE` bloco de instrução que nunca é alcançado durante a execução, o `SET` instrução ainda entrará em vigor porque o `IF...ELSE` bloco de instrução é analisado.  
  
 Se `SET FIPS_FLAGGER` é definido em um procedimento armazenado, o valor de `SET FIPS_FLAGGER` é restaurado depois que o controle é retornado pelo procedimento armazenado. Portanto, um `SET FIPS_FLAGGER` instrução especificada em SQL dinâmico não tem nenhum efeito em qualquer instrução após a instrução SQL dinâmica.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="see-also"></a>Consulte também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
