---
title: Gerenciador de Alertas de Dados para usuários do SharePoint | Microsoft Docs
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- managing, alerts
- managing, data alerts
ms.assetid: 7b9281c8-2f8b-48f7-85d8-7a7a596e3c82
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 79bf8462483347964fc1dece4486167d44f67d1f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47668696"
---
# <a name="data-alert-manager-for-sharepoint-users"></a>Gerenciador de Alertas de Dados para Usuários do SharePoint

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)][!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../includes/ssrs-previous-versions.md)]

[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] fornece o Gerenciador de Alertas de Dados para operadores de informações do SharePoint para gerenciar os alertas de dados. Eles podem exibir informações sobre os alertas que criaram, excluir alertas, abrir definições de alertas para edição e executar alertas sob demanda. Eles podem optar por exibir os alertas para um único relatório apenas ou os alertas de todos os relatórios. A imagem a seguir mostra os recursos disponíveis para os operadores de informações no Gerenciador de Alertas de Dados.

![Recursos do Gerenciador de Alertas para usuários do SharePoint](../reporting-services/media/rs-alertmanageriw.gif "Recursos do Gerenciador de Alertas para usuários do SharePoint")  

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.

Quando um site do SharePoint é habilitado para alertas de dados, duas páginas do SharePoint, MyDataAlerts.aspx e SiteDataAlerts.aspx, são criadas e adicionadas ao site do SharePoint. MyDataAlerts.aspx é o Gerenciador de Alertas de Dados para operadores de informações do SharePoint. Os operadores de informações abrem o Gerenciador de Alertas de Dados no menu de atalho de relatórios nos quais eles criaram alertas.  

 Você também pode abrir o Gerenciador de Alertas de Dados diretamente por meio de uma URL. O seguinte mostra a sintaxe da URL:  
  
 `http://<site name>/_layouts/ReportServer/MyDataAlerts.aspx`  
  
> [!NOTE]  
>  Para poder usar os recursos de alerta do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , você deve receber permissões de um administrador. Para obter informações sobre as permissões necessárias, consulte [Alertas de dados do Reporting Services](../reporting-services/reporting-services-data-alerts.md).  
  
##  <a name="ViewingAlerts"></a> Exibir informações de alertas de dados  
 Você pode exibir uma lista dos alertas de dados que criou no Designer de Alertas de Dados. Para abrir o Gerenciador de Alertas de Dados, você clica com o botão direito do mouse em um relatório publicado em uma biblioteca do SharePoint. A imagem a seguir mostra a opção **Gerenciar Alertas de Dados** no menu de atalho de relatório.  
  
 ![Abrir o Gerenciador de Alertas no menu de contexto do relatório](../reporting-services/media/rs-openalertmanager.gif "Abrir o Gerenciador de Alertas no menu de contexto do relatório")  
  
 O Gerenciador de Alertas de Dados inclui uma tabela que lista o nome do alerta, o nome do relatório, seu nome como o criador da definição de alerta, o número de mensagens de alerta enviadas, a última vez que o alerta foi executado, a última vez que a definição do alerta foi modificada e o status da última mensagem de alerta. Se a mensagem de alerta não puder ser gerada ou enviada, a coluna de status conterá informações sobre o erro e ajudará a solucionar problemas do alerta. Para obter mais informações, consulte [Gerenciar meus alertas de dados no Gerenciador de Alertas de Dados](../reporting-services/manage-my-data-alerts-in-data-alert-manager.md).  
  
 A tabela a seguir mostra dados de exemplo de uma tabela no Gerenciador de Alertas de Dados. Quando um erro ocorre, a mensagem de erro e o identificador da entrada no log (um GUID) são incluídos no campo **Status** na tabela.  
  
