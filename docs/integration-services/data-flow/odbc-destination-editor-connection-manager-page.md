---
title: "Editor do Destino ODBC (p&#225;gina Gerenciador de Conex&#245;es) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.designer.odbcdest.connection.f1"
ms.assetid: f6d9c6c2-e4c4-468b-9e0d-af7b9609614d
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Editor do Destino ODBC (p&#225;gina Gerenciador de Conex&#245;es)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destino ODBC** para selecionar o gerenciador de conexões para o destino. Essa página também permite que você selecione uma tabela ou exibição a partir do banco de dados  
  
 Para obter mais informações sobre o destino ODBC, consulte [ODBC Destination](../../integration-services/data-flow/odbc-destination.md).  
  
 **Para abrir a página do Gerenciador de Conexões do Editor de Destino ODBC**  
  
## Lista de Tarefas  
  
-   No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tem o destino ODBC.  
  
-   Na guia **Fluxo de Dados**, clique duas vezes no destino ODBC.  
  
-   No **Editor de Destino ODBC**, clique em **Gerenciador de Conexões**.  
  
## Opções  
  
### Gerenciador de conexões  
 Selecione na lista um gerenciador de conexões ODBC existente ou clique em Novo para criar uma nova conexão. A conexão pode ser com qualquer banco de dados com suporte ODBC.  
  
### Nova  
 Clique em **Nova**. É aberta a caixa de diálogo **Configurar Editor do Gerenciador de Conexões ODBC** , na qual você pode criar um novo gerenciador de conexões.  
  
### Modo de acesso a dados  
 Selecione o método de carregamento de dados no destino. As opções são mostradas na tabela a seguir:  
  
|Opção|Description|  
|------------|-----------------|  
|Nome da Tabela - Lote|Selecione esta opção para configurar o destino ODBC para trabalhar no modo de lote. Ao selecionar esta opção, as seguintes opções estão disponíveis:|  
||**Nome da tabela ou exibição**: selecione uma tabela ou exibição disponível na lista.<br /><br /> Essa lista contém apenas as primeiras 1.000 tabelas. Se o banco de dados contiver mais de 1000 tabelas, você poderá digitar o início do nome de uma tabela ou usar o curinga (\*) para inserir qualquer parte do nome para exibir a tabela ou tabelas desejadas.<br /><br /> **Tamanho do lote**: digite o tamanho do lote para carregamento em massa. Esse é o número de linhas carregadas como um lote|  
|Nome da Tabela - Linha a Linha|Selecione esta opção para configurar o destino ODBC para inserir cada uma das linhas na tabela de destino, uma de cada vez. Ao selecionar esta opção, a seguinte opção está disponível:|  
||**Nome da tabela ou exibição**: selecione uma tabela ou exibição disponível no banco de dados na lista.<br /><br /> Essa lista contém apenas as primeiras 1.000 tabelas. Se o banco de dados contiver mais de 1.000 tabelas, você poderá digitar o início do nome de uma tabela ou usar o curinga (*) para inserir qualquer parte do nome para exibir a tabela ou tabelas desejadas.|  
  
### Visualização  
 Clique em **Visualizar** para exibir até 200 linhas de dados da tabela selecionada.  
  
## Consulte também  
 [Propriedades personalizadas de destino ODBC](../../integration-services/data-flow/odbc-destination-custom-properties.md)   
 [Editor de Destinos ODBC &#40;Página Mapeamentos&#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)   
 [Editor do Destino ODBC &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/odbc-destination-editor-error-output-page.md)  
  
  