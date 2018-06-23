---
title: Pré-carregar o cache (Gerenciador de Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cache [Reporting Services]
- preloading cache
ms.assetid: 152a1051-8aa5-4c01-bc85-f8be8971b0cd
caps.latest.revision: 34
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: b24be62a990b92b522d6bf4d0bb04873b743fa99
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019056"
---
# <a name="preload-the-cache-report-manager"></a>Pré-carregar o cache (Gerenciador de Relatórios)
  Você pode pré-carregar o cache para um conjunto de dados compartilhado criando um plano de atualização do cache para o conjunto de dados compartilhado.  
  
 Você pode pré-carregar o cache para um relatório de duas maneiras:  
  
1.  Criar um plano de atualização do cache para o relatório. Este é o método preferencial.  
  
2.  Usar uma assinatura controlada por dados para pré-carregar o cache com instâncias de relatórios com parâmetros. Essa era a única maneira de pré-carregar o cache em versões do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] anteriores ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. Para obter mais informações, consulte [Armazenando relatórios em cache &#40;SSRS&#41;](caching-reports-ssrs.md).  
  
 As condições a seguir devem ser atendidas para que seja possível armazenar em cache um relatório ou um conjunto de dados compartilhado:  
  
-   O conjunto de dados compartilhado ou o relatório deve ter o armazenamento em cache habilitado.  
  
-   As fontes de dados compartilhadas do conjunto de dados compartilhado ou do relatório devem estar configurados para usar credenciais armazenadas ou nenhuma credencial.  
  
-   O serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve estar em execução.  
  
### <a name="to-preload-the-cache-by-creating-a-cache-refresh-plan"></a>Para pré-carregar o cache criando um plano de atualização do cache  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  No Gerenciador de Relatórios, navegue até a página **Conteúdo** e navegue até o item que deseja armazenar em cache.  
  
3.  Focalize o item, clique na lista suspensa e clique em **Gerenciar**.  
  
4.  Clique na guia **Opções de Atualização do Cache** .  
  
5.  Na barra de ferramentas, clique em **Novo Plano de Atualização do Cache**.  
  
    > [!NOTE]  
    >  Se o item não tiver o armazenamento em cache habilitado, será solicitado que você habilite o armazenamento em cache. Para habilitar o cache, clique em **OK**.  
  
     A página de Plano de Atualização do Cache é aberta.  
  
6.  Opcionalmente, digite uma descrição para o plano de atualização.  
  
7.  Para uma agenda compartilhada, clique em **Agenda Compartilhada**e selecione o nome da agenda a ser usada.  
  
     Para um agendamento personalizado, clique em **Agendamento específico do item**e clique em **Configurar**.  
  
8.  Configurar a agenda  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-preload-the-cache-with-a-user-specific-report-by-using-a-data-driven-subscription"></a>Para pré-carregar o cache com um relatório específico ao usuário usando uma assinatura controlada por dados  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  No Gerenciador de Relatórios, navegue até a página **Conteúdo** e navegue até o relatório para o qual você deseja criar uma assinatura.  
  
3.  Clique no relatório, na guia **Assinaturas** e em **Nova Assinatura Controlada por Dados**.  
  
4.  Opcionalmente, digite uma descrição para a assinatura.  
  
5.  Na lista **Especifique como os destinatários devem ser notificados** , selecione **Provedor de Entrega Nulo**.  
  
6.  Especifique um tipo de fonte de dados e clique em **Avançar** para configurar a fonte de dados.  
  
7.  Especifique o tipo de conexão, a cadeia de conexão e as credenciais para acessar a fonte de dados que contém dados de assinante. O exemplo a seguir ilustra uma cadeia de conexão usada para se conectar a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chamado Assinantes:  
  
    ```  
    data source=<servername>; initial catalog=Subscribers  
    ```  
  
8.  Clique em **Avançar**.  
  
9. Especifique a consulta ou o comando que recupera dados de assinante. Opcionalmente, aumente o período de tempo limite para as consultas que levam muito tempo para serem processadas. Por exemplo:  
  
    ```  
    Select * from UserInfo  
    ```  
  
10. Clique em **Validar**. A consulta deve ser validada antes de você continuar. Quando a mensagem **Consulta validada com êxito** for exibida, clique em **Avançar**.  
  
11. Como você não pode configurar as configurações de extensão de entrega para o provedor de entrega nulo, clique em **Avançar**.  
  
12. Especifique os valores de parâmetro do relatório para a assinatura e clique em **Avançar**.  
  
13. Especifique quando a assinatura é processada. Não escolha **Quando os dados do relatório forem atualizados no servidor de relatório**. Essa definição se aplica somente a instantâneos. Se quiser usar um agendamento preexistente, selecione **Em um agendamento compartilhado**.  
  
     Ou, para criar uma agenda personalizada, clique em **Em um agendamento criado para esta assinatura** e clique em **Avançar**. Configure a agenda e clique em **Concluir**.  
  
    > [!NOTE]  
    >  Para que os assinantes recebam o relatório mais recente, a gente que você configura deve ser consistente com a agenda de entrega do relatório definida para os assinantes. Para obter mais informações, consulte [Gerenciador de Relatórios &#40;modo nativo do SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
14. Configure as opções de Execução para o relatório como pode ser visto a seguir. Na página de relatório, clique na guia **Propriedades** .  
  
15. No quadro esquerdo, clique na guia **Execução** .  
  
16. Na página, selecione **Processar esse relatório com os dados mais recentes**.  
  
17. Escolha um das duas opções de cache a seguir e configure a validade do seguinte modo:  
  
    -   Para fazer com que uma cópia armazenada em cache expire depois de um período de tempo específico, clique em **Armazenar uma cópia temporária do relatório em cache. Expirar cópia de relatório após alguns minutos.** Digite o número de minutos para a validade do relatório.  
  
    -   Para fazer com que a cópia armazenada em cache expire de acordo com um agendamento, clique em **Armazenar uma cópia temporária do relatório em cache. Expirar cópia de relatório no próximo agendamento.** Clique em **Configurar**ou selecione um agendamento compartilhado para definir um agendamento para a expiração do relatório.  
  
18. Clique em **Aplicar**.  
  
## <a name="see-also"></a>Consulte também  
 [Assinaturas controladas por dados](../subscriptions/data-driven-subscriptions.md)   
 [Criar uma assinatura controlada por dados &#40;Tutorial do SSRS&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md)   
 [Desempenho, instantâneos, cache &#40;Reporting Services&#41;](performance-snapshots-caching-reporting-services.md)   
 [Definir propriedades de processamento de relatório](set-report-processing-properties.md)   
 [Armazenando relatórios em cache &#40;SSRS&#41;](caching-reports-ssrs.md)  
  
  