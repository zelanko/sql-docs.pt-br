---
title: Exibir propriedades do Administrador de Recursos | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.swb.rg.properties.f1
helpviewer_keywords:
- Resource Governor, properties
ms.assetid: de3510df-f792-4a9d-80fa-f198fd36cdc8
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 2250030405a0c6bb2512e3b8446cb76e11a7080e
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72903906"
---
# <a name="view-resource-governor-properties"></a>View Resource Governor Properties
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Você pode criar ou configurar entidades do Administrador de Recursos, como pools de recursos e grupos de cargas de trabalho, usando a página de Propriedades do Administrador de Recursos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 ##  <a name="BeforeYouBegin"></a> Tópicos relacionados 
 Além de exibir as propriedades de entidades do Administrador de Recursos, você pode executar várias tarefas de configuração usando a página **Propriedades do Administrador de Recursos** . Para obter mais informações, consulte estes tópicos:  
  
-   [Habilitar Administrador de Recursos](../../relational-databases/resource-governor/enable-resource-governor.md)  
  
-   [Desabilitar Administrador de Recursos](../../relational-databases/resource-governor/disable-resource-governor.md)  
  
-   [Criar um pool de recursos](../../relational-databases/resource-governor/create-a-resource-pool.md)  
  
-   [Criar um grupo de carga de trabalho](../../relational-databases/resource-governor/create-a-workload-group.md)  
  
-   [Alterar configurações do pool de recursos](../../relational-databases/resource-governor/change-resource-pool-settings.md)  
  
-   [Alterar as configurações de grupo de carga de trabalho](../../relational-databases/resource-governor/change-workload-group-settings.md)  
  
-   [Mover um Grupo de Cargas de Trabalho](../../relational-databases/resource-governor/move-a-workload-group.md)  
  
 Quando você clicar em **OK** depois de adicionar, excluir ou mover um grupo de cargas de trabalho ou pool de recursos, a instrução ALTER RESOURCE GOVERNOR RECONFIGURE será executada.  
  
 Se a operação de criação ou reconfiguração do pool de recursos ou grupo de cargas de trabalho falhar, um resumo de uma mensagem de erro será exibido abaixo do título da página de propriedades. Para visualizar uma mensagem de erro detalhada, clique na seta para baixo na mensagem de erro.  
  
 É possível determinar se há uma configuração pendente consultando a exibição de gerenciamento dinâmico de [sys.dm_resource_governor_configuration](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql.md) para obter o status atual de is_configuration_pending.  
  
##  <a name="Permissions"></a> Permissões  
 Exibir propriedades do administrador de recursos exige a permissão VIEW SERVER STATER. As tarefas de configuração do administrador de recursos exigem a permissão CONTROL SERVER.  
  
##  <a name="ViewRGProp"></a> Página de propriedades do Administrador de Recursos  
 **Para exibir as propriedades do administrador de recursos usando a página de Propriedades do Administrador de Recursos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra o Pesquisador de Objetos e expanda recursivamente o nó **Gerenciamento** para baixo e incluindo o **Administrador de Recursos**.  
  
2.  Clique com o botão direito do mouse em **Administrador de Recursos** e clique em **Propriedades**, para abrir a página **Propriedades do Administrador de Recursos** .  
  
3.  Para obter descrições dos campos na página, consulte [Propriedades do Administrador de Recursos](#RGProp).  
  
4.  Para salvar as alterações, clique em **OK**.  

##  <a name="RGProp"></a> Resource Governor properties  
 **Nome da função de classificação**  
 Especifique a função de classificação selecionando-a na lista.  
  
 **Habilitar Administrador de Recursos**  
 Habilite ou desabilite o Administrador de Recursos selecionando ou desmarcando a caixa de seleção.  
  
 **Pools de recursos**  
 Crie ou altere a configuração do pool de recursos e do pool de recursos externo usando a grade fornecida. Essa grade é populada com informações para os pools predefinidos internos e padrão. Selecione um pool com o qual trabalhar clicando na primeira coluna na linha do pool. Para criar um novo pool de recursos, clique na linha antecedida pelo asterisco ( **&#42;** ).  
  
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
  
 Para obter mais informações, consulte [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md) e [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md).  
  
 **Grupos de cargas de trabalho para o pool de recursos**  
 Crie ou altere a configuração do grupo de carga de trabalho usando a grade fornecida. Essa grade é populada com informações para os grupos predefinidos internos e padrão. Selecione um grupo com a qual trabalhar clicando na primeira coluna na linha para o pool. Para criar um novo grupo de carga de trabalho, clique na linha antecedida pelo asterisco ( **&#42;** ).  
  
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
  
 Para obter mais informações, consulte [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md).  
  
## <a name="view-resource-governor-properties-using-transact-sql"></a>Exibir as propriedades do administrador de recursos usando Transact-SQL  
 **Exibir as propriedades do administrador de recursos usando Transact-SQL**  
  
1.  Para exibir as definições de entidades do administrador de recursos, use o [Exibições do catálogo do administrador de recursos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md).  
  
2.  Para exibir a configuração atual de entidades do administrador de recursos, use o [Exibições de gerenciamento dinâmico relacionadas ao Administrador de Recursos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md).  
  
## <a name="more-information"></a>Mais informações
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Habilitar Administrador de Recursos](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Pool de recursos do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Grupos de carga de trabalho do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Função de classificação do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-classifier-function.md)  
  
  