|Nome do Alerta|Nome do Relatório|Criado por|Alertas enviados|Última Execução|Última Modificação|Status|  
|----------------|-----------------|----------------|-----------------|--------------|-------------------|------------|  
|SalesQTR|SalesByTerritoryAndQTR|Lauren Johnson|4|6/12/2011|6/1/2011|O último alerta foi executado com êxito e o alerta foi enviado.|  
|UnitsSold|ProductsSalesByQTR|Lauren Johnson|2|7/1/2011|6/28/2011|O último alerta foi executado com êxito, mas os dados estavam inalterados e nenhum alerta foi enviado.|  
|TopPromotion|PromotionTracking|Lauren Johnson|0||5/23/2011|Alertas criados.|  
  
  
##  <a name="DeleteAlerts"></a> Excluir alertas de dados  
 Você exclui definições de alertas no Gerenciador de Alertas de Dados. Como operador de informações, você pode excluir as definições de alerta que criou. Você não pode excluir definições de alerta criadas por outros. Para obter mais informações, consulte [Gerenciar meus alertas de dados no Gerenciador de Alertas de Dados](../reporting-services/manage-my-data-alerts-in-data-alert-manager.md).  
  
 Quando você exclui uma definição de alerta, ela é excluída permanentemente. Se você só quiser pausar mensagens de alerta, altere o padrão de recorrência ou a data de início ou término na definição de alerta. Para obter mais informações, consulte [Editar um Alerta de Dados no Designer de Alertas](../reporting-services/edit-a-data-alert-in-alert-designer.md).  
  
  
##  <a name="EditAlerts"></a> Editar alertas de dados  
 Como operador de informações, você abre as definições de alerta para edição no Gerenciador de Alertas de Dados. Você pode editar as definições de alerta que criou, mas não aquelas criadas por outros. Quando você clica com o botão direito do mouse na definição de alerta e clica em **Editar** , o Designer de Alerta de Dados é aberto, exibindo a definição de alertas. Para obter mais informações, consulte [Editar um Alerta de Dados no Designer de Alertas](../reporting-services/data-alert-designer.md) e [Designer de Alertas de Dados](../reporting-services/edit-a-data-alert-in-alert-designer.md).  
  
  
##  <a name="RunAlerts"></a> Executar alertas de dados  
 O Gerenciador de Alertas de Dados inclui informações sobre a última vez que o serviço de alertas processou a definição de alerta de dados e o número de vezes que a mensagem de alerta de dados foi enviada. Talvez você queira executar e enviar a mensagem de alerta imediatamente, em vez de esperar a hora especificada pelo agendamento. Quando você executa um alerta do Gerenciador de Alertas de Dados, o agendamento do alerta é substituída e o processamento da definição de alerta inicia em um a cinco minutos, dependendo do horário necessário para execução do relatório e o quão ocupado o servidor de relatório está no momento em que você decide executar o alerta. No entanto, se você especificou que uma mensagem somente seja enviada se os resultados forem alterados, e eles não foram alterados, nenhuma mensagem será criada ou enviada. Para obter mais informações, consulte [Gerenciar meus alertas de dados no Gerenciador de Alertas de Dados](../reporting-services/manage-my-data-alerts-in-data-alert-manager.md).  
  
> [!NOTE]  
>  Depois de clicar na opção **Executar**  , são necessários alguns segundos para atualizar o valor da coluna **Status** para indicar que o alerta está sendo processado. Se você clicar na opção **Executar**  várias vezes, o alerta será processado várias vezes. Isso consome recursos desnecessariamente no servidor de relatório e pode afetar o desempenho do servidor de relatório. Para visualizar informações atualizadas sobre o alerta, clique no botão de atualização de navegador da Web para verificar as atualizações de status e outras informações sobre o alerta.  
  
  
##  <a name="HowTo"></a> Tarefas relacionadas  
 Esta seção lista procedimentos que mostram como gerenciar seus alertas e editar suas definições de alertas.  
  
-   [Gerenciar meus alertas de dados no Gerenciador de Alertas de Dados](../reporting-services/manage-my-data-alerts-in-data-alert-manager.md)  
  
-   [Editar um alerta de dados no Designer de alertas](../reporting-services/edit-a-data-alert-in-alert-designer.md)  


## <a name="see-also"></a>Consulte Também

[Editar um Alerta de Dados no Designer de Alertas](../reporting-services/data-alert-designer.md)   
[Criar um alerta de dados no Designer de Alertas de Dados](../reporting-services/create-a-data-alert-in-data-alert-designer.md)   
[Reporting Services Data Alerts](../reporting-services/reporting-services-data-alerts.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
