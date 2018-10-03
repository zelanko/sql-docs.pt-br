---
title: Instalar o Distributed Replay no Prompt de comando | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: ea1171da-f50e-4f16-bedc-5e468a46477f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d7dbc86ff32e0c9ba6e77558a713cda2598221e0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126116"
---
# <a name="install-distributed-replay-from-the-command-prompt"></a>Instalar o Distributed Replay a partir do prompt de comando
  A instalação de uma nova instância do Distributed Replay no prompt de comando permite especificar os recursos a serem instalados e como eles devem ser configurados. A instalação do prompt de comando dá suporte à instalação, reparo, atualização e desinstalação dos componentes do Distributed Replay. Quando a instalação é feita via prompt de comando, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte ao modo silencioso completo usando o parâmetro /Q.  
  
> [!NOTE]  
>  Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.  
  
## <a name="installation-parameters"></a>Parâmetros de instalação  
 A lista de recursos de nível superior inclui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]e Ferramentas. O recurso Ferramentas instalará as Ferramentas de Gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , os Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]e outros componentes compartilhados. Para instalar os componentes do Distributed Replay, especifique os seguintes parâmetros:  
  
|Componente|Parâmetro|  
|---------------|---------------|  
|Distributed Replay Controller|**DREPLAY_CTLR**|  
|Distributed Replay Client|**DREPLAY_CLT**|  
|Ferramenta de administração|**Ferramentas**|  
  
> [!IMPORTANT]  
>  Depois de instalar o Distributed Replay, crie regras de firewall no controlador e nos computadores cliente e conceda permissões a cada computador cliente no servidor de destino. Para obter mais informações, veja [Concluir as etapas de pós-instalação](complete-the-post-installation-steps.md).  
  
 Use os parâmetros listados na tabela a seguir para desenvolver scripts de linha de comando para a instalação.  
  
|Parâmetro|Description|Valores com suporte|  
|---------------|-----------------|----------------------|  
|/CTLRSVCACCOUNT<br /><br /> **Opcional**|Conta de serviço para o serviço do controlador do Distributed Replay Utility.|Verifica a conta e a senha|  
|/CTLRSVCPASSWORD<br /><br /> **Opcional**|Senha da conta de serviço do controlador do Distributed Replay Controller.|Verifica a conta e a senha|  
|/CTLRSTARTUPTYPE<br /><br /> **Opcional**|Tipo de inicialização do serviço do controlador do Distributed Replay.|Automatic<br /><br /> Desabilitado<br /><br /> Manual|  
|/CTLRUSERS<br /><br /> **Opcional**|Especifique os usuários que têm permissões para o serviço do Distributed Replay Controller.|Conjunto de cadeias de contas de usuário que usam " " (espaço) para delimitador<br /><br /> **Importante**: quando você configura o serviço do controlador Distributed Replay, é possível especificar uma ou mais contas de usuário que serão usadas para executar os serviços de cliente do Distributed Replay. Esta é a lista das contas com suporte:<br /><br /> Conta de usuário do domínio<br /><br /> Conta de usuário local criada pelo usuário<br /><br /> Administrador<br /><br /> Conta virtual e MSA (Conta de Serviço Gerenciada)<br /><br /> Serviços de rede, serviços locais e sistema<br /><br /> <br /><br /> Não são aceitas contas de grupo (local ou domínio) e outras contas internas (como Todos).|  
|/CLTSVCACCOUNT<br /><br /> **Opcional**|Conta de serviço para o serviço do cliente do Distributed Replay.|Verifica a conta e a senha|  
|/CLTSVCPASSWORD<br /><br /> **Opcional**|Senha da conta de serviço do cliente Distributed Replay.|Verifica a conta e a senha|  
|/CLTSTARTUPTYPE<br /><br /> **Opcional**|Tipo de inicialização do serviço do cliente Distributed Replay.|Automatic<br /><br /> Desabilitado<br /><br /> Manual|  
|/CLTCTLRNAME<br /><br /> **Opcional**|O nome do computador com o qual o cliente se comunica para o serviço do controlador do Distributed Replay.||  
|/CLTWORKINGDIR<br /><br /> **Opcional**|O diretório de trabalho para o serviço do cliente do Distributed Replay.|Caminho válido|  
|/CLTRESULTDIR<br /><br /> **Opcional**|O diretório de resultado para o serviço do cliente do Distributed Replay.|Caminho válido|  
  
### <a name="sample-syntax"></a>Sintaxe de exemplo:  
 **Para instalar o componente do Distributed Replay Controller**  
  
```  
setup /q /ACTION=Install /FEATURES=DREPLAY_CTLR /IAcceptSQLServerLicenseTerms /CTLRUSERS="domain\user1" "domain\user2" /CTLRSVCACCOUNT="domain\svcuser" /CTLRSVCPASSWORD="password" /CTLRSTARTUPTYPE=Automatic  
```  
  
 **Para instalar o componente do cliente Distributed Replay**  
  
```  
setup /q /ACTION=Install /FEATURES=DREPLAY_CLT /IAcceptSQLServerLicenseTerms /CLTSVCACCOUNT="domain\svcuser" /CLTSVCPASSWORD="password" /CLTSTARTUPTYPE=Automatic /CLTCTLRNAME=ControllerMachineName /CLTWORKINGDIR="C:\WorkingDir" /CLTRESULTDIR="C:\ResultDir  
```  
  
  
