---
title: Aplicar hotfixes do Analytics Platform System | Microsoft Docs
description: Este artigo discute como aplicar hotfixes para o software do sistema de plataforma de análise.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b4b72017bb23ae44da9c5884f0ebf2a8b099fd3e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63019041"
---
# <a name="apply-analytics-platform-system-hotfixes"></a>Aplicar hotfixes do Analytics Platform System
Este artigo discute como aplicar hotfixes para o software do sistema de plataforma de análise.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
> [!WARNING]  
> Não tente aplicar um hotfix do Analytics Platform System, se seu dispositivo ou qualquer componente do dispositivo estiver inativo ou em uma falha ao longo de estado. Nesse caso, contate o suporte para obter assistência.  
  
> [!WARNING]  
> Não aplique um hotfix do Analytics Platform System, enquanto o dispositivo está em uso. Aplicar um hotfix, nós de dispositivo a reinicialização pode causar. O hotfix deve ser aplicado durante uma janela de manutenção quando o dispositivo não está sendo usado.  
  
### <a name="prerequisites"></a>Prerequisites  
Para executar essas etapas, você precisará de:  
  
-   Um logon do Analytics Platform System com permissões para acessar o Console de administração para monitorar o estado do dispositivo. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   Dados de Conhecimento da conta de administrador de domínio de malha para conectar-se para o _< nome_do_domínio >_ **-HST01** nó.  
  
## <a name="HowToInstallPDW"></a>Para aplicar um hotfix do Analytics Platform System  
Ao contrário de atualizações da Microsoft, os hotfixes para o software do Analytics Platform System não são manipulados por meio do WSUS. Eles têm um fluxo de trabalho diferente e são instalados por execução de um pacote de hotfix.  
  
1.  **Verifique se os indicadores de estado do dispositivo.**  
  
    1.  Abra o Console do administrador e navegue até a página de estado do dispositivo. Para obter mais informações, consulte [monitorar o dispositivo usando o Console de administração do &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
    2.  Todos os indicadores de vermelhos ou amarelos devem ser resolvidos antes de prosseguir para a próxima etapa. Duas exceções a isso são:  
  
        -   Se houver falhas de disco, use a página de alertas do Console de administrador para verificar se não há não mais de uma falha de disco em cada servidor ou uma matriz de SAN. Se houver falha de não mais de um disco em cada servidor ou uma matriz de SAN, você pode prosseguir para a próxima etapa antes de corrigir a falha de disco (s). Certifique-se de entrar em contato com o suporte da Microsoft para corrigir a falha de disco (s) assim que possível.  
  
        -   Se houver um erro de volume de disco (amarelo) não críticos que não está na unidade C:\, você pode prosseguir para a próxima etapa antes de resolver o erro de volume de disco.  
  
2.  **Instale o hotfix do Analytics Platform System**  
  
    1.  Logon para o <*appliance_domain*>-HST01 nó como o administrador de domínio.  
  
    2.  Use o **executar como administrador** opção para abrir um Prompt de comando.  
  
    3.  Execute o seguinte comando, substituindo *<HotfixPackageName>* com o nome do pacote executável de hotfix e substituindo os outros itens de espaço reservado *< >* com as informações apropriadas.  
  
        ```  
        <HotfixPackageName> /DomainAdminPassword="<password>"  
        ```  
  
    4.  Siga as etapas conforme apresentado pelo pacote de hotfix.  
  
## <a name="see-also"></a>Consulte também  
[Baixe e aplique as atualizações da Microsoft &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
[Desinstalar atualizações da Microsoft &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[Desinstalar Hotfixes do Analytics Platform System &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[Manutenção de software &#40;Analytics Platform System&#41;](software-servicing.md)  
  
