---
description: RECONFIGURE (Transact-SQL)
title: RECONFIGURE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/20/2016
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RECONFIGURE
- RECONFIGURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- reconfiguring configuration options
- configuration options [SQL Server], reconfiguring
- updating configuration options
- RECONFIGURE, RECONFIGURE statement
- RECONFIGURE
- RECONFIGURE, WITH OVERRIDE statement
ms.assetid: 2e6e4eeb-b70b-4f45-a253-28ac4e595d75
author: rothja
ms.author: jroth
ms.openlocfilehash: 26c8d6f53ef87fa2d9e6ab5dcfee6b39be01834f
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "92196783"
---
# <a name="reconfigure-transact-sql"></a>RECONFIGURE (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Atualiza o valor configurado atualmente (a coluna **config_value** no conjunto de resultados **sp_configure**) de uma opção de configuração alterada com o procedimento armazenado do sistema **sp_configure**. Como algumas opções de configuração requerem uma parada e um reinício do servidor para atualizar o valor em execução no momento, RECONFIGURE nem sempre atualiza o valor em execução no momento (a coluna **run_value** do conjunto de resultados **sp_configure**) para um valor de configuração alterado.    
    
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>Sintaxe    
    
```syntaxsql
RECONFIGURE [ WITH OVERRIDE ]    
```    
    
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 RECONFIGURE    
 Especifica que se a definição da configuração não requerer uma parada e um reinício do servidor, o valor atualmente em execução deverá ser atualizado. RECONFIGURE também verifica os novos valores de configuração buscando valores que não são válidos (por exemplo, um valor de ordem de classificação que não exista em **syscharsets**) ou não são recomendados. Com as opções de configuração que não requeiram uma parada e um reinício do servidor, o valor atualmente em execução e os valores atualmente configurados para a opção de configuração devem ser o mesmo valor depois que RECONFIGURE for especificado.    
    
 WITH OVERRIDE    
 Desabilita a verificação de valor de configuração (que busca valores que não são válidos ou não são recomendados) da opção de configuração avançada **recovery interval**.    
    
 Quase todas as opções de configuração podem ser reconfiguradas usando a opção WITH OVERRIDE, no entanto, alguns erros fatais ainda são evitados. Por exemplo, a opção de configuração **min server memory** não pode ser definida com um valor maior que o especificado na opção de configuração **max server memory**.
      
## <a name="remarks"></a>Comentários    
 **sp_configure** não aceita novos valores de opção de configuração fora dos intervalos válidos documentados para cada opção de configuração.    
    
 RECONFIGURE não é permitido em uma transação explícita ou implícita. Ao reconfigurar várias opções ao mesmo tempo, se alguma das operações de reconfiguração falhar, nenhuma delas entrará em vigor.    
    
 Ao reconfigurar o Resource Governor, consulte a opção RECONFIGURE de [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md).    
    
## <a name="permissions"></a>Permissões    
 O padrão das permissões de RECONFIGURE é concedida aos possuidores da permissão ALTER SETTINGS. As funções de servidor fixas **sysadmin** e **serveradmin** contêm esta permissão implicitamente.    
    
## <a name="examples"></a>Exemplos    
 O exemplo a seguir define o limite superior para a opção de configuração `recovery interval` como `75` minutos e usa `RECONFIGURE WITH OVERRIDE` para instalá-la. Por padrão, os intervalos de recuperação maiores que 60 minutos não são recomendados e nem permitidos. Entretanto, como a opção `WITH OVERRIDE` está especificada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não verifica se o valor especificado (`75`) é válido para a opção de configuração `recovery interval`.    
    
```sql    
EXEC sp_configure 'recovery interval', 75    
RECONFIGURE WITH OVERRIDE;    
GO    
```    
    
## <a name="see-also"></a>Consulte Também    
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)     
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)    
    
  
