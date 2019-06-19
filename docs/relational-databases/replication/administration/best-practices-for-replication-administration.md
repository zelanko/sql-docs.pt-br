---
title: Práticas recomendadas para administração de replicação | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- administering replication, best practices
- replication [SQL Server], administering
ms.assetid: 850e8a87-b34c-4934-afb5-a1104f118ba8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: aaf073341709e2c612f89d70f566f3b2dd09283d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62665371"
---
# <a name="best-practices-for-replication-administration"></a>Práticas recomendadas para administração de replicação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Depois de configurar a replicação, é importante entender como administrar uma topologia de replicação. Este tópico fornece diretrizes básicas de práticas recomendadas em várias áreas com links para mais informações para cada área. Além das seguintes diretrizes de práticas recomendadas apresentadas neste tópico, considere a leitura do tópico de perguntas frequentes para se familiarizar com as questões e problemas mais comuns: [Perguntas frequentes para os administradores de replicação](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md).  
  
 É útil dividir as diretrizes de prática recomendada em duas áreas:  
  
-   As informações seguintes cobrem as práticas recomendadas que devem ser implementadas para todas as topologias de replicação:  
  
    -   Desenvolva e teste uma estratégia de backup e restauração.  
  
    -   Faça o script da topologia de replicação.  
  
    -   Crie limites e alertas  
  
    -   Monitore a topologia de replicação.  
  
    -   Estabeleça linhas de base de desempenho e ajuste a replicação, se necessário.  
  
-   As informações a seguir cobrem as práticas recomendadas que devem ser consideradas, mas podem não ser requeridas para a sua topologia:  
  
    -   Valide os dados periodicamente.  
  
    -   Ajuste parâmetros de agente por perfis.  
  
    -   Ajuste a publicação e os períodos de retenção da distribuição.  
  
    -   Entenda como alterar as propriedades de artigo e de publicação se os requisitos do aplicativo alterarem.  
  
    -   Entenda como fazer alterações de esquema altera se os requisitos do aplicativo alterarem.  
  
## <a name="develop-and-test-a-backup-and-restore-strategy"></a>Desenvolva e teste uma estratégia de backup e restauração  
 Todos os bancos de dados devem ter backups feitos regularmente e a habilidade de restaurar esses backups deve ser testada periodicamente; bancos de dados replicados não são diferentes. Os bancos de dados seguintes deveriam ter seu backup feito regularmente:  
  
-   Banco de dados de publicação  
  
-   Banco de dados de distribuição  
  
-   Banco de dados de assinatura  
  
-   O banco de dados**msdb** e o banco de dados **mestre** no Publicador, Distribuidor e todos os Assinantes  
  
 Bancos de dados replicados requerem atenção especial em relação a backup e restauração de dados. Para obter mais informações, veja [Fazer backup e restaurar bancos de dados replicados](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md).  
  
## <a name="script-the-replication-topology"></a>Faça o script da topologia de replicação  
 Todos os componentes de replicação em uma topologia devem ser incluídos no script como parte de um plano de recuperação de desastre  e os scripts também podem ser usados para automatizar tarefas repetitivas. Um script contém os procedimentos armazenados do sistema [!INCLUDE[tsql](../../../includes/tsql-md.md)] necessários para implementar o(s) componente(s) de replicação que tiveram seus scripts feitos, como uma publicação ou assinatura. Os scripts podem ser criados em um assistente (como o Assistente para Nova Publicação) ou no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] depois de você criar um componente. É possível exibir, modificar e executar o script por meio do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou do **sqlcmd**. Os scripts podem ser armazenados com arquivos de backup para serem usados no caso de uma topologia de replicação precisar ser reconfigurada. Para obter mais informações, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
 Um componente deve ter seu script refeito se qualquer alteração na propriedade for realizada. Se você usar procedimentos armazenados com replicação transacional, uma cópia de cada procedimento deve ser armazenada com os scripts; a cópia deve ser atualizada se o procedimento for alterado (os procedimentos são normalmente alterados devido a mudanças no esquema ou nos requisitos de aplicativo). Para mais informações sobre procedimentos personalizados, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
## <a name="establish-performance-baselines-and-tune-replication-if-necessary"></a>Estabeleça linhas de base de desempenho e ajuste a replicação se necessário  
 Antes de configurar a replicação, recomenda-se a familiarização com os fatores que afetam o desempenho de replicação:  
  
