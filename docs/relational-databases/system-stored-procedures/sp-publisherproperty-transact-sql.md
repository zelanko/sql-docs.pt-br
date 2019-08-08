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
ms.openlocfilehash: 185ad0ad33419b20fffae9bff3e5562761ea7b31
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771169"
---
# <a name="sp_publisherproperty-transact-sql"></a>sp_publisherproperty (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Exibe ou altera as propriedades do Publicador [!INCLUDE[msCoName](../../includes/msconame-md.md)] para não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores. Esse procedimento armazenado é executado no Distribuidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_publisherproperty [ @publisher = ] 'publisher'   
   [ , [ @propertyname = ] 'propertyname' ]   
   [ , [ @propertyvalue = ] 'propertyvalue' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publisher** = ] **'***publisher***'**  
 É o nome do Publicador heterogêneo. o Publicador é **sysname**, sem padrão.  
  
 [ **@propertyname** =] **'***PropertyName***'**  
 É o nome da propriedade que está sendo definida. *PropertyName* é **sysname**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**xactsetbatching**|Se forem agrupadas transações no Publicador em conjuntos transacionalmente consistentes para processamento subsequente, conhecidos como Xactsets. Um valor **habilitado** significa que Xactsets pode ser criado, que é o padrão. Um valor **desabilitado** significa que os Xactsets existentes são processados por nenhum novo Xactsets é criado.|  
|**xactsetjob**|Se o trabalho Xactset estiver habilitado para a criação de Xactsets. Um valor **habilitado** significa que o trabalho Xactset é executado periodicamente para criar Xactsets no Publicador. Um valor **desabilitado** significa que o Xactsets só será criado pelo agente de leitor de log quando ele sondar o Publicador em busca de alterações.|  
|**xactsetjobinterval**|Intervalo entre execuções do trabalho de Xactset, em minutos.|  
  
 Quando *PropertyName* é omitido, todas as propriedades configurável são retornadas.  
  
 [ **@propertyvalue** =] **'***PropertyValue***'**  
 É o novo valor da configuração da propriedade. *PropertyValue* é **sysname**, com um valor padrão de NULL. Quando *PropertyValue* é omitido, a configuração atual da propriedade é retornada.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**propertyname**|**sysname**|Retorna as propriedades de publicação seguintes que podem ser definidas:<br /><br /> **xactsetbatching**<br /><br /> **xactsetjob**<br /><br /> **xactsetjobinterval**|  
|**PropertyValue**|**sysname**|É a configuração atual para a propriedade na coluna **PropertyName** .|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_publisherproperty** é usado na replicação transacional para não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores.  
  
 Quando apenas o Publicador é especificado, o conjunto de resultados inclui as configurações atuais para todas as propriedades que podem ser definidas.  
  
 Quando *PropertyName* é especificado, somente a propriedade nomeada aparece no conjunto de resultados.  
  
 Quando todos os parâmetros são especificados, a propriedade é alterada e um conjunto de resultados não é retornado.  
  
 Ao alterar a propriedade **xactsetjobinterval** para um trabalho em execução, você deve reiniciar o trabalho para que o novo intervalo entre em vigor.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** no distribuidor podem executar **sp_publisherproperty**.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar o trabalho do conjunto de transações para um Publicador Oracle &#40;programação Transact-SQL de replicação&#41;](../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
