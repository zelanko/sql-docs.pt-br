---
title: Opções de atualização do cache (Report Manager) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 227da40c-6bd2-48ec-aa9c-50ce6c1ca3a6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6ae1ee11edd51153585e9a6738bbfbd59af8974f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109917"
---
# <a name="cache-refresh-options-report-manager"></a>Opções de Atualização do Cache (Gerenciador de Relatórios)
  Use a página Opções de Atualização do Cache para criar agendas para pré-carregamento do cache com cópias temporárias de dados para um relatório ou para um conjunto de dados compartilhado. Um plano de atualização inclui uma agenda e a opção para especificar ou substituir valores de parâmetros. Para um conjunto de dados compartilhado, você não pode substituir valores de parâmetros que estão marcados como somente leitura. Você pode criar e usar mais de um plano de atualização como parte da página de opções de atualização.  
  
 As atribuições padrão de função que permitem adicionar, excluir, alterar e exibir relatórios e conjuntos de dados compartilhados relacionados para planos de atualização de cache são Gerenciador de Conteúdo, Meus Relatórios e Publicador.  
  
> [!NOTE]  
>  Este recurso não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="to-open-the-cache-refresh-plan-properties-page-for-a-report-or-shared-dataset"></a>Para abrir a página de propriedades do Plano de Atualização do Cache para um relatório ou conjunto de dados compartilhado  
  
1.  Abra o Gerenciador de Relatórios e localize o relatório ou conjunto de dados compartilhado cujas propriedades do plano de atualização do cache você deseja configurar.  
  
2.  Focalize o relatório ou o conjunto de dados compartilhado e clique na seta para baixo.  
  
3.  Na lista suspensa, clique em **Gerenciar**. A página **Propriedades gerais** é aberta.  
  
4.  Clique na guia **Plano de Atualização do Cache** .  
  
5.  Para criar um novo plano de cache, clique em **Novo Plano de Atualização do Cache**.  
  
    > [!NOTE]  
    >  Você deve habilitar e iniciar o serviço SQL Server Agent para criar um plano de atualização do cache.  
  
6.  Para criar uma cópia de um plano de cache e personalizá-la, clique em **Novo de Existente**.  
  
## <a name="cache-refresh-options"></a>Opções de Atualização do Cache  
 **Delete (excluir)**  
 Exclui todos os planos de atualização atualmente selecionados.  
  
 **Novo de Existente**  
 Essa opção é habilitada quando um e apenas um plano de atualização do cache é selecionado. Essa opção criará um novo plano de atualização que é copiado do plano original. A página Plano de Atualização do Cache é aberta pré-populada com detalhes do plano que foi selecionado. Você pode modificar as opções do plano de atualização e salvar o plano com uma nova descrição.  
  
 **Novo Plano de Atualização do Cache**  
 Clique para criar um novo plano de atualização a ser usado nas opções de atualização do cache atuais.  
  
 **Editar**  
 Selecione essa opção para editar o plano de atualização atual.  
  
