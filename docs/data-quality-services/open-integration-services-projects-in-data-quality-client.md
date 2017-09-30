---
title: Abrir projetos do Integration Services no Data Quality Client | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a8bad2f1-8fb0-4d14-a978-11a5720e62d6
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: b8f5c57ad6f0b73eb7d8f56bd8c34dd03319bf7c
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="open-integration-services-projects-in-data-quality-client"></a>Abrir projetos do Integration Services no cliente Data Quality
  O componente Limpeza do DQS no Integration Services permite executar um projeto de limpeza no modo de lote. No entanto, às vezes talvez você queira examinar os resultados da limpeza em um pacote do Integration Services semelhante ao modo como é possível examinar os resultados da limpeza na guia **Gerenciar e Exibir Resultados** de uma atividade de limpeza em um projeto de qualidade de dados no DQS. O DQS permite que você abra projetos do Integration Services no [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] da mesma forma que faria com qualquer outro projeto de qualidade de dados na tela **Abrir projeto** e proporciona uma experiência de limpeza interativa dos resultados da consulta em um projeto do Integration Services.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="LimitationsRestrictions"></a> Limitações e restrições  
  
-   Somente projetos concluídos do Integration Services estão disponíveis na tela **Abrir projeto** no [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Os projetos que falharam ou que estão em execução não estão disponíveis na tela **Abrir projeto** .  
  
-   Os projetos do Integration Services são abertos no estágio de limpeza interativa (guia**Gerenciar e Exibir Resultados** ) no [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Você não pode ir para as guias **Limpar** ou **Mapear** . Somente é possível acessar a guia **Exportar** clicando em **Avançar**.  
  
-   Não é possível excluir um projeto bloqueado do Integration Services do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Primeiro você deve desbloqueá-lo para excluir.  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Você deve ter concluído com êxito um projeto do Integration Services contendo um pacote com um componente de Limpeza do DQS para visualizá-lo e abri-lo no [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_kb_operator no banco de dados DQS_MAIN para abrir um projeto do Integration Services.  
  
  
##  <a name="Open"></a> Abrir um projeto do Integration Services  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Abrir Projeto de Qualidade de Dados**. A tela **Abrir projeto** é aberta.  
  
3.  Na tela **Abrir projeto** , você pode identificar um projeto do Integration Services de uma destas formas:  
  
    1.  **Nome do Projeto**: os projetos do Integration Services são listados com a seguinte terminologia de nomenclatura: “Package.DQS Cleansing_*\<DATE>**\<TIME>*_{GUID}”. Sempre que você executa com êxito o mesmo pacote no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], um novo projeto é listado na tela **Abrir projeto** .  
  
    2.  **Tipo de Projeto**: os projetos do Integration Services têm **SSIS** como o tipo de projeto na tela **Abrir projeto** .  
  
     Selecione um projeto e clique em **Avançar**.  
  
4.  O projeto do Integration Services é aberto no estágio de limpeza interativa (guia**Gerenciar e Exibir Resultados** ). Você pode executar uma limpeza interativa nos dados no projeto do Integration Services. Para obter informações detalhadas sobre a guia **Gerenciar e Exibir Resultados**, consulte [Estágio de limpeza interativa](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Interactive) em [Limpar dados usando o conhecimento &#40;interno&#41; do DQS](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md).  
  
5.  Clique em **Avançar** para ir para a guia **Exportar** em que você pode exportar os dados processados para qualquer um dos seguintes: uma nova tabela no banco de dados do SQL Server, um arquivo .csv ou um arquivo do Excel. Para obter informações detalhadas sobre a guia **Exportar**, consulte [Estágio de exportação](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Export) em [Limpar dados usando o conhecimento &#40;interno&#41; do DQS](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)  
  
6.  Depois de exportar os dados, clique em **Concluir** para fechar o projeto do Integration Services.  

  
## <a name="see-also"></a>Consulte também  
 [Transformação de Limpeza do DQS](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)   
 [Projetos do SSIS (Integration Services)](../integration-services/integration-services-ssis-projects-and-solutions.md)  
  
  
