---
title: Criar um alerta de dados no Designer de alertas de dados | Microsoft Docs
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8464ab9d-afe1-4490-955f-9f3319bcbf8d
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 5203aab062888ca40ee83ee3f00521d6661defba
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="create-a-data-alert-in-data-alert-designer"></a>Criar um alerta de dados no Designer de Alertas de Dados

[!INCLUDE[ssrs-appliesto-sql2016-xpreview](../includes/ssrs-appliesto-sql2016-xpreview.md)][!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

Você cria definições de alerta de dados no Designer de Alertas de Dados. Depois de salvar as definições de alertas, é possível abri-la novamente, editá-la e salvá-la novamente no Designer de Alertas de Dados. Para obter informações sobre como editar definições de alertas, consulte [Gerenciar meus alertas de dados no Gerenciador de Alertas de Dados](../reporting-services/manage-my-data-alerts-in-data-alert-manager.md) e [Editar um alerta de dados no Designer de Alertas](../reporting-services/edit-a-data-alert-in-alert-designer.md).

> [!NOTE]
> Integração do Reporting Services com o SharePoint não está mais disponível após o SQL Server 2016.

## <a name="create-a-data-alert-definition"></a>Criar uma definição de alerta de dados
 
1.  Localize a biblioteca do SharePoint que contém o relatório para o qual você deseja criar uma definição de alerta de dados.  
  
2.  Clique no relatório.  
  
     O relatório é executado. Se o relatório for parametrizado, verifique se o relatório mostra os dados sobre os quais você deseja receber mensagens de alerta de dados. Se você não vir as colunas ou valores nos quais está interessado, talvez seja necessário executar o relatório novamente, com o uso de valores de parâmetros diferentes.  
  
    > [!NOTE]  
    >  Os valores de parâmetros que você escolheu para executar o relatório são salvos na definição de alerta e serão usados quando o relatório for executado novamente como uma etapa do processamento da definição de alerta. Para usar diferentes valores de parâmetro, você deve criar uma nova definição de alerta.  
  
3.  No menu **Ações** , clique em **Novo Alerta de Dados**.  
  
     A imagem a seguir mostra o menu **Ações** .  
  
     ![Abra o Designer de alertas de biblioteca do SharePoint](../reporting-services/media/rs-openalertdesigneriw.gif "abrir o Designer de alertas de biblioteca do SharePoint")  
  
     O Designer de Alertas de Dados é aberto e mostra as primeiras 100 linhas do primeiro feed de dados que o relatório gera em uma tabela.  
  
    > [!NOTE]  
    >  Se você não visualizar a opção **Novo Alerta de Dados** , o serviço de alerta não está configurado no site do SharePoint ou a edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não inclui alertas de dados. Para obter mais informações, consulte [Serviço SharePoint do Reporting Services e aplicativos de serviço](../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md).  
    >   
    >  Se a opção **Novo Alerta de Dados** estiver acinzentada, a fonte de dados de relatório está configurada para usar credenciais de segurança integradas ou para solicitar credenciais. Para tornar a opção **Novo Alerta de Dados** disponível, você deve atualizar a fonte de dados para usar credenciais armazenadas ou nenhuma credencial.  
  
     O nome do feed de dados é exibido na lista suspensa **Nome de dados do relatório** .  
  
4.  Opcionalmente, selecione um feed de dados diferente na lista suspensa **Nome de dados do relatório** .  
  
     Se nenhum feed de dados for gerado a partir do relatório, você não poderá criar uma definição de alerta para o relatório. O layout do relatório determina o conteúdo de cada feed de dados. Para obter mais informações, consulte [Gerando feeds de dados de relatórios &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md).  
  
5.  Opcionalmente, na caixa de texto **Nome do alerta** , atualize o nome padrão para que seja mais significativo.  
  
     O nome padrão da definição de alerta é o nome do relatório. Os nomes de definições de alertas não precisam ser exclusivos, o que pode dificultar sua diferenciação quando você exibir a lista de alertas mais tarde no Gerenciador de Alertas de Dados. É recomendável usar nomes de definições de alertas significativos e exclusivos.  
  
6.  Opcionalmente, altere a opção de dados padrão de **quaisquer dados do feed de dados possui** para **nenhum dos dados do feed de dados tem**.  
  
7.  Clique em **Adicionar regra**.  
  
     Uma lista das colunas no feed de dados é exibida.  
  
8.  Na lista, selecione a coluna que você deseja usar na regra e selecione um operador de comparação e insira o valor de limite.  
  
     Dependendo do tipo dos dados da coluna selecionada, diferentes operadores de comparação serão listados. Se a coluna tiver um tipo de dados de data, um ícone de calendário será exibido ao lado do valor de limite da regra. É possível inserir dados com um clique em uma data no calendário ou por meio de digitação da data.  
  
     O Designer de Alertas de Dados fornece dois modos de comparação: **Modo de Entrada de Valor** e **Modo de Seleção de Campo**. O padrão é **Modo de Entrada de Valor**. Você só pode adicionar cláusulas OR quando está no **Modo de Entrada de Valor** e está usando a comparação **is** .  
  
9. Para adicionar uma cláusula OR, clique na seta para baixo e clique em **Modo de Entrada de Valor**.  
  
10. Digite o valor de comparação.  
  
11. Opcionalmente, clique nas reticências **(...)** novamente.  
  
     As reticências **(...)** aparecem na linha que contém a primeira cláusula.  
  
     Uma cláusula OR é adicionada sob e na regra AND.  
  
12. Opcionalmente, clique na seta para baixo, selecione **Modo de Seleção de Campo**e selecione uma coluna na lista.  
  
     Você notará que as reticências **(...)** em que clica para adicionar cláusulas OR desapareceram.  
  
13. Opcionalmente, clique em **Adicionar regra** novamente para adicionar mais regras.  
  
     As regras são combinadas com o uso do operador lógico AND.  
  
14. Selecione uma opção na lista de recorrência. Dependendo do tipo de recorrência, insira um intervalo.  
  
15. Opcionalmente, clique em **Avançado**.  
  
16. Opcionalmente, altere a data de início da mensagem de alerta por meio da digitação de uma data diferente ou por maio da abertura do calendário e um clique em uma data do calendário.  
  
     A data inicial padrão é a data atual.  
  
17. Opcionalmente, marque a caixa de seleção localizada ao lado de **Parar alerta em**e escolha uma data para parar a mensagem de alerta.  
  
     Por padrão, uma mensagem de alerta não tem nenhuma data de parada.  
  
    > [!NOTE]  
    >  Parar uma mensagem de alerta não exclui a definição do alerta. Depois que você parar uma mensagem de alerta, poderá reiniciá-la atualizando as datas de início e término. Para obter informações sobre como excluir definições de alertas, consulte [Gerenciar meus alertas de dados no Gerenciador de Alertas de Dados](../reporting-services/manage-my-data-alerts-in-data-alert-manager.md).  
  
18. Opcionalmente, desmarque a caixa de seleção **Enviar mensagens somente se os resultados forem alterados** .  
  
     Se você enviar mensagens de alerta frequentemente, informações redundantes talvez não sejam bem-vindas e essa caixa de seleção deverá ser desmarcada.  
  
19. Digite os endereços de email dos destinatários da mensagem de alerta. Separe os endereços com ponto-e-vírgulas.  
  
     Se o endereço de email da pessoa que criou a definição de alerta estiver disponível, ele será adicionado à caixa **Destinatário(s)** .  
  
20. Opcionalmente, na caixa de texto **Assunto** , atualize a linha de Assunto da mensagem de alerta.  
  
     O assunto padrão é **de alertas de dados para \<nome do alerta de dados >**.  
  
21. Opcionalmente, na caixa de texto **Descrição** , digite uma descrição da mensagem de alerta.  
  
22. Clique em **Salvar**.  

## <a name="see-also"></a>Consulte também

[Designer de Alertas de Dados](../reporting-services/data-alert-designer.md)   
[Gerenciador de Alertas de dados para administradores de alertas](../reporting-services/data-alert-manager-for-alerting-administrators.md)   
[Alertas de dados do Reporting Services](../reporting-services/reporting-services-data-alerts.md)  

Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
