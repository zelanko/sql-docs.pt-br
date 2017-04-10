---
title: "Abrir projetos do Integration Services no cliente Data Quality | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a8bad2f1-8fb0-4d14-a978-11a5720e62d6
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# Abrir projetos do Integration Services no cliente Data Quality
  O componente de limpeza do DQs no Integration Services permite que você execute um projeto de limpeza no modo em lotes. No entanto, às vezes você poderá examinar os resultados da limpeza em um pacote do Integration Services semelhante a como você pode examinar os resultados da limpeza no **Gerenciar e exibir resultados** guia de uma atividade de limpeza em um projeto de qualidade de dados no DQS. O DQS permite que você abra projetos do Integration Services em [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] assim como qualquer outro projeto de qualidade de dados do **Abrir projeto** tela e ter uma experiência de limpeza interativa dos resultados da limpeza em um projeto do Integration Services.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="LimitationsRestrictions"></a> Limitações e restrições  
  
-   Somente concluídos do Integration Services projetos estão disponíveis no **Abrir projeto** de tela [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Projetos em execução ou com falha não estão disponíveis na **Abrir projeto** tela.  
  
-   Abrir projetos do Integration Services no estágio de limpeza interativo (**Gerenciar e exibir resultados** guia) em [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Você não pode ir para o **Limpar** ou **mapa** guias. Você pode ir apenas até o **exportar** guia clicando **próxima**.  
  
-   Não é possível excluir um projeto bloqueado do Integration Services do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Primeiro você deve desbloqueá-lo para excluir.  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Você deve ter concluído com êxito um projeto do Integration Services que contém um pacote com um componente de limpeza do DQS para ver e abri-lo no [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_kb_operator no banco de dados DQS_MAIN para abrir um projeto do Integration Services.  
  
  
##  <a name="Open"></a> Abrir um projeto do Integration Services  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo de cliente de qualidade de dados](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] tela inicial, clique em **Abrir projeto de qualidade de dados**. A tela **Abrir projeto** é aberta.  
  
3.  No **Abrir projeto** tela, você pode identificar um projeto do Integration Services em qualquer uma das seguintes maneiras:  
  
    1.  **Nome do projeto**: projetos do Integration Services são listados com a seguinte terminologia de nomenclatura: "Package. DQS cleansing _*\< data>**\< tempo>*_ {GUID}." Sempre que você executa com êxito o mesmo pacote [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], um novo projeto é listado no **Abrir projeto** tela.  
  
    2.  **Tipo de projeto**: projetos do Integration Services têm **SSIS** como o tipo de projeto no **Abrir projeto** tela.  
  
     Selecione um projeto e clique em **próxima**.  
  
4.  O projeto do Integration Services será aberto no estágio de limpeza interativo (**Gerenciar e exibir resultados** guia). Você pode executar uma limpeza interativa nos dados no projeto do Integration Services. Para obter informações detalhadas sobre o **Gerenciar e exibir resultados** guia, consulte [estágio de limpeza interativa](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Interactive) em [Limpar dados usando o DQS &40; interno &41; Conhecimento](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md).  
  
5.  Clique em **próxima** para ir para o **exportar** guia onde você pode exportar os dados processados para qualquer um dos seguintes: uma nova tabela no banco de dados do SQL Server, um arquivo. csv ou um arquivo do Excel. Para obter informações detalhadas sobre o **exportar** guia, consulte [estágio de exportação](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Export) em [Limpar dados usando o DQS &40; interno &41; Dados de Conhecimento](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)  
  
6.  Depois de exportar os dados, clique em **Concluir** para fechar o projeto do Integration Services.  

  
## Consulte também  
 [Transformação de Limpeza DQS](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)   
 [O Integration Services (SSIS) projetos](https://msdn.microsoft.com/library/ms138028.aspx)  
  
  