-   Servidor e hardware de rede  
  
-   Design do banco de dados  
  
-   Configuração do Distribuidor  
  
-   Design e opções de publicação  
  
-   Design e uso de filtro  
  
-   Opções de Assinatura  
  
-   Opções de instantâneo  
  
-   Parâmetros de agente  
  
-   Manutenção  
  
 Após a replicação ser configurada, é recomendável desenvolver uma linha de base de desempenho, que permitirá determinar como a replicação se comporta com uma carga de trabalho típica de seus aplicativos e de sua topologia. Use o Replication Monitor e Monitor do Sistema para determinar os números típicos para as seguintes cinco dimensões de desempenho de replicação:  
  
-   Latência: a quantidade de tempo necessária para uma alteração de dados ser propagada entre nós em uma topologia de replicação.  
  
-   Taxa de Transferência: a quantidade de atividades de replicação (medida em comandos entregues em um período de tempo) que o sistema pode sustentar com o tempo.  
  
-   Simultaneidade: o número de processos de replicação que podem funcionar simultaneamente em um sistema.  
  
-   Duração de sincronização: quanto tempo uma determinada sincronização precisa para ser completada.  
  
-   Consumo de Recursos: hardware e recursos de rede usados como resultado do processamento de replicação.  
  
 A latência e a taxa de transferência são mais relevantes para a replicação transacional, porque os sistemas construídos em uma replicação transacional geralmente requerem baixa latência e alta taxa de transferência. Simultaneidade e duração de sincronização são mais relevantes para a replicação de mesclagem porque os sistemas construídos em replicação de mesclagem frequentemente têm um grande número de Assinantes, e um Publicador pode ter um número significante de sincronizações simultâneas com esses Assinantes.  
  
 Depois de estabelecer os números de linha de base, defina os limites no Replication Monitor. Para obter mais informações, consulte [Definir os limites e avisos no Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md) e [Usar alertas para eventos do agente de replicação](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md). Se encontrar um problema de desempenho, recomenda-se ler as sugestões nos tópicos de melhora de desempenho listados anteriormente, e aplicar as alterações em áreas que afetem os problemas encontrados.  
  
