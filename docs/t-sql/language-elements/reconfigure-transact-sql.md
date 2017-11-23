---
title: RECONFIGURE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/20/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RECONFIGURE
- RECONFIGURE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- reconfiguring configuration options
- configuration options [SQL Server], reconfiguring
- updating configuration options
- RECONFIGURE, RECONFIGURE statement
- RECONFIGURE
- RECONFIGURE, WITH OVERRIDE statement
ms.assetid: 2e6e4eeb-b70b-4f45-a253-28ac4e595d75
caps.latest.revision: "50"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 363a7f12b0be75dd73a2a72402c82be4ba403ed6
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="reconfigure-transact-sql"></a>RECONFIGURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Atualiza o valor configurado atualmente (a **config_value** coluna o **sp_configure** conjunto de resultados) de uma opção de configuração alterada com o **sp_configure** sistema procedimento armazenado. Como algumas opções de configuração requerem uma parada do servidor e reinicialização para atualizar o valor atualmente em execução, RECONFIGURE nem sempre atualiza o valor atualmente em execução (a **run_value** coluna o **sp_configure**  conjunto de resultados) para um valor de configuração alterado.    
    
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>Sintaxe    
    
```    
    
RECONFIGURE [ WITH OVERRIDE ]    
```    
    
## <a name="arguments"></a>Argumentos    
 RECONFIGURE    
 Especifica que se a definição da configuração não requerer uma parada e um reinício do servidor, o valor atualmente em execução deverá ser atualizado. RECONFIGURE também verifica se os novos valores de configuração para qualquer um dos valores que não são válidos (por exemplo, um valor de ordem de classificação que não existe no **syscharsets**) ou os valores recomendados. Com as opções de configuração que não requeiram uma parada e um reinício do servidor, o valor atualmente em execução e os valores atualmente configurados para a opção de configuração devem ser o mesmo valor depois que RECONFIGURE for especificado.    
    
 WITH OVERRIDE    
 Desabilita o configuração verificação do valor (para valores que não são válidos ou não recomendados) para o **intervalo de recuperação** opção de configuração avançada.    
    
 Quase qualquer opção de configuração pode ser reconfigurada usando a opção WITH OVERRIDE, no entanto, alguns fatais erros ainda são impedidos. Por exemplo, o **memória mínima do servidor** opção de configuração não pode ser configurada com um valor maior que o valor especificado no **memória máxima do servidor** opção de configuração.
      
## <a name="remarks"></a>Comentários    
 **sp_configure** não aceita novos valores de opção de configuração fora dos intervalos válidos documentados para cada opção de configuração.    
    
 RECONFIGURE não é permitido em uma transação explícita ou implícita. Ao reconfigurar várias opções ao mesmo tempo, se alguma das operações de reconfiguração falhar, nenhuma delas entrará em vigor.    
    
 Ao reconfigurar o administrador de recursos, consulte a opção de RECONFIGURAÇÃO de [ALTER RESOURCE GOVERNOR &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-resource-governor-transact-sql.md).    
    
## <a name="permissions"></a>Permissões    
 O padrão das permissões de RECONFIGURE é concedida aos possuidores da permissão ALTER SETTINGS. O **sysadmin** e **serveradmin** funções de servidor fixas contêm esta permissão implicitamente.    
    
## <a name="examples"></a>Exemplos    
 O exemplo a seguir define o limite superior para a opção de configuração `recovery interval` como `75` minutos e usa `RECONFIGURE WITH OVERRIDE` para instalá-la. Por padrão, os intervalos de recuperação maiores que 60 minutos não são recomendados e nem permitidos. Entretanto, como a opção `WITH OVERRIDE` está especificada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não verifica se o valor especificado (`90`) é válido para a opção de configuração `recovery interval`.    
    
```    
EXEC sp_configure 'recovery interval', 75'    
RECONFIGURE WITH OVERRIDE;    
GO    
```    
    
## <a name="see-also"></a>Consulte também    
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)     
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)    
    
  
