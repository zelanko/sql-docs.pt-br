---
title: Plano de manutenção (Guia Design)
description: Plano de manutenção (Guia Design)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.maintplanproperties.optimizations.f1
- sql13.swb.maint.planeditor.f1
- sql13.swb.maint.subplaneditor.f1
- Task.FileExtension
ms.assetid: 6d20d4d4-5b3f-454a-8a05-f0aac803c5ad
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 75cc3aaec07d038ed6218a7a20268e94f23d3949
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "93067302"
---
# <a name="maintenance-plan-design-tab"></a>Plano de manutenção (Guia Design)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

 Use o **Plano de Manutenção (Guia Design)** para especificar as propriedades de um plano de manutenção e seus subplanos. Arraste tarefas da caixa de ferramentas para o designer de plano. Clique com o botão direito do mouse em grupos de tarefas para criar caminhos de execução de ramificação. Os planos de manutenção são salvos como pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e são executados pelos trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opções  
 **Adicionar Subplano**  
 Adicione um subplano que você possa configurar.  
  
 **Propriedades do Subplano**  
 Exiba a caixa de diálogo **Propriedades do Subplano** . Selecione um subplano na grade e clique nesse ícone para inserir um nome, uma descrição e uma agenda para o subplano. Você também pode clicar duas vezes no subplano na grade para exibir a caixa de diálogo **Propriedades do Subplano** . Os nomes dos subplanos são limitados a 128 caracteres e suas descrições são limitadas a 512 caracteres.  
  
 **Exclua o Subplano Selecionado**  
 Exclua o subplano selecionado.  
  
 **Agenda do Subplano**  
 Exiba a caixa de diálogo **Propriedades do Agendamento do Trabalho** . Selecione um subplano na grade e clique nesse ícone para configurar uma agenda para o subplano.  
  
 **Remover Agenda**  
 Remova uma agenda do subplano selecionado.  
  
 **Gerenciar Conexões**  
 Exiba a caixa de diálogo **Gerenciar Conexões** . Usado para adicionar conexões de instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] adicionais ao plano de manutenção. Cada tarefa de manutenção no editor de subplano pode usar quaisquer dessas conexões. Quando executando, o plano de manutenção faz uma conexão do servidor do plano de manutenção para os servidores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificados usando credenciais de conexão.  
  
 **Relatório e Registro em Log**  
 Exiba a caixa de diálogo **Relatório e Registro em Log** , usada para gerenciar os relatórios relacionados com a atividade do plano de manutenção e para configurar o log ao servidor local ou remoto.  
  
 **Servidores**  
 Exiba a caixa de diálogo **Servidores** , que é usada para selecionar os servidores em que serão executadas as tarefas do subplano. Essa opção só está habilitada em servidores mestre em ambientes multisservidor. Para obter mais informações, veja [Criar um ambiente multisservidor](../../ssms/agent/create-a-multiserver-environment.md).  
  
 **Nome**  
 Exibe o nome do plano de manutenção. Para planos de manutenção novos, o nome é especificado em uma caixa de diálogo antes que o designer de plano de manutenção seja aberto. Para renomear um plano de manutenção, clique com o botão direito do mouse no plano no Pesquisador de Objetos e clique em **Renomear**.  
  
 **Descrição**  
 Exiba ou especifique uma descrição para o plano de manutenção. O comprimento máximo para uma descrição é 512 caracteres.  
  
 **Superfície do Designer**  
 Executa design e mantém os planos de manutenção. Use a superfície de designer para adicionar tarefas de manutenção a um plano, remover tarefas de um plano, especificar os links com precedência entre tarefas e para indicar a ramificação ou paralelismo de uma tarefa.  
  
 Um link de precedência entre duas tarefas estabelece uma relação entre elas. A segunda tarefa (a *tarefa dependente*) é executada somente se o resultado da execução da primeira tarefa (a *tarefa precedente*) corresponde aos critérios especificados. Normalmente o resultado da execução especificado é **Êxito**, **Falha** ou **Conclusão**. A superfície do designer do plano de manutenção baseia-se na superfície do designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Para obter informações, consulte [Restrições de precedência](../../integration-services/control-flow/precedence-constraints.md).  
  
 Por exemplo, poderá ser especificada a execução de uma tarefa Índice de Desfragmentação somente se a tarefa anterior Verificar a Integridade do Banco de Dados for completada com êxito. O recurso de vinculação de precedência de tarefa também permite que sejam tratadas condições de erro ou falha em um plano. Por exemplo, se a tarefa Verificar a Integridade do Banco de Dados falhar, uma tarefa Notificar Operador poderá notificar o usuário ou o operador sobre a falha.  
  
 A especificação de tarefas a serem executadas após a falha de uma tarefa anterior é um exemplo da *ramificação de tarefa*.  
  
 Indicando que duas ou mais tarefas iniciem simultaneamente, por exemplo, depois do término de uma tarefa anterior com êxito, é um exemplo da especificação do *paralelismo de tarefa*. Todas as tarefas sem-restrições iniciarão e executarão em paralelo. Use restrições para atrasar tarefas de modo que tarefas anteriores terminem antes.  
  
 Depois que uma tarefa de manutenção é colocada na superfície de design, suas propriedades podem ser editadas como necessário. Por exemplo, o banco de dados específico para fazer o backup na tarefa Executar Backup do Banco de Dados é especificado depois que a tarefa é adicionada ao plano. Tarefas na superfície de design que não são configuradas corretamente contêm um ícone vermelho com um x branco.  
  
 Para adicionar uma tarefa a um plano, arraste o ícone da tarefa da caixa de ferramentas **Tarefas do Plano de Manutenção** até a superfície de design do plano ou clique duas vezes na tarefa na caixa de ferramentas, o que adiciona a tarefa à superfície de designer ativa no momento. Se a caixa de ferramentas **Tarefas do Plano de Manutenção** não estiver visível, escolha **Caixa de Ferramentas** no menu [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Exibir** do . Expanda o nó **Tarefas do Plano de Manutenção** no painel **Caixa de Ferramentas** .  
  
 Para remover uma tarefa de um plano, selecione a tarefa na superfície do designer e pressione a tecla **DELETE** ou clique com o botão direito do mouse e clique em **Excluir**.  
  
 Para especificar links de precedência entre duas tarefas, primeiro arraste as tarefas para a superfície de design e então clique na tarefa que ocorre primeiro (a tarefa precedente), e arraste a seta até a tarefa dependente. Quando foi estabelecido um link de precedência, o designer exibe uma seta vinculando as duas tarefas, com a tarefa precedente apontando para a tarefa dependente. Por padrão, quando um link é estabelecido pela primeira vez, a restrição do link é definida de modo que a tarefa dependente só execute se o resultado da tarefa precedente for **Êxito**.  
  
 Para alterar as propriedades de um link de precedência, clique duas vezes no link para iniciar o **Editor de Restrição de Precedência**. Isso fornece muitas opções para especificar as condições lógicas que determinam se a tarefa dependente será executada. Por exemplo, o **Resultado da execução** pode ser definido como **Falha**, caso a tarefa dependente somente execute se a tarefa precedente falhar. A alteração da propriedade do resultado da execução de um link para **Êxito**, **Falha** ou **Conclusão** também pode ser feita clicando com o botão direito do mouse no link e selecionando do menu de contexto.  
  
 Para especificar ramificação de tarefa, primeiro crie links de precedência entre duas tarefas. Então, coloque outra tarefa dependente na superfície de design que executa quando ocorre um resultado diferente da primeira tarefa dependente. Clique na tarefa de precedência e arraste a segunda seta da tarefa de precedência para a tarefa dependente. Para alterar o resultado de execução (**Êxito**, **Falha**, **Conclusão**) que faz com que uma tarefa dependente execute, clique duas vezes na seta do link e altere o campo **Resultado de execução** . Alternativamente, clique com o botão direito do mouse no link e selecione o valor de resultado de execução desejado no menu de atalho.  
  
 Para especificar paralelismo de tarefa, vincule duas ou mais tarefas dependentes a uma única tarefa precedente. Altere as propriedades dos links de precedência de modo que os links que apontam para tarefas dependentes que executam em paralelo tenham o mesmo valor em seus campos de resultado de execução.  
  
## <a name="additional-features-available-from-the-shortcut-menu"></a>Recursos adicionais disponíveis no menu de atalho  
 Para ver opções adicionais, selecione uma ou mais tarefas na superfície de design e, então, clique com o botão direito do mouse para abrir o menu de atalho. Além das opções comuns **Cortar**, **Copiar**, **Colar**, **Excluir** e **Selecionar Tudo**, para algumas tarefas estão disponíveis as seguintes opções especiais.  
  
 **Adicionar Anotação**  
 Adiciona uma nota descritiva à superfície de design.  
  
 **Editar**  
 Abre a caixa de diálogo de propriedade para a tarefa.  
  
 **Disable**  
 Torna a tarefa temporariamente indisponível.  
  
 **Habilitar**  
 Restaura uma tarefa desabilitada.  
  
 **Grupo**  
 Cria um grupo que contém uma ou mais tarefas.  
  
 **Desagrupar**  
 Remove tarefas de um grupo.  
  
 **Dimensionamento automático**  
 Define o tamanho de cada tarefa como o tamanho ótimo para aquela tarefa.  
  
 **Recolher**  
 Oculta as tarefas dentro de um grupo.  
  
 **Expandir**  
 Mostra as tarefas em um grupo que anteriormente estava oculto usando **Recolher**.  
  
 **Zoom**  
 Altera o tamanho das tarefas na superfície de design  
  
## <a name="see-also"></a>Consulte Também  
 [Planos de manutenção](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Criar um Plano de Manutenção](../../relational-databases/maintenance-plans/create-a-maintenance-plan.md)  
  
  
