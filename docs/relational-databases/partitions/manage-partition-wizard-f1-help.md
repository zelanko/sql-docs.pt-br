---
title: "Ajuda F1 do Assistente para Gerenciar Partição | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: partitions
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-partition
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- sql13.swb.managepartition.createjob.f1
- sql13.swb.managepartition.progress.f1
- sql13.swb.managepartition.getstart.f1
- sql13.swb.managepartition.selectswitchtables.f1
- sql13.swb.managepartition.stagingtable.f1
- sql13.swb.managepartition.switchin.f1
- sql13.swb.managepartition.switchout.f1
- sql13.swb.managepartition.partitionaction.f1
- sql13.swb.managepartition.summary.f1
- sql13.swb.managepartition.selectoutput.f1
helpviewer_keywords:
- wizards [SQL Server Management Studio] See Manage Partition Wizard
ms.assetid: e2478d26-dea4-428d-98c5-aad2d2a30da8
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: edef05d3a9cd1ae3a363a4cdead10130ee42459f
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="manage-partition-wizard-f1-help"></a>Ajuda de F1 do Assistente para Gerenciar Partição
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Use o **Assistente para Gerenciar Partição** para gerenciar e modificar as tabelas particionadas existentes por meio da troca de partição ou pela implementação de um cenário de janela deslizante. Esse assistente pode facilitar o gerenciamento das partições e simplificar a migração regular de dados de e para as tabelas.  
  
### <a name="to-start-the-manage-partition-wizard"></a>Para iniciar o Assistente para Gerenciar Partição  
  