## <a name="create-thresholds-and-alerts"></a>Crie limites e alertas  
 O Replication Monitor permite definir vários limites relacionados a status e desempenho. É recomendável definir os limites apropriados para a sua topologia; se um limite for alcançado, um aviso é exibido e, opcionalmente, um alerta pode ser enviado para uma conta de email, um pager ou outro dispositivo. Para obter mais informações, consulte [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
 Além dos alertas que podem ser associados com a monitoração de limites, a replicação fornece uma série de alertas pré-definidos que respondem a ações do agente de replicação. Esses alertas podem ser usados por um administrador para ficar informado sobre o estado da topologia de replicação. É recomendável a leitura do tópico que descreve os alertas e o uso de qualquer um que se encaixe em suas necessidades administrativas (também é possível criar alertas adicionais, se necessário). Para obter mais informações, consulte [Usar alertas para eventos do agente de replicação](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
## <a name="monitor-the-replication-topology"></a>Monitore a topologia de replicação  
 Depois que a topologia de replicação estiver funcionando e os limites e alertas tiverem sido configurados, recomenda-se monitorar regularmente a replicação. Monitorar uma topologia de replicação é um aspecto importante na implantação da replicação. Já que a atividade de replicação é distribuída, é essencial controlar sua atividade e o status em todos os computadores envolvidos na replicação. As seguintes ferramentas podem ser usadas para monitorar a replicação:  
  
-   O Replication Monitor é a ferramenta mais importante para a monitoração da replicação, permitindo monitorar a saúde geral de uma topologia de replicação. Para obter mais informações, consulte [Monitoring Replication](../../../relational-databases/replication/monitor/monitoring-replication.md).  
  
-   O[!INCLUDE[tsql](../../../includes/tsql-md.md)] e o RMO (Replication Management Objects) fornecem interfaces para monitorar replicação. Para obter mais informações, consulte [Monitoring Replication](../../../relational-databases/replication/monitor/monitoring-replication.md).  
  
-   O Monitor do Sistema também pode ser útil para monitorar o desempenho da replicação. Para obter mais informações, consulte [Monitoring Replication with System Monitor](../../../relational-databases/replication/monitor/monitoring-replication-with-system-monitor.md).  
  
## <a name="validate-data-periodically"></a>Valide os dados periodicamente  
 A validação não é requerida pela replicação, mas é recomendada a execução da validação periódica para a replicação transacional e a replicação de mesclagem. A validação permite verificar que os dados no Assinante correspondem aos dados no Publicador. Uma validação bem-sucedida indica que naquele point-in-time todas as alterações do Publicador foram replicadas no Assinante (e do Assinante no Publicador, se houver suporte para atualizações no Assinante) e que os dois bancos de dados estão em sincronia.  
  
 É recomendado que a validação seja executada de acordo com a agenda de backup do banco de dados de publicação. Por exemplo, se o banco de dados de publicação tem um backup completo uma vez por semana, a validação poderia ser executada uma vez por semana após o backup ser completado. Para obter mais informações, consulte [Validar os dados replicados](../../../relational-databases/replication/validate-data-at-the-subscriber.md).  
  
## <a name="use-agent-profiles-to-change-agent-parameters-if-necessary"></a>Use perfis de agente para alterar os parâmetros de agente, se necessário  
 Os perfis de agente fornecem um método conveniente de definir parâmetros do agente de replicação. Os parâmetros podem também ser especificados na linha de comando do agente, mas é normalmente mais apropriado usar um perfil predefinido de agente ou criar um novo perfil se for necessário alterar o valor do parâmetro. Por exemplo, se estiver usando uma replicação de mesclagem e o Assinante mudar de uma conexão de banda larga para uma conexão discada, considere usar o perfil **vínculo lento** para o Agente de Mesclagem; esse perfil usa um conjunto de parâmetros que são mais adequados para vínculos de comunicações mais lentas. Para saber mais, confira [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="adjust-publication-and-distribution-retention-periods-if-necessary"></a>Ajuste a publicação e os períodos de retenção da distribuição, se necessário  
 A replicação transacional e a replicação de mesclagem usam os períodos de retenção para determinar, respectivamente, quanto tempo as transações são armazenadas no banco de dados de distribuição e com que frequência uma assinatura precisa ser sincronizada. Recomenda-se usar inicialmente os valores padrão, porém é necessário monitorar a topologia para determinar se a configuração requer ajustes. Por exemplo, no caso da replicação de mesclagem, o período de retenção da publicação (que por padrão é de 14 dias) determina quanto tempo os metadados são armazenados nas tabelas do sistema. Se as assinaturas sempre são sincronizadas a cada cinco dias, considere ajustar a configuração para um número menor, o que reduzirá os metadados e possivelmente melhorará o desempenho. Para obter mais informações, consulte [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
## <a name="understand-how-to-modify-publications-if-application-requirements-change"></a>Entenda como alterar as publicações se os requisitos do aplicativo alterarem  
 Depois de criar uma publicação, poderá ser necessário adicionar ou descartar artigos, ou alterar as propriedades da publicação e do artigo. A maioria das alterações é permitida após a criação de uma publicação, mas em alguns casos, é necessário gerar um novo instantâneo para a publicação e/ou reinicializar as assinaturas para uma publicação. Para obter mais informações, consulte [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md) e [Add Articles to and Drop Articles from Existing Publications](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md) (Adicionar e remover artigos para/de publicações existentes).  
  
## <a name="understand-how-to-make-schema-changes-if-application-requirements-change"></a>Entenda como fazer alterações de esquema se os requisitos do aplicativo alterarem.  
 Em muitos casos, são necessárias alterações de esquema depois que um aplicativo estiver em produção. Em uma topologia de replicação, essas alterações devem ser propagadas frequentemente a todos os Assinantes. A replicação oferece suporte para um amplo intervalo de alterações de esquema para objetos publicados. Ao fazer qualquer uma das seguintes alterações de esquema no objeto publicado adequado em um Publicador do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , a alteração é propagada por padrão a todos os Assinantes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 Para obter mais informações, consulte [Make Schema Changes on Publication Databases](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md) (Fazer alterações de esquema em bancos de dados de publicação).  
  
## <a name="see-also"></a>Consulte Também  
 [Perguntas Frequentes sobre Administração de Replicação](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)  
  
  
