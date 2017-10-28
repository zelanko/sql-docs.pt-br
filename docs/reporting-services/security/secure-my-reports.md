---
title: "Proteger meus relatórios | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- denying My Reports folder access
- private folders [Reporting Services]
- user workspace [Reporting Services]
- security [Reporting Services], My Reports folder
- My Reports folder [Reporting Services]
ms.assetid: 3b23a382-13b8-4196-9a93-7fe62d03a63c
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 162f43fc4f81c228d90839c75d1959d71eff9322
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="secure-my-reports"></a>Proteger Meus Relatórios
  O recurso Meus Relatórios fornece uma área de trabalho gerenciada pelo usuário para trabalhar com relatórios. Para funcionar conforme pretendido, a pasta Meus Relatórios requer permissões menos restritivas do que as outras pastas que estão disponíveis para uso geral. Os usuários que têm permissões apenas para exibir e executar relatórios em outras pastas podem precisar de um conjunto maior de permissões para gerenciar suas pastas Meus Relatórios e seu próprio conteúdo. O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece uma atribuição de função especializada e uma definição de função para essa finalidade.  
  
> [!NOTE]  
>  O recurso Meus Relatórios só está disponível no Gerenciador de Relatórios. Não está disponível em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
## <a name="role-assignment-for-my-reports"></a>Atribuição de função para Meus Relatórios  
 A atribuição de função para Meus Relatórios tem elementos predefinidos e é criada automaticamente para cada usuário que ativa uma pasta Meus Relatórios. A atribuição automática de segurança feita pelo servidor de relatório é especialmente útil para organizações que usam muito o recurso Meus Relatórios porque os administradores não precisam permitir o acesso para cada usuário dessa funcionalidade.  
  
 Uma atribuição de função de **Meus Relatórios** consiste nos seguintes elementos:  
  
-   O usuário da pasta Meus relatórios, que está localizada em pastas dos usuários\\*\<nome de usuário >*\My pasta de relatórios.  
  
-   A conta de usuário, que é determinada quando a pasta Meus Relatórios é ativada. Uma pasta é ativada quando o usuário clica em uma pasta Meus Relatórios no Gerenciador de Relatórios ou publica um relatório em uma pasta Meus Relatórios a partir do Designer de Relatórios. Essa pasta também é ativada quando o usuário solicita propriedades no link Meus Relatórios.  
  
-   A definição de função predefinida para Meus Relatórios.  
  
## <a name="role-definition-for-my-reports"></a>Definição de função para Meus Relatórios  
 A definição de função de **Meus Relatórios** inclui tarefas que dão suporte ao gerenciamento de conteúdo de uma pasta Meus Relatórios. A função **Meus Relatórios** tem uma única finalidade. Embora seja possível definir qualquer política de segurança no nível do item para essa pasta, evite fazer isso para minimizar a chance de modificá-la para satisfazer requisitos de outra pasta. A reserva da função **Meus Relatórios** para o recurso Meus Relatórios pode ajudar você a manter uma experiência consistente para os usuários.  
  
 Por padrão, só administradores de servidor de relatório modificam a função **Meus Relatórios** . Você pode personalizar a função **Meus Relatórios** alterando as tarefas que ela contém. Você também pode substituir uma função diferente.  
  
## <a name="denying-access-to-my-reports"></a>Negando o acesso a Meus Relatórios  
 Para impedir que os usuários acessem Meus Relatórios:  
  
-   Desabilite Meus Relatórios na página Configurações de Site. Para obter mais informações, consulte [Habilitar e desabilitar Meus Relatórios](../../reporting-services/report-server/enable-and-disable-my-reports.md).  
  
-   Remova todas as tarefas da função **Meus Relatórios** .  
  
 Ao desabilitar Meus Relatórios, o link para uma pasta Meus Relatórios é removido do Gerenciador de Relatórios. A estrutura de pasta subjacente que dá suporte a Meus Relatórios (quer dizer, a pasta Pastas dos Usuários e as subpastas) ainda estará disponível e poderá ser acessada se o usuário souber o caminho da pasta. A remoção de tarefas da função **Meus Relatórios** assegura a negação do acesso.  
  
## <a name="see-also"></a>Consulte também  
 [Proteger relatórios e recursos](../../reporting-services/security/secure-reports-and-resources.md)   
 [Proteger pastas](../../reporting-services/security/secure-folders.md)   
 [Concedendo permissões em um servidor de relatório do modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  

