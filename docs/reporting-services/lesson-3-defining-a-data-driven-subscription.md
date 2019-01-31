---
title: 'Lição 3: Definindo uma assinatura controlada por dados | Microsoft Docs'
ms.date: 05/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 89197b9b-7502-4fe2-bea3-ed7943eebf3b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4de4f510bcb584e0ec409f89eaba8c13ba6d8c6e
ms.sourcegitcommit: a192814756570bcbce3b1dbbb05acb24a79d1530
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54457649"
---
# <a name="lesson-3-defining-a-data-driven-subscription"></a>Lição 3: Definindo uma assinatura controlada por dados
Nesta lição do tutorial do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] , você usa as páginas da assinatura controlada por dados dos portais da Web do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para se conectar a uma fonte de dados de assinatura, criar uma consulta que recupera dados de assinatura e mapear o conjunto de resultados para opções de relatório e entrega.  
  
> [!NOTE]  
> Antes de começar, verifique se o serviço **[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent** está em execução. Se não estiver, não será possível salvar a assinatura.  Um método de verificação é abrir o [Gerenciador de Configuração do SQL Server](../relational-databases/sql-server-configuration-manager.md).
Esta lição pressupõe que você concluiu a Lição 1 e Lição 2, e que a fonte de dados de relatório usa credenciais armazenadas.  Para obter mais informações, veja [Lição 2: Modificar as propriedades de fonte de dados de relatório](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md)  
  
## <a name="bkmk_startwizard"></a>Iniciar o Assistente de Assinatura Controlada por Dados  
  
1.  No portal da Web do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] , clique em **Início**e navegue até a pasta que contém o relatório **Pedidos de Vendas** .  
  
2.  No menu de contexto ![ssrs_tutorial_datadriven_reportmenu](../reporting-services/media/ssrs-tutorial-datadriven-reportmenu.png) do relatório, clique em **Gerenciar**e clique em **Assinaturas** no painel esquerdo.  
  
3.  Clique em **+ Nova Assinatura**. Se este botão não estiver visível, você não tem permissões do Gerenciador de Conteúdo. 
  
## <a name="define-a-description"></a>Definir uma descrição  
1.  Digite **Entrega de ordem de venda** na descrição.

## <a name="type"></a>Digite
1.  Clique em **Assinatura controlada por dados**.  

## <a name="schedule"></a>Agenda
1. Na seção de agendamento, clique em **Agendamento específico do relatório**.
2. Clique em **Editar agendamento**.
3.  Em **Detalhes do Agendamento**, clique em **Uma vez**.  
4.  Especifique uma hora de início que esteja alguns minutos adiantados da hora atual.  
5.  Clique em **Aplicar**.

## <a name="destination"></a>Destino  
1.  Na seção Destino, selecione **Compartilhamento de Arquivos do Windows** como o método de entrega.  

## <a name="dataset"></a>Dataset
1. Clique em **Editar Conjunto de Dados**.
2. Selecione **Uma fonte de dados personalizada**.
3. Selecione **Microsoft SQL Server** como o tipo de **Conexão** da fonte de dados.
4. Na Cadeia de conexão, digite a cadeia de conexão a seguir. *Assinantes* são o banco de dados que você criou na lição 1. 
  
    ```  
    data source=localhost; initial catalog=Subscribers
    ```
    
## <a name="credentials"></a>Credenciais
1. Selecione **Usando as seguintes credenciais**.
2. Selecione **Nome de usuário e senha do Windows**.
3.  Em **Nome de Usuário** e **Senha**, digite seu nome de usuário de domínio e senha. Inclua a conta de domínio e de usuário ao especificar **Nome de Usuário**.

> [!NOTE]  
> As credenciais usadas para a conexão com uma fonte de dados de assinante não são retransmitidas para o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. Se você modificar a assinatura mais tarde, deverá digitar novamente a senha usada para a conexão com a fonte de dados.

## <a name="query"></a>Consulta      
1.  Na caixa de consulta, digite a seguinte consulta:  
  
    ```sql
    Select * from OrderInfo  
    ```  
  
2.  Especifique um tempo limite de 30 segundos.  
  
3.  Clique em **Validar consulta**e em **Aplicar**.

## <a name="delivery-options"></a>Opções de entrega
Preencha os seguintes valores:

Parâmetro  |Origem do valor  | Valor/campo  
---------|---------|---------
**Nome do arquivo**     |Obter valor do conjunto de dados | Order     
**Caminho**     | Inserir valor  | Em Valor, digite o nome de um compartilhamento de arquivos públicos para os quais você tem permissões de gravação (por exemplo, `\\mycomputer\public\myreports`). 
**Formato de renderização** | Obter valor do conjunto de dados | Formato
**Modo de gravação**| Inserir valor| Incremento automático    
**Extensão do arquivo** |Inserir valor |True
**Nome de Usuário** | Inserir valor | Digite sua conta de usuário de domínio. Insira-o neste formato: \<domain>\\\<account>. A conta de usuário precisa ter permissões para o caminho configurado. 
**Senha** | Inserir valor | Digite sua senha

## <a name="report-parameters"></a>Parâmetros de relatório
 1. No campo **OrderNumber** , selecione **Obter valor do conjunto de dados**. Em Valor, selecione **Pedido**. 
 2. Clique em **Criar Assinatura**.
   
## <a name="next-steps"></a>Next Steps  
Quando a assinatura é executada, quatro arquivos de relatórios são entregues no compartilhamento de arquivos especificado, um para cada pedido na fonte de dados *Assinantes* . Cada entrega deve ser exclusiva em termos de dados (os dados devem ser específicos do pedido), formato de renderização e formato de arquivo. Você pode abrir cada relatório da pasta compartilhada para verificar se cada versão está personalizada com base nas opções de assinatura definidas.  
  
![Lista de arquivos criados pela assinatura](../reporting-services/media/ssrs-tutorial-datadriven-subscription-filelist.gif "Lista de arquivos criados pela assinatura")  
  
A página de assinatura no portal da Web conterá a data da **Última Execução** e o **Status** da assinatura. 
**Observação:** Atualize a página depois que a assinatura for executada para consultar as informações atualizadas.  
    
![Resultados da assinatura no Gerenciador de Relatórios](../reporting-services/media/ssrs-tutorial-datadriven-subscription-status-reportmanager.png "Resultados da assinatura no Gerenciador de Relatórios")  
  
Esta etapa conclui o tutorial “Definir uma assinatura controlada por dados”.   
  
## <a name="see-also"></a>Consulte Também  
[Assinaturas e entrega &#40;Reporting Services&#41;](../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)  
[Assinaturas controladas por dados](../reporting-services/subscriptions/data-driven-subscriptions.md)  
[Criar, modificar e excluir assinaturas controladas por dados](../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)  
[Usar uma fonte de dados externa para obter dados de assinante &#40;Assinatura controlada por dados&#41;](../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)  
  
  
  

