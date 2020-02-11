---
title: Editor de destino ODBC (página Gerenciador de conexões) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcdest.connection.f1
ms.assetid: f6d9c6c2-e4c4-468b-9e0d-af7b9609614d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 281bbda38a6711efd4e2ffae7afbfa17d689254b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66057213"
---
# <a name="odbc-destination-editor-connection-manager-page"></a>Editor do Destino ODBC (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destino ODBC** para selecionar o gerenciador de conexões para o destino. Essa página também permite que você selecione uma tabela ou exibição a partir do banco de dados  
  
 Para obter mais informações sobre o destino ODBC, consulte [ODBC Destination](data-flow/odbc-destination.md).  
  
 **Para abrir a página do Gerenciador de Conexões do Editor de Destino ODBC**  
  
## <a name="task-list"></a>Lista de Tarefas  
  
-   No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] que tem o destino ODBC.  
  
-   Na guia **Fluxo de Dados** , clique duas vezes no destino ODBC.  
  
-   No **Editor de Destino ODBC**, clique em **Gerenciador de Conexões**.  
  
## <a name="options"></a>Opções  
  
### <a name="connection-manager"></a>Gerenciador de conexões  
 Selecione na lista um gerenciador de conexões ODBC existente ou clique em Novo para criar uma nova conexão. A conexão pode ser com qualquer banco de dados com suporte ODBC.  
  
### <a name="new"></a>Novo  
 Clique em **Nova**. É aberta a caixa de diálogo **Configurar Editor do Gerenciador de Conexões ODBC** , na qual você pode criar um novo gerenciador de conexões.  
  
### <a name="data-access-mode"></a>Modo de acesso a dados  
 Selecione o método de carregamento de dados no destino. As opções são mostradas na tabela a seguir:  
  
|Opção|DESCRIÇÃO|  
|------------|-----------------|  
|Nome da Tabela - Lote|Selecione esta opção para configurar o destino ODBC para trabalhar no modo de lote. Ao selecionar esta opção, as seguintes opções estão disponíveis:|  
||**Nome da tabela ou exibição**: selecione uma tabela ou exibição disponível na lista.<br /><br /> Essa lista contém apenas as primeiras 1.000 tabelas. Se o banco de dados contiver mais de 1000 tabelas, você poderá digitar o início do nome de uma tabela ou usar o curinga (\*) para inserir qualquer parte do nome para exibir a tabela ou tabelas desejadas.<br /><br /> **Tamanho do lote**: digite o tamanho do lote para carregamento em massa. Esse é o número de linhas carregadas como um lote|  
|Nome da Tabela - Linha a Linha|Selecione esta opção para configurar o destino ODBC para inserir cada uma das linhas na tabela de destino, uma de cada vez. Ao selecionar esta opção, a seguinte opção está disponível:|  
||**Nome da tabela ou exibição**: selecione uma tabela ou exibição disponível no banco de dados na lista.<br /><br /> Essa lista contém apenas as primeiras 1.000 tabelas. Se o banco de dados contiver mais de 1.000 tabelas, você poderá digitar o início do nome de uma tabela ou usar o curinga (*) para inserir qualquer parte do nome para exibir a tabela ou tabelas desejadas.|  
  
### <a name="preview"></a>Visualização  
 Clique em **Visualizar** para exibir até 200 linhas de dados da tabela selecionada.  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades personalizadas de destino ODBC](data-flow/odbc-destination-custom-properties.md)   
 [Editor de Destinos ODBC &#40;Página Mapeamentos&#41;](../../2014/integration-services/odbc-destination-editor-mappings-page.md)   
 [Editor do Destino ODBC &#40;Página Saída de Erro&#41;](../../2014/integration-services/odbc-destination-editor-error-output-page.md)  
  
  