## <a name="cache-refresh-plan-options"></a>Opções do Plano de Atualização do Cache  
 **Descrição**  
 Especifique uma descrição para o plano de atualização do cache.  
  
 **Agenda específica de item**  
 Selecione essa opção para criar uma agenda que será usada somente por este item.  
  
 **Configurar**  
 Clique para abrir a página Agenda que é usada para especificar informações de frequência.  
  
 Para obter mais informações, consulte a [página novo agendamento: editar agenda &#40;Report Manager&#41;](../../2014/reporting-services/new-schedule-edit-schedule-page-report-manager.md).  
  
 **Agenda compartilhada**  
 Selecione essa opção para selecionar uma agenda existente.  
  
 Para obter mais informações, consulte [Create, Modify, and Delete Schedules](subscriptions/create-modify-and-delete-schedules.md).  
  
 **@\<***Parâmetro* do**>**  
 Especifique uma combinação de valores de parâmetros. Essa seção aparece apenas se o conjunto de dados atual ou o relatório tiver parâmetros.  
  
 Consulte [Especificando Parâmetros](#Parameters) na próxima seção.  
  
 **Usar padrão**  
 Selecione essa opção para usar o valor padrão predefinido para este parâmetro.  
  
##  <a name="Parameters"></a>Especificando parâmetros  
 Para criar um plano de atualização do cache, cada parâmetro do relatório ou do conjunto de dados compartilhado deve ter um valor. Se o relatório ou o conjunto de dados compartilhado não tiver um valor padrão especificado na definição, você deverá especificar um valor. Se existir um valor padrão já existir, você não precisará fornecê-lo aqui. Se você fornecer um valor, ele substituirá o valor padrão.  
  
 Para especificar várias combinações de valores de parâmetros, crie um plano de atualização do cache separado para cada combinação.  
  
 Adições, alterações e exclusões feitas nos parâmetros em um relatório ou conjunto de dados compartilhado podem afetar o plano de atualização do cache. Se você adicionar um parâmetro com um valor padrão para um relatório, remover um parâmetro ou alterar o tipo de dados ou a opção somente leitura de um parâmetro do conjunto de dados compartilhado, as alterações entrarão em vigor na próxima vez que o plano de atualização do cache for processado.  
  
### <a name="shared-dataset-parameters"></a>Parâmetros de conjunto de dados compartilhado  
 Para um conjunto de dados compartilhado, as seguintes informações são derivadas da definição do conjunto de dados compartilhado:  
  
-   **Nome** do Especifica o nome do parâmetro de consulta.  
  
-   **Tipo** de Especifica o tipo de dados do parâmetro de consulta. Como esse tipo de dados é desconhecido até que o provedor de dados processe a consulta do conjunto de dados, a validação do tipo de dados não pode ocorrer até que o conjunto de dados compartilhado seja processado.  
  
-   **Permite valor nulo** Especifica se NULL é um valor válido.  
  
-   **Somente leitura** Especifica se este parâmetro está marcado como somente leitura na definição do conjunto de conjuntos compartilhado. Parâmetros somente leitura não aparecem na lista de parâmetros para opções de atualização do cache e têm um padrão especificado como parte da definição do conjunto de dados compartilhado.  
  
-   **Valores** de Valores padrão que foram especificados na definição do conjunto de valores compartilhado. Parâmetros de consulta podem ter múltiplos valores. Para substituir os valores padrão, digite novos valores nas áreas de prompt da caixa de texto.  
  
 Se a definição do conjunto de dados compartilhado especificar a opção **Omitir da consulta** para um parâmetro, você não precisará fornecer um valor padrão. Esse sinalizador indica que o parâmetro do conjunto de dados não é usado na consulta. Por exemplo, o parâmetro aparece na definição do conjunto de dados compartilhado porque é um parâmetro de relatório que é usado apenas no filtro do conjunto de dados.  
  
 Para exibir ou alterar opções de parâmetros do conjunto de dados, você deve editar a definição do conjunto de dados compartilhado. Para obter mais informações, consulte [Gerenciar conjuntos de dados compartilhados](report-data/manage-shared-datasets.md).  
  
### <a name="report-parameters"></a>Parâmetros de relatório  
 Para um relatório, cada valor de parâmetro deve ser válido para que você possa criar um plano de atualização do cache com êxito. Você deve digitar ou selecionar um valor padrão para cada parâmetro de relatório. O valor que você define substitui o valor padrão definido para o parâmetro de relatório no servidor de relatório.  
  
 Os parâmetros devem estar de acordo com os requisitos especificados nas propriedades do parâmetro no servidor de relatório. Por exemplo, se a Propriedade AllowBlank for false para um parâmetro de relatório, uma cadeia de caracteres vazia não será um valor válido.  
  
 Para exibir ou alterar opções de parâmetros de relatório, você deve editar os parâmetros de relatório no relatório ou, independentemente, no servidor de relatório. Para obter mais informações, consulte [conceito de parâmetros de relatório &#40;Construtor de relatórios e SSRS&#41;](report-design/report-parameters-concepts-report-builder-and-ssrs.md).  
  
## <a name="conditions-that-cause-a-cache-refresh-plan-to-be-inactive"></a>Condições que fazem com que um plano de atualização do cache fique inativo  
 As condições a seguir podem fazer com que um conjunto de dados compartilhado ou plano de atualização do cache do relatório fique inativo.  
  
-   A opção de cache do conjunto de dados compartilhado ou do relatório é desabilitada.  
  
-   Os valores dos parâmetros exigidos não estão definidos, não são válidos ou estão ausentes. Todas as consultas para um relatório devem ser válidas para que o relatório seja processado. Para um relatório que tem sub-relatórios, todas as consultas do conjunto de dados, inclusive conjuntos de dados do sub-relatório, são processadas primeiro. Se qualquer conjunto de dados não puder ser processado com êxito, o relatório não poderá ser executado.  
  
## <a name="conditions-that-cause-a-cache-refresh-plan-to-be-reactivated"></a>Condições que fazem com que um plano de atualização do cache seja reativado  
 Depois que um plano está inativo, proceda de uma das seguintes maneiras para disparar a avaliação de um plano de atualização do cache:  
  
-   Altere uma opção do plano.  
  
-   Habilite o cache para um conjunto de dados compartilhado ou relatório que esteja associado ao plano de atualização.  
  
-   Desmarque ou selecione a opção somente leitura para um parâmetro de consulta do conjunto de dados associado ao plano de atualização e salve a nova definição no servidor de relatório.  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas em nível de item](security/tasks-and-permissions-item-level-tasks.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Ajuda F1 Report Manager](../../2014/reporting-services/report-manager-f1-help.md)   
 [Armazenando relatórios em cache &#40;SSRS&#41;](report-server/caching-reports-ssrs.md)   
 [Gerenciar conjuntos de dados compartilhados](report-data/manage-shared-datasets.md)  
  
  
