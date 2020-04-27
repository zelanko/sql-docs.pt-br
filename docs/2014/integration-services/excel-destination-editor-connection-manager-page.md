---
title: Editor de destino do Excel (página Gerenciador de conexões) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.exceldestadapter.connection.f1
helpviewer_keywords:
- Excel Destination Editor
ms.assetid: fc13f725-963c-488e-91e2-20627133e842
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c55b9daba7e8e1823e1ced43fc9958d4fe5892ff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66059239"
---
# <a name="excel-destination-editor-connection-manager-page"></a>Editor de Destinos do Excel (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destinos do Excel** para especificar informações da fonte de dados e visualizar os resultados. O destino do Excel carrega dados em uma planilha ou um intervalo nomeado em uma pasta de trabalho do [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] .  
  
> [!NOTE]  
>  A `CommandTimeout` Propriedade do destino do Excel não está disponível no **Editor de destino do Excel**, mas pode ser definida usando o **Editor avançado**. Além disso, determinadas opções de carregamento rápido só estarão disponíveis no **Editor Avançado**. Para obter mais informações sobre essas propriedades, consulte a seção Destino do Excel em [Excel Custom Properties](data-flow/excel-custom-properties.md).  
  
 Para obter mais informações sobre destinos do Excel, consulte [Excel Destination](data-flow/excel-destination.md).  
  
## <a name="static-options"></a>Opções estáticas  
 **Gerenciador de conexões do Excel**  
 Selecione um gerenciador de conexões do Excel existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Novo**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Gerenciador de Conexões do Excel** .  
  
 **Modo de acesso a dados**  
 Especifique o método para selecionar os dados da origem.  
  
|Opção|Descrição|  
|------------|-----------------|  
|Tabela ou exibição|Carregue dados em uma planilha ou intervalo nomeado na fonte de dados do Excel.|  
|Nome da tabela ou variável do nome de exibição|Especifique a planilha ou o nome do intervalo em uma variável.<br /><br /> **Informações relacionadas**: [Usar variáveis em pacotes](../../2014/integration-services/use-variables-in-packages.md)|  
|Comando SQL|Carregue dados no destino do Excel usando uma consulta SQL.|  
  
 **Nome da planilha do Excel**  
 Selecione o destino do Excel da listagem suspensa. Se a lista estiver vazia, clique em **Novo**.  
  
 **Novo**  
 Clique em **Novo** para iniciar a caixa de diálogo **Criar Tabela** . Quando você clicar em **OK**, a caixa de diálogo cria o arquivo Excel para o qual o **Gerenciador de Conexões do Excel** aponta.  
  
 **Exibir dados existentes**  
 Visualize os resultados usando a caixa de diálogo **Visualizar Resultados da Consulta** . A visualização pode exibir até 200 linhas.  
  
> [!WARNING]  
>   Se o **Gerenciador de conexões do Excel** que você selecionou apontar para um arquivo do Excel que não existe, você verá uma mensagem de erro ao clicar neste botão.  
  
## <a name="data-access-mode-dynamic-options"></a>Opções dinâmicas de modo de acesso aos dados  
  
### <a name="data-access-mode--table-or-view"></a>Modo de acesso aos dados = Tabela ou exibição  
 **Nome da planilha do Excel**  
 Selecione o nome da planilha ou o intervalo nomeado na lista disponível na fonte de dados.  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modo de acesso aos dados = Variável do nome da tabela ou do nome de exibição  
 **Nome da variável**  
 Selecione a variável que contém o nome da planilha ou do intervalo nomeado.  
  
### <a name="data-access-mode--sql-command"></a>Modo de acesso aos dados = Comando SQL  
 **Texto do comando SQL**  
 Digite o texto de uma consulta SQL, crie a consulta clicando em **Construir Consulta**ou localize o arquivo que contém o texto da consulta clicando em **Procurar**.  
  
 **Construir Consulta**  
 Use a caixa de diálogo **Construtor de Consultas** para construir a consulta SQL visualmente.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para localizar o arquivo com contém o texto da consulta SQL.  
  
 **Analisar consulta**  
 Verifique a sintaxe do texto da consulta.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Página Mapeamentos &#40;editor de destinos do Excel&#41;](../../2014/integration-services/excel-destination-editor-mappings-page.md)   
 [Editor de destinos do Excel &#40;página saída de erro&#41;](../../2014/integration-services/excel-destination-editor-error-output-page.md)   
 [Loop por meio de arquivos do Excel e tabelas usando um contêiner de Loop Foreach](control-flow/foreach-loop-container.md)  
  
  