-   No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], selecione o banco de dados, clique com o botão direito do mouse na tabela em que você deseja criar partições, aponte para **Armazenamento**e clique em **Gerenciar Partição**.  
  
     **Observação** Se a opção **Gerenciar Partição** não estiver disponível, talvez você tenha selecionado uma tabela que não contém partições. Clique em **Criar Partição** no submenu **Armazenamento** e use o **Assistente para Criar Partição** para criar partições na tabela.  
  
 Para obter mais informações sobre índices particionados, veja [Tabelas e índices particionados](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 Esta seção fornece as informações necessárias para gerenciar, modificar e implementar partições usando o **Assistente para Gerenciar Partição**.  
  
##  <a name="Top"></a> Nesta seção  
 As seções a seguir fornecem ajuda sobre as páginas do **Assistente para Gerenciar Partição**.  
  
 [Assistente para Gerenciar Partição (página Selecionar Ação de Partição)](#SelectPartitionAction)  
  
 [Assistente para Gerenciar Partição (página de ativação)](#SwitchIn)  
  
 [Assistente para Gerenciar Partição (página de desativação)](#SwitchOut)  
  
 [Assistente para Gerenciar Partição (Página Selecionar Opções da Tabela de Preparação)](#StagingTableOptions)  
  
 [Assistente para Gerenciar Partição (página Selecionar Opção de Saída)](#OutputOption)  
  
 [Assistente para Gerenciar Partição (página Nova Agenda de Trabalho)](#NewJob)  
  
 [Assistente para Gerenciar Partição (página Resumo)](#Summary)  
  
 [Assistente para Gerenciar Partição (página Progresso)](#Progress)  
  
##  <a name="SelectPartitionAction"></a> Página Selecionar Ação de Partição  
 Use a página **Selecionar Ação de Partição** para escolher a ação que você deseja executar na partição.  
  
### <a name="create-a-staging-table"></a>Criar uma tabela de preparação  
 A alternação de partições é uma tarefa de particionamento comum se houver uma tabela particionada para a qual e da qual você migrou dados com certa regularidade; por exemplo, existe uma tabela particionada que armazena dados trimestrais e você precisa mover novos dados para ela e arquivar dados antigos ao final de cada trimestre.  
  
 O assistente cria a tabela de preparação com a mesma estrutura de coluna de particionamento, tabela e coluna e com os mesmos índices e armazena a nova tabela no grupo de arquivos onde está a partição de origem.  
  
 Para criar uma tabela de preparo para inserir ou extrair os dados da partição, selecione **Criar uma tabela de preparo para alternar partições**.  
  
### <a name="sliding-window-scenario"></a>Cenário de janela deslizante  
 Para gerenciar as partições em um cenário da janela deslizante, selecione **Gerenciar dados particionados em um cenário de janela deslizante**.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Criar uma tabela de preparo para alternar partições**  
 Cria uma tabela de preparação para os dados que você está ativando ou desativando na tabela particionada existente.  
  
 **Desativar partição**  
 Fornece opções ao remover uma partição da tabela.  
  
 **Ativar partição**  
 Fornece opções ao adicionar uma partição à tabela.  
  
 **Gerenciar dados particionados em um cenário de janela deslizante**  
 Acrescenta uma partição vazia à tabela existente que pode ser usada para alternar dados. O assistente oferece suporte à alternância para a última partição e da primeira partição.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../analysis-services/instances/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início") [Nesta seção](#Top)  
  
##  <a name="SwitchIn"></a> Página Selecione as Opções de Inserção de Partição  
 Use a página **Selecione as opções de Inserção de Partição** para selecionar a tabela de preparo que você está ativando na tabela particionada.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Mostrar Todas as Partições**  
 Selecione para mostrar todas as partições, inclusive as partições que estão na tabela particionada no momento.  
  
 **Grade de partição**  
 Exibe o nome da partição, o **Limite esquerdo**, o **Limite direito**, o **Grupo de arquivos**e a **Contagem de linhas** das partições selecionadas.  
  
 **Tabela de inserção**  
 Selecione a partição de preparação que contém a partição à qual você deseja adicionar a tabela particionada. É necessário criar essa tabela de preparo antes de ativar as partições com o **Assistente para Gerenciar Partições**.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../analysis-services/instances/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início") [Nesta seção](#Top)  
  
##  <a name="SwitchOut"></a> Página Selecione as Opções de Extração de Partição  
 Use a página **Selecione as opções de Extração de Partição** para selecionar a partição e a tabela de preparo para reter os dados particionados que você está desativando na tabela particionada.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Grade de partição**  
 Exibe o nome da partição, o **Limite esquerdo**, o **Limite direito**, o **Grupo de arquivos**e a **Contagem de linhas** das partições selecionadas.  
  
 **Tabela de extração**  
 Escolha uma nova tabela ou uma tabela existente no qual os dados serão desativados.  
  
 **Nova**  
 Digite um novo nome para a tabela de preparação que você deseja usar para a partição a ser desativada da tabela de origem atual.  
  
 **Existente**  
 Selecione uma tabela de preparação existente que você deseja usar para a partição a ser desativada da tabela de origem atual. Se a tabela existente contiver dados, eles serão substituídos pelos dados que você está desativando.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../analysis-services/instances/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início") [Nesta seção](#Top)  
  
##  <a name="StagingTableOptions"></a> Página Selecionar Opções da Tabela de Preparação  
 Use a página **Selecionar Opções da Tabela de Preparação** para criar a tabela de preparo que você deseja usar para alternar os dados particionados.  
  
 As tabelas de preparação devem residir no mesmo grupo de arquivos da partição selecionada da tabela de origem. A tabela de preparação deve espelhar o design da tabela de origem e da tabela de destino.  
  
 Também é possível criar os mesmos índices na tabela de preparação existente na partição de origem. A tabela de preparação contém automaticamente uma restrição que se baseia nos elementos da partição de origem. Normalmente, essa restrição é gerada a partir do valor de limite da partição de origem.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Nome da tabela de preparação**  
 Crie um nome para a tabela de preparação ou aceite o nome padrão exibido na caixa de edição.  
  
 **Alternar partição**  
 Selecione a partição de origem que você quer alternar com a tabela atual.  
  
 **Novo valor de limite**  
 Selecione ou digite o valor de limite desejado para a partição da tabela de preparação.  
  
 **Grupo de arquivos**  
 Selecione um grupo de arquivos para a nova tabela.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../analysis-services/instances/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início") [Nesta seção](#Top)  
  
##  <a name="OutputOption"></a> Página Selecionar Opção de Saída  
 Use a página **Selecionar Opção de Saída** para especificar como deseja concluir as modificações em suas partições.  
  
### <a name="create-script"></a>Criar script  
 Quando o assistente é concluído, ele cria um script no Editor de Consultas para modificar partições na tabela. Selecione **Criar Script** se desejar examinar o script. Em seguida, execute o script manualmente.  
  
 **Script para arquivo**  
 Gere o script em um arquivo .sql. Especifique **Unicode** ou **Texto ANSI**. Para especificar nome e localização para o arquivo, clique em **Procurar**.  
  
 **Script para Área de Transferência**  
 Salve o script na área de transferência.  
  
 **Script para Nova Janela de Consulta**  
 Gere o script para uma janela do Editor de Consultas. Se não houver uma janela de editor aberta, uma nova janela será aberta como destino para o script.  
  
### <a name="run-immediately"></a>Executar imediatamente  
 **Run immediately**  
 Faça com que o assistente conclua as modificações nas partições quando você clicar em **Avançar** ou em **Concluir**.  
  
### <a name="schedule"></a>Agenda  
 Selecione para modificar as partições de tabela na data e na hora agendadas.  
  
 **Alterar agenda**  
 Abre a caixa de diálogo **Novo Agendamento de Trabalho** , em que é possível selecionar, alterar ou exibir as propriedades do trabalho agendado.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../analysis-services/instances/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início") [Nesta seção](#Top)  
  
##  <a name="NewJob"></a> Página Nova Agenda de Trabalho  
 Use a página **Novo Agendamento de Trabalho** para exibir e alterar as propriedades do agendamento.  
  
### <a name="options"></a>Opções  
 Selecione o tipo de agenda que deseja para o trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 **Nome**  
 Digite um nome novo para a agenda.  
  
 **Trabalhos na agenda**  
 Exiba os trabalhos existentes que usam a agenda.  
  
 **Tipo de agenda**  
 Selecione o tipo de agenda.  
  
 **Enabled**  
 Habilite ou desabilite a agenda.  
  
### <a name="recurring-schedule-types-options"></a>Opções de tipos de agenda recorrentes  
 Selecione a frequência do trabalho agendado.  
  
 **Ocorre**  
 Selecione o intervalo no qual a agenda ocorre periodicamente.  
  
 **Repete-se a cada**  
 Selecione o número de dias ou semanas entre ocorrências periódicas da agenda. Essa opção não está disponível para agendas mensais.  
  
 **Segunda-feira**  
 Defina o trabalho para ocorrer em uma segunda-feira. Disponível somente para agendamentos semanais.  
  
 **Terça-feira**  
 Defina o trabalho para ocorrer em uma terça-feira. Disponível somente para agendamentos semanais.  
  
 **Quarta-feira**  
 Defina o trabalho para ocorrer em uma quarta-feira. Disponível somente para agendamentos semanais.  
  
 **Quinta-feira**  
 Defina o trabalho para ocorrer em uma quinta-feira. Disponível somente para agendamentos semanais.  
  
 **Sexta-feira**  
 Defina o trabalho para ocorrer em uma sexta-feira. Disponível somente para agendamentos semanais.  
  
 **Sábado**  
 Defina o trabalho para ocorrer em um sábado. Disponível somente para agendamentos semanais.  
  
 **Domingo**  
 Defina o trabalho para ocorrer em um domingo. Disponível somente para agendamentos semanais.  
  
 **Day**  
 Selecione o dia do mês que a agenda ocorre. Disponível somente para agendas mensais.  
  
 **de cada**  
 Selecione o número de meses entre ocorrências da agenda. Disponível somente para agendas mensais.  
  
 **O**  
 Especifique uma agenda durante um dia específico da semana em uma semana específica durante o mês. Disponível somente para agendas mensais.  
  
 **Ocorre uma vez em**  
 Defina a hora para que um trabalho ocorra diariamente.  
  
 **Ocorre a cada**  
 Defina o número de horas ou minutos entre ocorrências.  
  
 **Data de início**  
 Defina a data quando essa agenda ficará efetiva.  
  
 **Data de término**  
 Defina a data quando a agenda já não será válida.  
  
 **Nenhuma data de término**  
 Especifique que a agenda permanecerá efetiva indefinidamente.  
  
### <a name="one-time-schedule-types-options"></a>Opções de tipos de agendas que ocorrem apenas uma vez  
 Se você agendar um trabalho para uma única execução, selecione uma data e uma hora no futuro.  
  
 **Date**  
 Selecione a data para que o trabalho seja executado.  
  
 **Hora**  
 Selecione a hora para que o trabalho seja executado.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../analysis-services/instances/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início") [Nesta seção](#Top)  
  
##  <a name="Summary"></a> Página de Resumo  
 Use a página **Resumo** para examinar as opções selecionadas nas páginas anteriores.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Examinar as seleções**  
 Exibe as seleções feitas em cada página do assistente. Clique em um nó para expandir e exibir as opções selecionadas anteriormente.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../analysis-services/instances/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início") [Nesta seção](#Top)  
  
##  <a name="Progress"></a> Página Progresso  
 Use a página **Progresso** para monitorar informações de status das ações do **Assistente para Gerenciar Partição**. Dependendo das opções selecionadas no assistente, a página **Progresso** pode conter uma ou várias ações. A caixa superior exibe o status geral do assistente e o número de mensagens de status, erro e aviso que ele recebeu.  
  
### <a name="options"></a>Opções  
 **Detalhes**  
 Fornece a ação, status e qualquer mensagem retornada pela ação executada pelo assistente.  
  
 **Ação**  
 Especifica o tipo e o nome de cada ação.  
  
 **Status**  
 Indica se a ação do assistente retornou como um todo o valor de **Êxito** ou de **Falha**.  
  
 **Mensagem**  
 Fornece qualquer mensagem de aviso ou erro retornada pelo processo.  
  
 **Parar**  
 Interrompe a ação do assistente.  
  
 **Relatório**  
 Crie um relatório contendo os resultados do **Assistente para Gerenciar Partição**. As opções são:  
  
-   **Exibir Relatório**  
  
-   **Salvar Relatório no Arquivo**  
  
-   **Copiar Relatório na Área de Transferência**  
  
-   **Enviar Relatório como Email**  
  
 **Exibir Relatório**  
 Abra a caixa de diálogo **Exibir Relatório** . Essa caixa de diálogo contém um relatório de texto do progresso do **Assistente para Gerenciar Partição**.  
  
 **Fechar**  
 Feche o assistente.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../analysis-services/instances/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início") [Nesta seção](#Top)  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas e índices particionados](../../relational-databases/partitions/partitioned-tables-and-indexes.md)  
  
  
