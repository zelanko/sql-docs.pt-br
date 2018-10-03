---
title: XP_LOGINCONFIG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_loginconfig_TSQL
- xp_loginconfig
dev_langs:
- TSQL
helpviewer_keywords:
- xp_loginconfig
ms.assetid: d380e799-2857-408a-bcbf-5e73a8e6aa5a
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8590a33f870dc14ac34118ce5e655acc6e67f257
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47658724"
---
# <a name="xploginconfig-transact-sql"></a>xp_loginconfig (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Relata a configuração de segurança de logon de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
xp_loginconfig ['config_name']  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *config_name* **'**  
 É o valor de configuração a ser exibido. Se *config_name* não é especificado, todos os valores de configuração são relatados. *config_name* está **sysname**, com um padrão de NULL, e pode ser um destes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**modo de logon**|Modo de segurança de logon. Os valores possíveis são **Mixed** e **autenticação do Windows**.<br /><br /> Substituído por:<br /><br /> `SELECT SERVERPROPERTY('IsIntegratedSecurityOnly'); GO`|  
|**logon padrão**|Nome da ID de logon padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usuários autorizados de conexões confiáveis (para usuários sem um nome de logon correspondente). O logon padrão é **convidado**. Esse valor é fornecido para a compatibilidade com versões anteriores.|  
|**Domínio padrão**|Nome do domínio padrão do Windows para usuários de rede de conexões confiáveis. O domínio padrão é o domínio do computador que executa o Windows e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse valor é fornecido para a compatibilidade com versões anteriores.|  
|**nível de auditoria**|Nível de auditoria. Os valores possíveis são **none**, **sucesso**, **falha**, e **todos os**. As auditorias são gravadas no log de erros e no recurso Visualizador de Eventos do Windows.|  
|**nome do host do conjunto**|Indica se o nome do host do registro de logon do cliente é substituído pelo nome de usuário de rede do Windows. Os valores possíveis são **verdadeira** ou **falso**. Se isso estiver definido, o nome de usuário de rede aparecerá na saída de **sp_who**.|  
|**mapa _**|Relata quais caracteres especiais do Windows são mapeados para o caractere de sublinhado (_) válido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os valores possíveis são **separador de domínio** (padrão), **espaço**, **nulo**, ou qualquer caractere único. Esse valor é fornecido para a compatibilidade com versões anteriores.|  
|**mapear $**|Relata quais caracteres especiais do Windows são mapeados para o caractere de cifrão ($) válido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os valores possíveis são **separador de domínio**, **espaço**, **nulo**, ou qualquer caractere único. O padrão é **espaço**. Esse valor é fornecido para a compatibilidade com versões anteriores.|  
|**n º do mapa**|Relata quais caracteres especiais do Windows são mapeados para o caractere de sinal numérico (#) válido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os valores possíveis são **separador de domínio**, **espaço**, **nulo**, ou qualquer caractere único. Hífen é o padrão. Esse valor é fornecido para a compatibilidade com versões anteriores.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Valor de configuração|  
|**valor de configuração**|**sysname**|Definição de valor de configuração|  
  
## <a name="remarks"></a>Comentários  
 **XP_LOGINCONFIG** não pode ser usado para definir valores de configuração.  
  
 Para definir o modo de logon e o nível de auditoria, use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL sobre o **mestre** banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-how-to-report-all-configuration-values"></a>A. Como relatar todos os valores de configuração  
 O exemplo a seguir mostra todas as configurações atualmente definidas.  
  
```  
EXEC xp_loginconfig;  
GO  
```  
  
### <a name="b-how-to-report-a-specific-configuration-value"></a>B. Como relatar um valor de configuração específico  
 O exemplo a seguir mostra a configuração somente para o modo de logon.  
  
```  
EXEC xp_loginconfig 'login mode';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_denylogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [xp_logininfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
