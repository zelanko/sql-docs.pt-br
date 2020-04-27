---
title: Configurar o Data Warehouse de Gerenciamento (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.dc.datacollection.wizard_finish.f1
- sql12.swb.dc.datacollection.wizard_maploginuser.f1
- sql12.swb.dc.datacollection.wizard_welcome.f1
- sql12.swb.dc.datacollection.wizard_choosemdw.f1
- sql12.swb.dc.datacollection.wizard_completecfg.f1
- sql12.swb.dc.datacollection.wizard_config.f1
- sql12.swb.dc.datacollection.wizard_createmdw.f1
helpviewer_keywords:
- data warehouse [SQL Server], multiple instances
- data warehouse [SQL Server], configuring
- Configure Management Data Warehouse Wizard
- management data warehouse, configuring
ms.assetid: 23a584f3-c5e1-414c-9afe-73cd7efbda4b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a29a8b9adda07015a7f6fec953db42748a1e752e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62918813"
---
# <a name="configure-the-management-data-warehouse-sql-server-management-studio"></a>Configurar o Data Warehouse de Gerenciamento (SQL Server Management Studio)
  Este tópico descreve como configurar o data warehouse de gerenciamento para oferecer suporte de armazenamento de dados em uma ou várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usam o coletor de dados. Essas instâncias podem estar no mesmo servidor ou em servidores diferentes. Este tópico também fornece descrições da interface do usuário para a caixa de diálogo [Assistente para Configurar Data Warehouse de Gerenciamento](#Wizard) . Para obter informações sobre como configurar um coletor de dados, consulte [Configure Properties of a Data Collector](configure-properties-of-a-data-collector.md).  
  
> [!NOTE]  
>  Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent estiver configurado para ser executado usando uma das contas de serviço do Sistema (Sistema Local, Serviço de Rede ou Serviço Local) e o data warehouse de gerenciamento for criado em uma instância diferente do coletor de dados, você deverá configurar os conjuntos de coleta para usar um proxy para carregar dados no data warehouse de gerenciamento.  
  
### <a name="configure-the-management-data-warehouse-on-a-single-instance-or-multiple-instances-of-ssnoversion"></a>Configurar o data warehouse de gerenciamento em uma ou várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  Verifique se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent está em execução.  
  
2.  No Pesquisador de Objetos, expanda o nó **Gerenciamento** .  
  
3.  Clique com o botão direito do mouse em **Coleta de Dados**, expanda **Tarefas**e clique em **Configurar Data Warehouse de Gerenciamento**.  
  
4.  Use o [Assistente para Configurar Data Warehouse de Gerenciamento](#Wizard) para criar um data warehouse de gerenciamento, configurar logons, habilitar a coleta de dados e iniciar os **Conjuntos de Coleta de Dados do Sistema**.  
  
     Para configurar várias instâncias, continue com a etapa 5.  
  
    > [!NOTE]  
    >  O uso de proxies é considerado uma prática recomendada em implantações em que o coletor de dados está instalado em várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usam o mesmo data warehouse de gerenciamento.  
  
5.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] em outra instância e proceda de uma das seguintes maneiras:  
  
    -   Use o Assistente para Configurar Data Warehouse de Gerenciamento para configurar a coleta de dados para o data warehouse de gerenciamento existente.  
  
    -   Clique com o botão direito do mouse em **Coleta de Dados**e clique em **Propriedades**. Na guia **Geral** , especifique o data warehouse de gerenciamento existente e o servidor no qual ele está instalado.  
  
6.  Repita a etapa 5 até que todas as instâncias do banco de dados que usam o coletor de dados sejam configuradas para carregar os dados para o data warehouse de gerenciamento compartilhado.  
  
####  <a name="configure-management-data-warehouse-wizard"></a><a name="Wizard"></a> Configurar o Assistente de Data Warehouse de Gerenciamento  
 **Página de boas-vindas**  
  
 A página Bem-vindo é a página inicial do Assistente para Configurar Coleta de Dados. A exibição dessa página é opcional.  
  
 **Não mostrar essa página inicial novamente.**  
 Selecione para omitir esta página na próxima vez em que você iniciar o Assistente para Configurar Coleta de Dados.  
  
 **Página Armazenamento do Assistente para Configurar Data Warehouse de Gerenciamento**  
  
 Use esta página para selecionar um servidor de banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o data warehouse de gerenciamento. O data warehouse de gerenciamento é um banco de dados relacional que armazenará dados coletados.  
  
> [!NOTE]  
>  Você deve ter o nível apropriado de permissões para criar o data warehouse de gerenciamento no servidor. Para obter mais informações, consulte [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql). Você também deve ter o nível apropriado de permissões para criar logons para funções de data warehouse de gerenciamento.  
  
 **Nome do servidor**  
 Especifica o nome do servidor que hospedará o data warehouse de gerenciamento.  
  
 Ao configurar um data warehouse de gerenciamento, **Nome do servidor** será sempre o nome do servidor local e não será possível alterá-lo.  
  
 **Nome do banco de dados**  
 Especifica o banco de dados relacional que armazenará os dados coletados. Selecione na lista um banco de dados existente ou clique em **Novo** para criar um novo banco de dados usando a caixa de diálogo **Novo Banco de Dados** .  
  
 O opção **Novo** só estará disponível durante a configuração de um conjunto de coleta de dados.  
  
 **Página Mapear Logons e Usuários**  
  
 Use esta página para mapear logons para funções de usuário de banco de dados no data warehouse de gerenciamento.  
  
 **Usuários mapeados para este logon**  
 Exibe os logons existentes no servidor que hospedará o data warehouse de gerenciamento. Cada linha contém uma caixa de seleção **Mapear** editável, um nome de **Logon** e um **Tipo** de logon.  
  
 Especifique um logon marcando a caixa de seleção **Mapear** para o logon.  
  
 **Associação à função de banco de dados para:** *\<nome do data warehouse>*  
 Selecione a função do data warehouse de gerenciamento para o qual o logon está mapeado marcando a caixa de seleção em uma ou mais da opções a seguir:  
  
-   **mdw_admin**  
  
-   **mdw_reader**  
  
-   **mdw_writer**  
  
 **Novo Logon**  
 Abra a caixa de diálogo **Logon - Novo** e crie um novo logon para o data warehouse de gerenciamento.  
  
 **Página Concluir o Assistente**  
  
 Use esta página para verificar e concluir a configuração de coleta de dados. A árvore exibida na janela de visualização mostra quais configurações serão aplicadas, além de quais ações serão executadas quando você clicar em **Concluir**.  
  
 **Página Progresso do Assistente para Configurar Coleta de Dados**  
  
 Use esta página para exibir os resultados de cada etapa de configuração.  
  
 **Detalhes**  
 Exibe cada etapa de configuração como uma linha na grade **Detalhes** . Cada linha contém uma coluna **Ação** que descreve a etapa e uma coluna **Status** que indica o sucesso ou a falha da etapa. Se houver um erro, será exibida uma mensagem na coluna **Mensagem** .  
  
 **Parar**  
 Pare o processamento do assistente.  
  
 **Report**  
 Exiba um relatório da configuração de coleta de dados. São fornecidas as seguintes opções de relatório:  
  
-   Exibir Relatório  
  
-   Salvar Relatório no Arquivo  
  
-   Copiar Relatório na Área de Transferência  
  
-   Enviar Relatório como Email  
  
 **Fechar**  
 Feche o assistente.  
  
## <a name="see-also"></a>Consulte Também  
 [sp_syscollector_enable_collector &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql)   
 [sp_syscollector_disable_collector &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql)   
 [Coleta de Dados](data-collection.md)   
 [Gerenciar coleta de dados](manage-data-collection.md)  
  
  
