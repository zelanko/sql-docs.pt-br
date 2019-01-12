---
title: Exibir propriedades do Administrador de Recursos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql12.swb.rg.properties.f1
helpviewer_keywords:
- Resource Governor, properties
ms.assetid: de3510df-f792-4a9d-80fa-f198fd36cdc8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 35d4720a8fe8b8c1b404a97e27b36896f36dd5f7
ms.sourcegitcommit: 78e32562f9c1fbf2e50d3be645941d4aa457e31f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2019
ms.locfileid: "54100791"
---
# <a name="view-resource-governor-properties"></a>View Resource Governor Properties
  Você pode criar ou configurar entidades do Administrador de Recursos, como pools de recursos e grupos de cargas de trabalho, usando a página de Propriedades do Administrador de Recursos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
1.  **Antes de começar:**  [Permissões](#Permissions)  
  
2.  **Para exibir as propriedades do administrador de recursos, usando:**  [Página de propriedades do administrador de recursos](#ViewRGProp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
 Além de exibir as propriedades de entidades do Administrador de Recursos, você pode executar várias tarefas de configuração usando a página **Propriedades do Administrador de Recursos** . Para obter mais informações, consulte estes tópicos:  
  
-   [Habilitar Administrador de Recursos](enable-resource-governor.md)  
  
-   [Desabilitar Administrador de Recursos](disable-resource-governor.md)  
  
-   [Criar um pool de recursos](create-a-resource-pool.md)  
  
-   [Criar um grupo de carga de trabalho](create-a-workload-group.md)  
  
-   [Alterar configurações do pool de recursos](change-resource-pool-settings.md)  
  
-   [Alterar as configurações de grupo de carga de trabalho](change-workload-group-settings.md)  
  
-   [Mover um Grupo de Cargas de Trabalho](move-a-workload-group.md)  
  
 Quando você clicar em **OK** depois de adicionar, excluir ou mover um grupo de cargas de trabalho ou pool de recursos, a instrução ALTER RESOURCE GOVERNOR RECONFIGURE será executada.  
  
 Se a operação de criação ou reconfiguração do pool de recursos ou grupo de cargas de trabalho falhar, um resumo de uma mensagem de erro será exibido abaixo do título da página de propriedades. Para visualizar uma mensagem de erro detalhada, clique na seta para baixo na mensagem de erro.  
  
 É possível determinar se há uma configuração pendente consultando a exibição de gerenciamento dinâmico de [sys.dm_resource_governor_configuration](/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql) para obter o status atual de is_configuration_pending.  
  
###  <a name="Permissions"></a> Permissões  
 Exibir propriedades do administrador de recursos exige a permissão VIEW SERVER STATER. As tarefas de configuração do administrador de recursos exigem a permissão CONTROL SERVER.  
  
##  <a name="ViewRGProp"></a> Exibir a página de propriedades do administrador de recursos  
 **Para exibir as propriedades do administrador de recursos usando a página de Propriedades do Administrador de Recursos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra o Pesquisador de Objetos e expanda recursivamente o nó **Gerenciamento** para baixo e incluindo o **Administrador de Recursos**.  
  
2.  Clique com o botão direito do mouse em **Administrador de Recursos** e clique em **Propriedades**, para abrir a página **Propriedades do Administrador de Recursos** .  
  
3.  Para obter descrições dos campos na página, consulte [Propriedades do Administrador de Recursos](#RGProp).  
  
4.  Para salvar as alterações, clique em **OK**.  
  
##  <a name="RGProp"></a> Propriedades do administrador de recursos  
 **Nome da função de classificação**  
 Especifique a função de classificação selecionando-a na lista.  
  
 **Habilitar Administrador de Recursos**  
 Habilite ou desabilite o Administrador de Recursos selecionando ou desmarcando a caixa de seleção.  
  
 **Pools de recursos**  
 Crie ou altere a configuração do pool de recursos usando a grade fornecida. Essa grade é populada com informações para os pools predefinidos internos e padrão. Selecione um pool com o qual trabalhar clicando na primeira coluna na linha do pool. Para criar um novo pool de recursos, clique na linha antecedida pelo asterisco (**&#42;**).  
  
 **Nome**  
 Especifique o nome do pool de recursos.  
  
 **% Mínima de CPU**  
 Especifique a média de largura de banda de CPU garantida para todas as solicitações no pool de recursos quando houver contenção de CPU. O intervalo é de 0 a 100.  
  
 **% Máxima de CPU**  
 Especifique a média máxima de largura de banda de CPU que todas as solicitações desse pool de recursos receberão quando houver contenção de CPU. O intervalo é de 0 a 100. A configuração padrão é 100.  
  
 **% Mínima de Memória**  
 Especifique a quantidade mínima de memória reservada para esse pool de recursos que não pode ser compartilhada com outros pools de recursos. O intervalo é de 0 a 100.  
  
 **% Máxima de Memória**  
 Especifique a memória total de servidor que pode ser usada através de solicitações nesse pool de recursos. O intervalo é de 0 a 100. A configuração padrão é 100.  
  
 Para obter mais informações, consulte [criar POOL de recursos &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-resource-pool-transact-sql).  
  
 **Grupos de cargas de trabalho para o pool de recursos**  
 Crie ou altere a configuração do grupo de carga de trabalho usando a grade fornecida. Essa grade é populada com informações para os grupos predefinidos internos e padrão. Selecione um grupo com a qual trabalhar clicando na primeira coluna na linha para o pool. Para criar um novo grupo de carga de trabalho, clique na linha antecedida pelo asterisco (**&#42;**).  
  
 **Nome**  
 Especifique o nome do grupo de carga de trabalho.  
  
 **Importância**  
 Especifique a importância relativa de uma solicitação no grupo de carga de trabalho. Configurações disponíveis são Baixa, Média, e Alta.  
  
 **Máximo de Solicitações**  
 Especifique o número máximo de solicitações simultâneas permitido para execução no grupo de carga de trabalho. O valor deve ser 0 ou um número inteiro positivo.  
  
 **Tempo de CPU (s)**  
 Especifique o tempo máximo de CPU que uma solicitação pode usar. O valor deve ser 0 ou um número inteiro positivo. Se 0, o tempo é ilimitado.  
  
 **% de Concessão de Memória**  
 Especifique o máximo de memória que uma única solicitação pode usar do pool. O intervalo é de 0 a 100.  
  
 **Tempo limite geral (segundo)**  
 Especifique o tempo máximo que uma consulta pode esperar para que um recurso se torne disponível antes que a consulta falhe. O valor deve ser 0 ou um número inteiro positivo.  
  
 **Grau de paralelismo**  
 Especifique o grau máximo de paralelismo (DOP) para solicitações paralelas. O intervalo é de 0 a 64.  
  
 Para obter mais informações, consulte [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-workload-group-transact-sql).  
  
## <a name="view-resource-governor-properties-by-using-transact-sql"></a>Exibir as Propriedades do Administrador de Recursos usando Transact-SQL  
 **Exibir as propriedades do administrador de recursos usando Transact-SQL**  
  
1.  Para exibir as definições de entidades do administrador de recursos, use o [Exibições do catálogo do administrador de recursos &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql).  
  
2.  Para exibir a configuração atual de entidades do administrador de recursos, use o [Exibições de gerenciamento dinâmico relacionadas ao Administrador de Recursos &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql).  
  
## <a name="see-also"></a>Consulte também  
 [Administrador de Recursos](resource-governor.md)   
 [Habilitar Administrador de Recursos](enable-resource-governor.md)   
 [Pool de recursos do Administrador de Recursos](resource-governor-resource-pool.md)   
 [Grupos de carga de trabalho do Administrador de Recursos](resource-governor-workload-group.md)   
 [Função de classificação do Administrador de Recursos](resource-governor-classifier-function.md)  
  
  
