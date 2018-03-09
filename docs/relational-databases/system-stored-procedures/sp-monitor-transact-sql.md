---
title: sp_monitor (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_monitor_TSQL
- sp_monitor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_monitor
ms.assetid: cb628496-2f9b-40e4-b018-d0831c4cb018
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8b4ef90280e72a7afd6a8787b053115a4bffa4fa
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="spmonitor-transact-sql"></a>sp_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe estatísticas sobre [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_monitor  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Description|  
|-----------------|-----------------|  
|**last_run**|Tempo **sp_monitor** foi executado pela última vez.|  
|**current_run**|Tempo **sp_monitor** está sendo executado.|  
|**segundos**|Número de segundos decorridos desde **sp_monitor** foi executado.|  
|**cpu_busy**|Segundos durante os quais a CPU do computador servidor está executando o trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**io_busy**|Segundos durante os quais o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executou operações de entrada e saída.|  
|**ocioso**|Segundos durante os quais o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ficou inativo.|  
|**packets_received**|Número de leituras de pacotes de entrada feitas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**packets_sent**|Número de pacotes de saída gravados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**packet_errors**|Número de erros encontrados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao ler e gravar pacotes.|  
|**total_read**|Número de leituras feias pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**total_write**|Número de gravações feias pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**total_errors**|Número de erros encontrados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durante a leitura e gravação.|  
|**conexões**|Número de logons ou tentativas de logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="remarks"></a>Comentários  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controla, através de várias funções, a quantidade de trabalho realizada. Executar **sp_monitor** exibe os valores atuais retornados por essas funções e mostra o quanto eles foram alterados desde a última vez em que o procedimento foi executado.  
  
 Para cada coluna, a estatística é impressa no formato *número*(*número*)-*número*% ou *número*(*número*). A primeira *número* refere-se ao número de segundos (para **cpu_busy**, **io_busy**, e **ocioso**) ou o número total (para os outros variáveis) desde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi reiniciado. O *número* entre parênteses refere-se ao número de segundos ou número total desde a última vez **sp_monitor** foi executado. A porcentagem é a porcentagem de tempo decorrido desde **sp_monitor** foi executado pela última vez. Por exemplo, se o relatório mostra **cpu_busy** como 4250 (215)-68%, a CPU ficou ocupada 4250 segundos desde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi iniciado pela última vez, 215 segundos desde **sp_monitor** foi a última vez e 68% das total de tempo desde **sp_monitor** foi executado pela última vez.  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir relata as informações sobre o quanto o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esteve ocupado.  
  
```  
USE master  
EXEC sp_monitor  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
||||  
|-|-|-|  
|**last_run**|**current_run**|**segundos**|  
|29 de março de 1998 11:55|4 de abril de 1998 14:22|561|  
  
||||  
|-|-|-|  
|**cpu_busy**|**io_busy**|**ocioso**|  
|190(0)-0%|187(0)-0%|148(556)-99%|  
  
||||  
|-|-|-|  
|**packets_received**|**packets_sent**|**packet_errors**|  
|16(1)|20(2)|0(0)|  
  
|||||  
|-|-|-|-|  
|**total_read**|**total_write**|**total_errors**|**conexões**|  
|141(0)|54920(127)|0(0)|4(0)|  
  
## <a name="see-also"></a>Consulte também  
 [SP_WHO &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
