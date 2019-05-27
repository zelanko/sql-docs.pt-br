---
title: 'Novo Agendamento: Editar agenda a página (Gerenciador de relatórios) | Microsoft Docs'
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 52a4d250-e185-4116-a29c-d809940a00fb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ea1eed70c3eac8bac1c4141628e72ce0af8099c2
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108144"
---
# <a name="new-schedule-edit-schedule-page-report-manager"></a>Novo Agendamento: Editar página de agenda (Gerenciador de relatórios)
  Use a página Nova Agenda / Editar Agenda para criar uma agenda para um relatório. As agendas são usadas com assinaturas para atualizar relatórios armazenados em cache e criar instantâneos como itens autônomos ou em histórico de relatório.  
  
> [!NOTE]  
>  Este recurso não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 Só é possível criar agendas para relatórios que podem ser executados de modo autônomo. A execução de um relatório autônomo requer que você armazene credenciais de fonte de dados de relatório no banco de dados do servidor de relatório. Para obter mais informações, consulte [página de propriedades de fontes de dados &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/data-sources-properties-page-report-manager.md).  
  
 Nem todas as combinações de frequência têm suporte em uma única agenda. Por exemplo, se você desejar executar um relatório às 12h00 e às 16h00 todas as sextas-feiras, você deverá criar duas agendas diárias que especifiquem uma data de execução na sexta-feira, uma com horário de início às 12h00 e outra com horário de início às 16h00.  
  
 O processamento da agenda se baseia no horário local do servidor de relatório que hospeda e processa a agenda.  
  
## <a name="navigation"></a>Navegação  
 Use os procedimentos a seguir para navegar para este local na interface do usuário.  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-execution-properties-page-of-a-report"></a>Para abrir a página Nova Agenda ou Editar Agenda a partir da página de propriedades de Execução de um relatório  
  
1.  Abra o Gerenciador de Relatórios e localize o relatório cuja agenda você deseja configurar.  
  
2.  Focalize o relatório e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Gerenciar**. Esse procedimento abre a página de propriedades Geral do modelo.  
  
4.  Selecione a guia **Execução** .  
  
5.  Selecione a opção **Renderizar este relatório em um instantâneo de execução de relatórios**. Em seguida, selecione **Use a agenda a seguir para adicionar instantâneos a histórico de relatórios**e selecione **Agenda específica do relatório**. Clique em **Configurar**.  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-history-properties-page-of-a-report"></a>Para abrir a página Nova Agenda ou Editar Agenda a partir da página de propriedades de Histórico de um relatório.  
  
1.  Abra o Gerenciador de Relatórios e localize o relatório cuja agenda você deseja configurar.  
  
2.  Focalize o relatório e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Gerenciar**. Esse procedimento abre a página de propriedades Geral do modelo.  
  
4.  Selecione a guia **Histórico** .  
  
5.  Selecione **Use a agenda a seguir para adicionar instantâneos a histórico de relatórios**e selecione **Agenda específica do relatório**. Clique em **Configurar**.  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-subscriptions-page"></a>Para abrir a página Nova Agenda ou Editar Agenda a partir da página Assinaturas.  
  
1.  Abra o Gerenciador de Relatórios e localize o relatório cuja agenda você deseja configurar.  
  
2.  Focalize o relatório e clique na seta do menu suspenso.  
  
3.  No menu suspenso,  
  
    -   Clique em **Gerenciar**. Esse procedimento abre a página de propriedades Geral do relatório. Em seguida, selecione a guia **Assinaturas** .  
  
    -   Clique em **Assinar**. Esse procedimento abre a página de propriedades de **Assinaturas** do relatório.  
  
4.  Na barra de ferramentas, clique em **Nova Assinatura** ou selecione uma assinatura existente para editar.  
  
5.  Em **Opções de Processamento de Assinaturas**, clique em **Nova Agenda**.  
  
## <a name="options"></a>Opções  
 **Detalhes da agenda**  
 Selecione opções que determinam quando e com que frequência um relatório é executado. As opções de frequência são colocadas em camadas. O primeiro conjunto de opções especifica uma categoria de frequência (a cada hora, diariamente, semanalmente e assim por diante). O segundo conjunto de opções exibido é baseado em sua seleção inicial.  
  
-   **Hora** define uma agenda que é executada a intervalos de hora em hora. Use a seção **Datas de início e término** para especificar o dia em que o agendamento deve ser executado.  
  
-   **Dia** define uma agenda que é executada nos dias que você seleciona, em uma hora e minuto específicos. Você pode especificar dias das seguintes maneiras: Cada \< *dia*>, cada dia da semana e cada \< *número*> dias. A escolha de uma abordagem invalida as outras, mesmo se os outros dias parecem selecionados.  
  
-   **Semana** define uma agenda que é executada a intervalos semanais, em uma hora e minuto específicos. O intervalo pode ser uma semana completa (por exemplo, a cada duas semanas) ou dias dentro de uma semana.  
  
-   **Mês** define uma agenda que é executada mensalmente. Dentro de um mês você pode escolher um dia com base em um padrão (por exemplo, o último domingo de cada mês) ou datas de calendário específicas (como 1 e 15, para indicar o primeiro e o décimo quinto dia de cada mês). Usando vírgulas e hífens, você pode especificar vários dias e intervalos, por exemplo, 1, 5, 7-12, 21.  
  
-   **Uma vez** define uma agenda que só executa uma vez. Use a seção **Datas de início e término** para especificar o dia em que o agendamento deve ser executado. Esta agenda expira assim que é processada.  
  
 **Datas de início e término**  
 Especifique uma data de início que determina quando o agendamento entra em vigor e uma data de término que determina quando a agendamento expira.  
  
 Os agendamentos expiram sem notificação. Depois da data de término, eles não são mais executados. Agendamentos expirados não são excluídos. Eles só podem ser excluídos manualmente. Assim, se você escolher continuar o agendamento, poderá estender a data de término.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Criar, modificar e excluir agendas](subscriptions/create-modify-and-delete-schedules.md)   
 [Ajuda F1 do Gerenciador de Relatórios](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
