---
title: Pré-carregar o cache (SSRS)| Microsoft Docs
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- cache [Reporting Services]
- preloading cache
ms.assetid: 152a1051-8aa5-4c01-bc85-f8be8971b0cd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6b2be1e020354f47aa21dc83f17ff6169bcf2d72
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "66174997"
---
# <a name="preload-the-cache"></a>Pré-carregar o cache  
  Você pode pré-carregar o cache para um conjunto de dados compartilhado criando um plano de atualização do cache para o conjunto de dados compartilhado.  
  
 Você pode pré-carregar o cache para um relatório de duas maneiras:  
  
1.  Criar um plano de atualização do cache para o relatório. Este é o método preferencial.  
  
2.  Usar uma assinatura controlada por dados para pré-carregar o cache com instâncias de relatórios com parâmetros. Essa era a única maneira de pré-carregar o cache em versões do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] anteriores ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. Para obter mais informações, consulte [Armazenando relatórios em cache &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md).  
  
 As condições a seguir devem ser atendidas para que seja possível armazenar em cache um relatório ou um conjunto de dados compartilhado:  
  
-   O conjunto de dados compartilhado ou o relatório deve ter o armazenamento em cache habilitado.  
  
-   As fontes de dados compartilhadas do conjunto de dados compartilhado ou do relatório devem estar configurados para usar credenciais armazenadas ou nenhuma credencial.  
  
-   O serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve estar em execução.  
  
## <a name="to-preload-the-cache-by-creating-a-cache-refresh-plan"></a>Para pré-carregar o cache criando um plano de atualização do cache  
  
1. Inicie o [portal da Web de um servidor de relatório](../../reporting-services/web-portal-ssrs-native-mode.md "O portal da Web de um servidor de relatório").  
  
2. Selecione **Procurar** na Página Inicial e navegue pela hierarquia de pastas até localizar o item que você deseja armazenar em cache.  
  
3. Selecione as reticências no canto superior direito do item e selecione **Gerenciar** no menu suspenso.  
  
4. Selecione a guia **Cache** no menu vertical à esquerda.  
  
5. Para ativar o cache de um conjunto de dados, selecione o botão de opção **Armazenar cópias deste conjunto de dados em cache e usá-las quando disponíveis**. A seção **Expiração do cache** aparece abaixo dele. Selecione um destes botões de opção:

    - **O cache expira após x minutos** (insira o número desejado de minutos para x).
    - **O cache expira segundo uma agenda**.  O Reporting Services fornece agendas compartilhadas e outras específicas ao relatório, para ajudar você a controlar o processamento, a consistência do conteúdo e o desempenho da distribuição dos relatórios. Para obter mais informações, consulte [Create, Modify, and Delete Schedules](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md "Create, Modify, and Delete Schedules"). Há várias opções para criar uma agenda, neste caso, para expiração do cache: selecione uma das duas opções de agenda abaixo:  
      - botão de opção **Agenda compartilhada** e selecione uma agenda na caixa de texto suspensa **Selecione uma agenda compartilhada**. Para obter mais informações, consulte [Schedules](../../reporting-services/subscriptions/schedules.md "Agendas").  
      - botão de opção **Agenda específica do relatório** e selecione o link **Editar agenda**, para exibir a página *Detalhes da agenda*.  

         ![A página de detalhes da agenda de expiração do cache do portal da Web para conjuntos de dados](../../reporting-services/report-server/media/preload-the-cache/web-portal-dataset-cache-schedule-details.png "Página detalhes da agenda do cache de conjunto de dados")

          Nesta página, você pode selecionar:
         - O tipo de agenda:
           - **Hora** - execute a agenda a cada: especifique as horas e os minutos, e a hora de início.
           - **Dia** - selecione uma das três opções abaixo:  
              - **Nos seguintes dias**: (domingo, segunda-feira, terça-feira, quarta-feira, quinta-feira, sexta-feira, sábado).
              - **Todos os dias úteis**
              - **Repetir após esse número de dias** - especifique um número.  
           - **Semana** - especifique os dois itens a seguir:
              - **Repetir após esse número de semanas** - especifique um número.  
              - **Nos dias** - escolha os dias da semana para executá-lo.  
           - **Mês** - quais meses, com a opção de:
              - **Na semana do mês**,  
                 - Selecione (1º, 2ª, 3ª, 4º ou última) na lista suspensa.  
                 - **No dia da semana** para executá-lo. Marque uma ou mais caixas de seleção (Dom, Seg, Ter, Qua, Qui, Sex, Sáb).  
                 - **Nos dias do calendário** – insira o número do dia do mês separado por vírgulas, ou um intervalo de dias separados por um traço ou qualquer combinação de ambos (por exemplo, 1,3-5).  
           - **Uma vez** - uma única ocorrência.  
         - **Hora de início** - o horário do dia para o início da agenda.  
         - **Datas inicial e final** - especifique a data de início e, opcionalmente, a data de término da agenda.
         - Selecione **Aplicar** para salvar a agenda.  
           > [!NOTE]
           > Se o item não tiver o armazenamento em cache habilitado, será solicitado que você habilite o armazenamento em cache. Para habilitar o cache, selecione **OK**.  

         - Selecione **Criar plano de atualização de cache** para criar/salvar o plano de cache.  
         A página **Planos de Atualização do Cache** é aberta na tela. Nela você pode:
           - Adicionar um novo plano de atualização do cache.
           - Criar um novo plano de atualização de cache com base em um plano existente.
           - Atualizar a página de planos de atualização do cache.
           - Excluir um plano.
           - Procurar um plano pelo nome.

         Se não houver planos de atualização do cache salvos ainda, a lista estará vazia e a opção "Adicionar" será a única opção disponível. Selecione **+ Novo plano de atualização do cache** para adicionar um novo, e a página **Novo Plano de Atualização do Cache** será exibida.  
           - Digite uma **Descrição** na primeira caixa de texto para nomear o plano de atualização.  
           - Selecione um dos seguintes botões de opção em **Atualizar o cache na seguinte agenda**  
             - **Agenda compartilhada** - selecione uma agenda compartilhada na lista suspensa adjacente. 
             - **Agenda específica do relatório** - edite a agenda como na etapa 2.2 acima, selecionando o link **Editar agenda** para exibir a página *Detalhes da agenda*. 
             - Selecione **Criar plano de atualização de cache** para salvar o plano se estiver adicionando, ou **Aplicar** se estiver editando o plano.  
      Você retornará para a página **Planos de Atualização do Cache** atualizada.
  
