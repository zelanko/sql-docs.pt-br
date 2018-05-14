---
title: Cmdlet New-RestoreFolder | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f5fded902a54a37cd91f4f283aa84252b6ae007a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="new-restorefolder-cmdlet"></a>Cmdlet New-RestoreFolder
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Restaura uma pasta original em uma nova pasta.  

>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
## <a name="syntax"></a>Sintaxe  
 `New-RestoreFolder [-OriginalFolder] <String> [-NewFolder] <String> [-AsTemplate] [-Server <String>] [-Credential <PSCredential>] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]`  
  
 `New-RestoreFolder [-Server <String>] [-Credential <PSCredential>] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]`  
  
 Parâmetros comuns, como –Verbose, –Debug, erro e parâmetros de aviso, –Whatif e –Confirm são documentados na referência do Windows PowerShell. Para obter mais informações, consulte [about_CommonParameters](http://technet.microsoft.com/library/dd315352.aspx).  
  
## <a name="description"></a>Description  
 O cmdlet New-RestoreFolder é usado para criar uma nova pasta com base no nome da pasta original.  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="-originalfolder-string"></a>-OriginalFolder \<cadeia de caracteres >  
 Obtém o local da pasta original.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|true|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-newfolder-string"></a>-NewFolder \<cadeia de caracteres >  
 Define o local de uma nova pasta.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|1|  
|Valor padrão||  
|Aceitar entrada de pipeline?|true|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-astemplate-switchparameter"></a>-AsTemplate \<SwitchParameter >  
 Especifica se o objeto deve ser criado em memória e retornado.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-server-string"></a>-Servidor \<cadeia de caracteres >  
 Especifica a instância do Analysis Services que o cmdlet conectará e executará. Se nenhum nome de servidor for fornecido, uma conexão será feita com o localhost. Para instâncias padrão, especifique apenas o nome do servidor. Para instâncias nomeadas, use o formato nome_do_servidor\nome_da_instância. Para conexões HTTP, use o formato http[s]://servidor[:porta]/diretório_virtual/msmdpump.dll.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão|localhost|  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-credential-pscredential"></a>-Credential \<PSCredential >  
 Este parâmetro é usado para passar um nome de usuário e senha ao usar uma conexão HTTP para uma instância do Analysis Services, para uma instância que você configurou para acesso HTTP. Para obter mais informações, consulte [configurar o acesso HTTP ao Analysis Services nos serviços de informações da Internet &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md) para conexões HTTP.  
  
 Se este parâmetro for especificado, o nome de usuário e a senha serão usados para conectar à instância do Analysis Server especificado. Se nenhuma credencial for especificada, será usada a conta do Windows padrão do usuário que está executando a ferramenta.  
  
 Para usar este parâmetro, primeiro crie um objeto PSCredential usando Get-Credential para especificar o nome de usuário e a senha (por exemplo, `$Cred=Get-Credential “adventure-works\bobh”`. Você pode redirecionar este objeto para o parâmetro –Credential `(-Credential:$Cred`).  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|True (ByValue)|  
|Aceitar caracteres curinga?|false|  
  
## <a name="inputs-and-outputs"></a>Entradas e saídas  
 O tipo de entrada é o tipo dos objetos que você pode transportar para o cmdlet. O tipo de retorno é o tipo dos objetos que o cmdlet retorna.  
  
|||  
|-|-|  
|Entradas||  
|Saídas|Nenhuma|  
  
