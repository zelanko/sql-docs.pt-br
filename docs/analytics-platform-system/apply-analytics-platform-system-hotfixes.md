---
title: Aplique Analytics Platform System (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fca5eec9-86b8-4d20-b498-1678c367b5c8
caps.latest.revision: 25
ms.openlocfilehash: 1a054ead9ef39169257eb1813ba49eae06082b96
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="apply-analytics-platform-system-hotfixes"></a>Aplicar Hotfixes do sistema de plataforma de análise
Este tópico discute como aplicar hotfixes para o software do sistema de plataforma de análise.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
> [!WARNING]  
> Não tente aplicar um hotfix Analytics Platform System se seu dispositivo ou qualquer componente do dispositivo está inativo ou em um failover de estado. Nesse caso, contate o suporte para obter assistência.  
  
> [!WARNING]  
> Não aplique um hotfix Analytics Platform System enquanto o dispositivo estiver em uso. Aplicação de um hotfix pode causar nós de dispositivo a reinicialização. O hotfix deve ser aplicado durante uma janela de manutenção quando o dispositivo não está sendo usado.  
  
### <a name="prerequisites"></a>Prerequisites  
Para executar essas etapas, você precisará de:  
  
-   Um logon de sistema de plataforma de análise com permissões para acessar o Console de administração para monitorar o estado do dispositivo. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   Conhecimento da conta de administrador de domínio de malha para conectar-se para o *< nome_do_domínio > * * *-HST01** nó.  
  
## <a name="HowToInstallPDW"></a>Para aplicar um hotfix Analytics Platform System  
Ao contrário das atualizações da Microsoft, os hotfixes para o software do sistema de plataforma de análise não são controlados por meio do WSUS. Eles têm um fluxo de trabalho diferente e são instalados pela execução de um pacote de hotfix.  
  
1.  **Verifique se os indicadores de estado do dispositivo.**  
  
    1.  Abra o Console do administrador e navegue até a página de estado do aplicativo. Para obter mais informações, consulte [monitorar o dispositivo usando o Console de administração &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
    2.  Todos os indicadores de vermelhos ou amarelos devem ser resolvidos antes de prosseguir para a próxima etapa. Duas exceções são:  
  
        -   Se houver falhas de disco, use a página de alertas do Console de administrador para verificar se não mais de uma falha de disco em cada servidor ou uma matriz SAN. Se houver falha de não mais de um disco em cada servidor ou uma matriz SAN, você pode prosseguir para a próxima etapa antes de corrigir a falha de disco (s). Certifique-se de entrar em contato com o suporte da Microsoft para corrigir a falha de disco (s) assim que possível.  
  
        -   Se houver um erro de volume de disco (amarelo) não críticos que não está na unidade C:\, você pode continuar para a próxima etapa antes de resolver o erro de volume do disco.  
  
2.  **Instale o hotfix Analytics Platform System**  
  
    1.  Logon para o <*appliance_domain*>-HST01 nó como o administrador de domínio.  
  
    2.  Use o **executar como administrador** opção para abrir um Prompt de comando.  
  
    3.  Execute o seguinte comando, substituindo *<HotfixPackageName>* com o nome do pacote executável do hotfix e substituindo os outros itens de espaço reservado *< >* com as informações apropriadas.  
  
        ```  
        <HotfixPackageName> /DomainAdminPassword="<password>"  
        ```  
  
    4.  Siga as etapas apresentadas pelo pacote de hotfix.  
  
## <a name="see-also"></a>Consulte também  
[Baixe e aplique as atualizações da Microsoft &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
[Desinstalar atualizações Microsoft &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[Desinstalar o Analytics Platform System Hotfixes &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[Manutenção de software &#40;Analytics Platform System&#41;](software-servicing.md)  
  