## <a name="to-preload-the-cache-with-a-user-specific-report-by-using-a-data-driven-subscription"></a>Para pré-carregar o cache com um relatório específico ao usuário usando uma assinatura controlada por dados

1. Inicie o [portal da Web de um servidor de relatório](../../reporting-services/web-portal-ssrs-native-mode.md "O portal da Web de um servidor de relatório").  
2. Selecione **Procurar** na Página Inicial e navegue pela hierarquia de pastas até localizar o relatório que você quer assinar.  
3. Clique com o botão direito do mouse no relatório, selecione **Assinar** no menu suspenso. A página **Novas Assinaturas** é exibida.  
4. Insira uma descrição para a assinatura na caixa de texto **Descrição**.  
5. O botão de opção **Tipo de assinatura** exibe duas opções:  
   - **Assinatura padrão** - para gerar e fornecer um relatório
   - **Assinatura controlada por dados** - para gerar e fornecer um relatório para cada linha em um conjunto de dados. Essa é a opção para pré-carregar o cache.
6. Na seção **Agenda**, selecione um destes botões de opção:
   - **Agenda compartilhada** - selecione uma agenda compartilhada na lista suspensa.  
   - **Agenda específica do relatório** - edite a agenda como na etapa 2.2 acima, selecionando o link **Editar agenda** para exibir a página *Detalhes da agenda*.  
7. A seção **Destino** exibe as seguintes opções em uma caixa suspensa:
    - **Compartilhamento de Arquivos do Windows**
    - **Email**
    - **Provedor de Entrega Nulo** – para esta tarefa, selecione Provedor de Entrega Nulo.  
