---
title: Exibir ou alterar agendas de conjuntos de coleta (SQL Server Management Studio) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.dc.collectionsetprop.uploads.f1
- sql13.swb.dc.collectionsetprop.description.f1
- sql13.swb.dc.collectionsetprop.general.f1
helpviewer_keywords:
- collection sets [SQL Server], changing schedules
- schedules [SQL Server], changing collection set
- collection sets [SQL Server], viewing schedules
- schedules [SQL Server], viewing collection set
ms.assetid: 26336c98-78c5-414f-8d6a-574fc3af60c4
caps.latest.revision: "26"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1ce50a767b5d704a889de0aaf96a74c0196f1587
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="view-or-change-collection-set-schedules-sql-server-management-studio"></a>Exibir ou alterar agendas de conjuntos de coleta (SQL Server Management Studio)
  É possível exibir ou alterar agendas de conjuntos de coleta usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 O modo de coleta, armazenado em cache ou não, determina como você pode fazer alterações em uma agenda. O modo cache usa agendas separadas para coleção e carregamento. O modo não cache usa a mesma agenda para coleta e carregamento. O tipo de modo de coleta de cada um dos conjuntos de coleta de Dados do Sistema é o seguinte:  
  
-   **Uso do Disco** usa o modo de coleta não cache.  
  
-   **Estatísticas de Consulta** usa o modo cache de coleção.  
  
-   **Atividade do Servidor** usa o modo cache de coleção.  
  
### <a name="to-view-collection-set-schedules"></a>Para exibir agendas de conjuntos de coleta  
  
1.  No Pesquisador de Objetos, expanda o nó **Gerenciamento** , expanda **Coleta de Dados**e, em seguida, **Conjuntos de Coleta de Dados do Sistema**.  
  
