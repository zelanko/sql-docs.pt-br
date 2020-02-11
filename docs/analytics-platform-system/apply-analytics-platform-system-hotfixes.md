---
title: Aplicar hotfixes do Analytics Platform System
description: Este artigo discute como aplicar hotfixes ao software do sistema da plataforma de análise.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: fd62413ec8542aba9f3973d0e8483cb9c5c9128a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401370"
---
# <a name="apply-analytics-platform-system-hotfixes"></a>Aplicar hotfixes do Analytics Platform System
Este artigo discute como aplicar hotfixes ao software do sistema da plataforma de análise.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
> [!WARNING]  
> Não tente aplicar um hotfix do sistema de plataforma de análise se seu dispositivo ou qualquer componente de dispositivo estiver inoperante ou em um estado de failover. Nesse caso, entre em contato com o suporte para obter assistência.  
  
> [!WARNING]  
> Não aplique um hotfix do sistema de plataforma de análise enquanto o dispositivo estiver em uso. A aplicação de um hotfix pode fazer com que os nós do dispositivo sejam reinicializados. O hotfix deve ser aplicado durante uma janela de manutenção quando o dispositivo não está sendo usado.  
  
### <a name="prerequisites"></a>Prerequisites  
Para executar essas etapas, será necessário:  
  
-   Um logon do sistema de plataforma de análise com permissões para acessar o console de administração para monitorar o estado do dispositivo. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   Conhecimento da conta do administrador de domínio da malha para se conectar ao _<domain_name nó>_ **-HST01** .  
  
## <a name="HowToInstallPDW"></a>Para aplicar um hotfix do sistema de plataforma de análise  
Ao contrário das atualizações da Microsoft, os hotfixes para o software de sistema da plataforma de análise não são tratados por meio do WSUS. Eles têm um fluxo de trabalho diferente e são instalados executando um pacote de hotfix.  
  
1.  **Verifique os indicadores de estado do dispositivo.**  
  
    1.  Abra o console do administrador e navegue até a página estado do dispositivo. Para obter mais informações, consulte [monitorar o dispositivo usando o console de administração &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
    2.  Todos os indicadores vermelhos ou amarelos devem ser resolvidos antes de prosseguir para a próxima etapa. Algumas exceções a isso são:  
  
        -   Se houver falhas de disco, use a página de alertas do console de administração para verificar se não há mais de uma falha de disco em cada servidor ou matriz SAN. Se não houver mais de uma falha de disco em cada servidor ou matriz de SAN, você poderá prosseguir para a próxima etapa antes de corrigir as falhas de disco. Lembre-se de entrar em contato com o suporte da Microsoft para corrigir as falhas de disco assim que possível.  
  
        -   Se houver um erro de volume de disco não crítico (amarelo) que não esteja em C:\ , você pode prosseguir para a próxima etapa antes de resolver o erro de volume de disco.  
  
2.  **Instalar o hotfix do sistema da plataforma de análise**  
  
    1.  Faça logon no <*appliance_domain* nó>-HST01 como administrador de domínio.  
  
    2.  Use a opção **Executar como administrador** para abrir um prompt de comando.  
  
    3.  Execute o comando a seguir, *<HotfixPackageName>* substituindo pelo nome do pacote executável do hotfix e substituindo os outros itens de espaço reservado *<  >* com as informações apropriadas.  
  
        ```  
        <HotfixPackageName> /DomainAdminPassword="<password>"  
        ```  
  
    4.  Siga as etapas conforme apresentado pelo pacote de hotfix.  
  
## <a name="see-also"></a>Consulte Também  
[Baixar e aplicar as atualizações da Microsoft &#40;o sistema de plataforma de análise&#41;](download-and-apply-microsoft-updates.md)  
[Desinstalar o Microsoft Updates &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[Desinstale os hotfixes do Analytics Platform System &#40;o Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[Manutenção de software &#40;o sistema de plataforma de análise&#41;](software-servicing.md)  
  
