---
description: SET FIPS_FLAGGER (Transact-SQL)
title: SET FIPS_FLAGGER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: baec8662d21347340eede171bb8dcf3966f54a7f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540581"
---
# <a name="set-fips_flagger-transact-sql"></a>SET FIPS_FLAGGER (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Especifica a verificação de conformidade com o padrão FIPS 127-2. Baseia-se no padrão ISO. Para obter informações sobre a conformidade com FIPS do SQL Server, veja [Como usar o SQL Server 2016 no modo compatível com FIPS 140-2](https://support.microsoft.com/help/4014354/how-to-use-sql-server-2016-in-fips-140-2-compliant-mode). 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
SET FIPS_FLAGGER ( 'level' |  OFF )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 **'** *level* **'**  
 É o nível de conformidade em relação ao padrão FIPS 127-2, segundo o qual todas as operações de banco de dados são verificadas. Se uma operação de banco de dados entrar em conflito com o nível de padrões ISO escolhido, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerará um aviso.  
  
 *level* deve ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|ENTRY|Verificação dos padrões com relação à conformidade do nível de entrada do ISO.|  
|FULL|Verificação dos padrões com relação à conformidade total com o ISO.|  
|INTERMEDIATE|Verificação dos padrões com relação à conformidade do nível intermediário do ISO.|  
|OFF|Nenhum padrão é verificado.|  
  
## <a name="remarks"></a>Comentários  
 A configuração de `SET FIPS_FLAGGER` é definida no tempo da análise, e não no tempo de execução ou operação. A configuração no momento da análise significa que se a instrução SET estiver presente no lote ou no procedimento armazenado, ela terá efeito, independentemente de se a execução do código realmente atinge esse ponto; e a instrução `SET` terá efeito antes de qualquer instrução ser executada. Por exemplo, mesmo que a instrução `SET` esteja em um bloco de instruções `IF...ELSE` que nunca é atingido durante a execução, a instrução `SET` ainda entrará em vigor porque o bloco de instruções `IF...ELSE` é analisado.  
  
 Se `SET FIPS_FLAGGER` for definido em um procedimento armazenado, um valor de `SET FIPS_FLAGGER` será restaurado depois que o controle for retornado do procedimento armazenado. Portanto, uma instrução `SET FIPS_FLAGGER` especificada em SQL dinâmico não causa nenhum efeito em nenhuma instrução depois da instrução SQL dinâmica.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