2.  Clique com o botão direito do mouse no nome do conjunto de coleta e clique em **Propriedades** para abrir a caixa de diálogo [Propriedades do Conjunto de Coleta de Dados](#CollectionSet) .  
  
### <a name="to-change-the-schedules-for-a-cached-mode-collection-set"></a>Para alterar as agendas para um conjunto de coleta no modo cache  
  
1.  No Pesquisador de Objetos, expanda o nó **Gerenciamento** , expanda **Coleta de Dados**e, em seguida, **Conjuntos de Coleta de Dados do Sistema**.  
  
2.  Clique com o botão direito do mouse em um conjunto de coleta que usa o modo cache, como **Estatísticas de Consulta**, e clique em **Propriedades** para abrir a caixa de diálogo [Propriedades do Conjunto de Coleta de Dados](#CollectionSet) .  
  
3.  Você pode alterar a frequência da coleta na página **Geral** . Para fazer isso, siga estas etapas:  
  
    1.  No painel de detalhes, clique duas vezes no número exibido para a coluna **Frequência de Coleta (s)** na tabela **Itens da coleta** .  
  
    2.  Para aumentar ou reduzir a frequência da coleta, digite um número inferior ou superior e pressione ENTER para armazenar o novo valor.  
  
4.  Para alterar a agenda de carregamento existente para o conjunto de coleta, siga estas etapas:  
  
    1.  Clique na página **Carregamentos** .  
  
    2.  No painel de detalhes, clique em **Escolher**.  
  
         A caixa de diálogo **Escolher Agenda para o Trabalho** é aberta. As agendas disponíveis aparecem como uma tabela.  
  
    3.  Clique na linha que contém a agenda desejada. Por exemplo, para alterar o agendamento a cada 5 minutos, clique na linha em que o nome de agendamento é **CollectorSchedule_Every_5min.**  
  
        > [!NOTE]  
        >  É possível exibir e editar as propriedades da agenda selecionada clicando em **Propriedades** para abrir a caixa de diálogo **Propriedades da Agenda de Trabalho** da agenda. Você pode usar essa caixa de diálogo para alterar as informações da agenda, como a frequência.  
        >   
        >  Como alternativa à modificação de uma agenda existente, você pode criar uma nova agenda de carregamento clicando em **Nova** na página **Carregamentos** . Essa ação abre a caixa de diálogo **Nova Agenda de Trabalho** que pode ser usada para criar uma agenda personalizada.  
  
    4.  Ao concluir a configuração da agenda, clique em **OK**.  
  
         As alteração feitas aparecem na página **Carregamentos** .  
  
5.  Clique em **OK** para salvar as alterações na frequência da coleta e na agenda de carregamento e para fechar a caixa de diálogo **Propriedades do Conjunto de Coleta de Dados** .  
  
### <a name="to-change-the-schedule-for-a-non-cached-mode-collection-set"></a>Para alterar a agenda de um conjunto de coleta no modo não cache  
  
1.  No Pesquisador de Objetos, expanda o nó **Gerenciamento** , expanda **Coleta de Dados**e, em seguida, **Conjuntos de Coleta de Dados do Sistema**.  
  
2.  Clique com o botão direito do mouse em um conjunto de coleta que usa o modo não cache, como **Uso do Disco**, e clique em **Propriedades** para abrir a caixa de diálogo [Propriedades do Conjunto de Coleta de Dados](#CollectionSet) .  
  
     A caixa de diálogo **Propriedades do Conjunto de Coleta de Dados** exibe uma exibição paginada das propriedades do conjunto de coleta.  
  
3.  Para alterar a agenda para o conjunto de coleta, clique em **Escolher**.  
  
     A caixa de diálogo **Escolher Agenda para o Trabalho** é aberta. As agendas disponíveis são exibidas como uma tabela.  
  
4.  Clique na linha que contém a agenda desejada. Por exemplo, para alterar o agendamento a cada 5 minutos, clique na linha em que o nome de agendamento é **CollectorSchedule_Every_5min**.  
  
    > [!NOTE]  
    >  É possível exibir e editar as propriedades da agenda selecionada clicando em **Propriedades** para abrir a caixa de diálogo **Propriedades da Agenda de Trabalho** da agenda. Você pode usar essa caixa de diálogo para alterar as informações da agenda, como a frequência.  
    >   
    >  Como alternativa à modificação de uma agenda existente, você pode criar uma nova agenda de carregamento e de coleta clicando em **Nova** na página **Geral** . Essa ação abre a caixa de diálogo **Nova Agenda de Trabalho** .  
  
5.  Ao concluir a configuração da agenda, clique em **OK**.  
  
6.  Clique em **OK** para salvar as alterações e fechar a caixa de diálogo **Propriedades do Conjunto de Coleta de Dados** .  
  
####  <a name="CollectionSet"></a> Caixa de diálogo Propriedades de Conjunto de Coleta de Dados  
 **Página Geral**  
  
 Use esta página para configurar o modo como os dados devem ser coletados e carregados, para configurar cronogramas e configurar períodos de retenção de dados no data warehouse de gerenciamento. Esta página fornece também informações sobre conjuntos de coleta, como tipos de coletor e frequências de coleta, além de parâmetros de entrada usados em um conjunto de coleta.  
  
 **Nome**  
 Exibe o nome do conjunto de coleta ao qual a página se refere.  
  
 **Coleta e carregamento de dados**  
 Especifica de que modo os dados são coletados e carregados no data warehouse de gerenciamento. Clique em uma das opções a seguir.  
  
|||  
|-|-|  
|**Sem-cache. Coleta e upload de dados na mesma agenda.**|Quando selecionada, especifique uma destas opções:<br /><br /> **Agenda**. Os dados são coletados e carregados de acordo com a agenda. Clique em **Escolher** para selecionar em uma lista predefinida de agendas ou clique em **Novo** para criar uma nova agenda.<br /><br /> **Sob demanda**. Os dados são coletados e carregados sob demanda.|  
|**Em cache. Coletar e armazenar os dados em cache em um conjunto de frequências de coleta. Carregar os dados armazenados em cache em uma agenda separada.**|Colete e armazene os dados em cache para uma frequência de coleta especificada. Carregue os dados coletados em uma agenda separada.|  
  
 **Itens da coleta**  
 Exibe os itens de coleção no conjunto de coleta. São fornecidas as informações a seguir para cada item de coleta:  
  
-   **Nome**  
  
-   **Tipo de Coletor**  
  
-   **Frequência de Coleta** (segundos). Este campo pode ser editado se **Coleta e carregamento de dados** for configurado como em cache. Clique duas vezes nesta célula para definir a frequência de coleta.  
  
 **Parâmetros de entrada**  
 Exibe os parâmetros de entrada usados no conjunto de coleta.  
  
 **Executar como**  
 Especifica a conta usada para executar o conjunto de coleta. Por padrão, essa é a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Conta de Serviço do Agent. Se contas proxy estiverem definidas, a lista incluirá os nomes das contas proxy disponíveis.  
  
 **Definir por quanto tempo serão retidos dados coletados no data warehouse de gerenciamento.**  
 Especifica por quanto tempo os dados coletados serão retidos. Clique em uma das opções a seguir.  
  
|||  
|-|-|  
|**Reter dados para**|Esta opção fica selecionada por padrão e o período de retenção padrão é de 14 dias.|  
|**Reter dados indefinidamente**|Não há nenhum limite no período de tempo em que os dados são retidos.|  
  
 **Página Carregamentos**  
  
 Use esta página para configurar a agenda de carregamento de dados coletados por esse conjunto de coleta.  
  
> [!NOTE]  
>  Esta guia só estará habilitada se a opção **Em cache** for configurada para **Coleta e carregamento de dados**.  
  
 **Servidor**  
 Exibe o nome do servidor que hospeda o data warehouse de gerenciamento. Para obter mais informações, veja [Configurar o data warehouse de gerenciamento &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md).  
  
 **Data warehouse de gerenciamento**  
 Exibe o nome do data warehouse de gerenciamento. Para obter mais informações, veja [Configurar o data warehouse de gerenciamento &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md).  
  
 **Último carregamento**  
 Exibe informações de data e hora do último carregamento feito para o conjunto de coleta.  
  
 **Agenda de carregamento**  
 Especifica a agenda de carregamento do conjunto de coleta. E estiver habilitada, clique em **Escolher** para selecionar em uma lista predefinida de agendas ou clique em **Novo** para criar uma agenda nova.  
  
 **Página Descrição**  
  
 Use esta página para exibir uma descrição do conjunto de coleta ao qual essa página de propriedades se refere.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar coleta de dados](../../relational-databases/data-collection/manage-data-collection.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)  
  
  
