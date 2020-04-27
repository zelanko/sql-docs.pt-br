---
title: Editor de origem ODBC (página Gerenciador de conexões) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcsource.connection.f1
ms.assetid: e2c8dc83-6394-4d6c-9232-97e94be72431
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bea70ca9d5d511660ff19a84165a7fc7921b6de1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66057217"
---
# <a name="odbc-source-editor-connection-manager-page"></a>Editor de Origem ODBC (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem ODBC** para selecionar o gerenciador de conexões ODBC para a origem. Essa página também permite que você selecione uma tabela ou exibição a partir do banco de dados.  
  
 Para obter mais informações sobre essa fonte ODBC, consulte [Fonte ODBC](data-flow/odbc-source.md).  
  
## <a name="task-list"></a>Lista de Tarefas  
 **Para abrir a página do Gerenciador de Conexões do Editor de Origem ODBC**  
  
-   No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] que tem a fonte ODBC.  
  
-   Na guia **Fluxo de Dados** , clique duas vezes na fonte ODBC.  
  
## <a name="options"></a>Opções  
  
### <a name="connection-manager"></a>Gerenciador de conexões  
 Selecione um Gerenciador de conexões ODBC existente na lista ou clique em **novo** para criar uma nova conexão. A conexão pode ser com qualquer banco de dados com suporte ODBC.  
  
### <a name="new"></a>Novo  
 Clique em **Novo**. É aberta a caixa de diálogo **Configurar Editor do Gerenciador de Conexões ODBC** , na qual você pode criar um novo gerenciador de conexões ODBC.  
  
### <a name="data-access-mode"></a>Modo de acesso a dados  
 Especifique o método para selecionar dados da origem. As opções são mostradas na tabela a seguir:  
  
|Opção|Descrição|  
|------------|-----------------|  
|Nome da tabela|Recupere os dados de uma tabela ou exibição na fonte de dados ODBC. Quando você selecionar esta opção, selecione um valor na lista para o seguinte:|  
||**Nome da tabela ou exibição**: selecione uma tabela ou exibição disponível na lista ou digite uma expressão regular para identificar a tabela.|  
||Essa lista contém apenas as primeiras 1.000 tabelas. Se o banco de dados contiver mais de 1.000 tabelas, você poderá digitar o início do nome de uma tabela ou usar o curinga (*) para inserir qualquer parte do nome para exibir a tabela ou tabelas desejadas.|  
|Comando SQL|Recupere os dados da fonte de dados ODBC usando uma consulta SQL. Você deve escrever a consulta na sintaxe do banco de dados de origem com o qual está trabalhando. Quando selecionar esta opção, insira uma consulta de uma das seguintes maneiras:|  
||Insira o texto da consulta SQL no campo **Texto do comando do SQL** .|  
||Clique em **Procurar** para carregar a consulta SQL de um arquivo de texto.|  
||Clique em **Analisar consulta** para verificar a sintaxe do texto da consulta.|  
  
### <a name="preview"></a>Visualização  
 Clique em **Visualizar** para exibir até as primeiras 200 linhas dos dados extraídos da tabela ou exibição selecionada.  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades personalizadas de origem ODBC](data-flow/odbc-source-custom-properties.md)   
 [Editor de origem ODBC &#40;página colunas&#41;](../../2014/integration-services/odbc-source-editor-columns-page.md)   
 [Editor de Fonte ODBC &#40;Página Saída de Erro&#41;](../../2014/integration-services/odbc-source-editor-error-output-page.md)  
  
  