8. Na seção **Conjunto de dados**, edite ou crie um conjunto de dados dessa assinatura de relatório, selecionando o botão **Editar conjunto de dados**.  
9. Na página **Editar Conjunto de Dados**, na seção **Fonte de dados**, escolha a fonte de dados que contém os valores de parâmetro de relatório e as opções de entrega. Suas opções são:  
   - **Uma fonte de dados compartilhada** - selecione as reticências e selecione uma fonte de dados compartilhada na pasta *Fonte de Dados Compartilhada*.
   - **Uma fonte de dados personalizada** - a mais provável. Essa é a opção que você terá que escolher, a menos que você ou outra pessoa já tenha concluído as etapas abaixo para criar como uma fonte de dados compartilhada.  
     - Especifique o tipo de conexão, a cadeia de conexão e as credenciais para acessar a fonte de dados que contém dados de assinante. O exemplo a seguir ilustra uma cadeia de conexão usada para se conectar a um banco de dados SQL Server chamado Subscribers (Assinantes).  
  
   ```T-SQL
   data source=<servername>;initial catalog=Subscribers  
   ```
  
10. Na seção **Consulta** – especifique a consulta que recupera os dados do assinante desejado.  Por exemplo:  
  
    ```T-SQL  
    Select * from RptSubscribers  
    ```
  
    Opcionalmente, aumente o período de tempo limite para as consultas que levam muito tempo para serem processadas.  
  
11. Selecione **Validar**. A consulta deve ser validada antes de você continuar. Quando a mensagem **Validação bem-sucedida** for exibida, também será exibida uma lista de campos de Conjunto de dados abaixo do botão **Validar**. Selecione **Aplicar** para criar a fonte de dados personalizada.  
  
12. Você será levado de volta à página **Nova Assinatura**.  Na seção **Parâmetros de Relatório**, especifique os valores de parâmetro do relatório para os parâmetros do relatório exibidos, se houver algum.  

13. Selecione **Criar assinatura**.  
  
14. A página **Assinaturas** é exibida, mostrando sua nova Assinatura controlada por dados. Nessa página, você poderá habilitar a assinatura, quando estiver pronto, marcando a caixa de seleção à esquerda dela e selecionando o botão **Habilitar**. ![botão habilitar página de assinaturas](../../reporting-services/report-server/media/preload-the-cache/subscriptions-page-enable-button.png "O botão habilitar na página de assinaturas")

15. Especifique quando a assinatura é processada. Não escolha **Quando os dados do relatório forem atualizados no servidor de relatório**. Essa definição se aplica somente a instantâneos. Se quiser usar um agendamento preexistente, selecione **Em um agendamento compartilhado**.  
  
     Ou, para criar uma agenda personalizada, selecione **Em um agendamento criado para esta assinatura** e selecione **Avançar**. Configure a agenda e selecione **Concluir**.  
  
    > [!NOTE]  
    > Para que os assinantes recebam o relatório mais recente, a gente que você configura deve ser consistente com a agenda de entrega do relatório definida para os assinantes. Para saber mais, confira o [portal da Web de um servidor de relatório](../../reporting-services/web-portal-ssrs-native-mode.md  "O portal da Web de um servidor de relatório").  
  
16. Configure as opções de Execução para o relatório como pode ser visto a seguir. Na página do relatório, clique na guia **Propriedades**.  
  
17. No quadro esquerdo, selecione a guia **Execução**.  
  
18. Na página, selecione **Processar esse relatório com os dados mais recentes**.  
  
19. Escolha um das duas opções de cache a seguir e configure a validade do seguinte modo:  
  
    - Para fazer com que uma cópia armazenada em cache expire depois de um período de tempo específico, selecione **Armazenar uma cópia temporária do relatório em cache. Expirar cópia de relatório após alguns minutos.** Digite o número de minutos para a validade do relatório.  
  
    - Para fazer com que a cópia armazenada em cache expire de acordo com um agendamento, selecione **Armazenar uma cópia temporária do relatório em cache. Expirar cópia de relatório no próximo agendamento.** Selecione **Configurar**ou selecione um agendamento compartilhado para definir um agendamento para a expiração do relatório.  
  
20. Escolha **Aplicar**.
  
## <a name="see-also"></a>Confira também  

 [Assinaturas controladas por dados](../../reporting-services/subscriptions/data-driven-subscriptions.md)  
 [Criar uma assinatura controlada por dados &#40;Tutorial do SSRS&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
 [Desempenho, instantâneos, cache &#40;Reporting Services&#41;](../../reporting-services/report-server/performance-snapshots-caching-reporting-services.md)  
 [Definir propriedades de processamento de relatórios](../../reporting-services/report-server/set-report-processing-properties.md)  
 [Armazenando relatórios em cache &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)  
 [Working with shared datasets (Trabalhando com conjuntos de dados compartilhados)](../../reporting-services/work-with-shared-datasets-web-portal.md)  
  
