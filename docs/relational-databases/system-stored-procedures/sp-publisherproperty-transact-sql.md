---
title: sp_publisherproperty (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_publisherproperty
- sp_publisherproperty_TSQL
helpviewer_keywords:
- sp_publisherproperty
ms.assetid: 0ed1ebc1-a1bd-4aed-9f46-615c5cf07827
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5c4ba291619ae756fa9803606eda4427a155ae39
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67896488"
---
# <a name="sppublisherproperty-transact-sql"></a>sp_publisherproperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe ou altera as propriedades do publicador para não - [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores. Esse procedimento armazenado é executado no Distribuidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_publisherproperty [ @publisher = ] 'publisher'   
   [ , [ @propertyname = ] 'propertyname' ]   
   [ , [ @propertyvalue = ] 'propertyvalue' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publisher** = ] **'***publisher***'**  
 É o nome do Publicador heterogêneo. *Publisher* está **sysname**, sem padrão.  
  
 [ **@propertyname** =] **'***propertyname***'**  
 É o nome da propriedade que está sendo definida. *PropertyName* está **sysname**, e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**xactsetbatching**|Se forem agrupadas transações no Publicador em conjuntos transacionalmente consistentes para processamento subsequente, conhecidos como Xactsets. Um valor de **habilitado** significa que Xactsets podem ser criados, que é o padrão. Um valor de **desabilitada** significa que Xactsets existentes são processados por nenhum novo Xactsets é criadas.|  
|**xactsetjob**|Se o trabalho Xactset estiver habilitado para a criação de Xactsets. Um valor de **habilitado** significa que o trabalho de Xactset é executado periodicamente para criar Xactsets no publicador. Um valor de **desabilitada** significa que os Xactsets só são criados pelo Log Reader Agent quando ele pesquisa alterações no publicador.|  
|**xactsetjobinterval**|Intervalo entre execuções do trabalho de Xactset, em minutos.|  
  
 Quando *propertyname* for omitido todas as propriedades configuráveis são retornadas.  
  
 [ **@propertyvalue** =] **'***propertyvalue***'**  
 É o novo valor da configuração da propriedade. *PropertyValue* está **sysname**, com um valor padrão de NULL. Quando *propertyvalue* for omitido, a configuração atual para a propriedade é retornada.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**propertyname**|**sysname**|Retorna as propriedades de publicação seguintes que podem ser definidas:<br /><br /> **xactsetbatching**<br /><br /> **xactsetjob**<br /><br /> **xactsetjobinterval**|  
|**PropertyValue**|**sysname**|É a configuração atual da propriedade na **propertyname** coluna.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_publisherproperty** é usado em replicação transacional para não - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores.  
  
 Quando apenas *publicador* for especificado, o conjunto de resultados inclui as configurações atuais para todas as propriedades que podem ser definidas.  
  
 Quando *propertyname* for especificado, somente a propriedade nomeada aparece no conjunto de resultados.  
  
 Quando todos os parâmetros são especificados, a propriedade é alterada e um conjunto de resultados não é retornado.  
  
 Ao alterar o **xactsetjobinterval** propriedade para um trabalho em execução, você deve reiniciar o trabalho para o novo intervalo entre em vigor.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa no distribuidor pode executar **sp_publisherproperty**.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar o trabalho do conjunto de transações para um Publicador Oracle &#40;programação Transact-SQL de replicação&#41;](../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
