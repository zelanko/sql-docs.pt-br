---
title: Editor de destinos do Excel (página Gerenciador de Conexão) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.exceldestadapter.connection.f1
helpviewer_keywords:
- Excel Destination Editor
ms.assetid: fc13f725-963c-488e-91e2-20627133e842
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f790e0cc9193f2f31c7f021c4d4901e7a825fb13
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62769732"
---
# <a name="excel-destination-editor-connection-manager-page"></a>Editor de Destinos do Excel (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destinos do Excel** para especificar informações da fonte de dados e visualizar os resultados. O destino do Excel carrega dados em uma planilha ou um intervalo nomeado em uma pasta de trabalho do [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] .  
  
> [!NOTE]  
>  O `CommandTimeout` propriedade do destino do Excel não está disponível na **Editor de destino do Excel**, mas pode ser definida usando a **Editor Avançado**. Além disso, determinadas opções de carregamento rápido só estarão disponíveis no **Editor Avançado**. Para obter mais informações sobre essas propriedades, consulte a seção Destino do Excel em [Excel Custom Properties](data-flow/excel-custom-properties.md).  
  
 Para obter mais informações sobre destinos do Excel, consulte [Excel Destination](data-flow/excel-destination.md).  
  
## <a name="static-options"></a>Opções estáticas  
 **Gerenciador de conexões do Excel**  
 Selecione um gerenciador de conexões do Excel existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Gerenciador de Conexões do Excel** .  
  
 **Modo de acesso aos dados**  
 Especifique o método para selecionar os dados da origem.  
  
|Opção|Descrição|  
|------------|-----------------|  
|Tabela ou exibição|Carregue dados em uma planilha ou intervalo nomeado na fonte de dados do Excel.|  
|Nome da tabela ou variável do nome de exibição|Especifique a planilha ou o nome do intervalo em uma variável.<br /><br /> **Informações relacionadas**: [Usar variáveis em pacotes](../../2014/integration-services/use-variables-in-packages.md)|  
|Comando SQL|Carregue dados no destino do Excel usando uma consulta SQL.|  
  
 **Nome da planilha do Excel**  
 Selecione o destino do Excel da listagem suspensa. Se a lista estiver vazia, clique em **Novo**.  
  
 **Nova**  
 Clique em **Novo** para iniciar a caixa de diálogo **Criar Tabela** . Quando você clicar em **OK**, a caixa de diálogo cria o arquivo Excel para o qual o **Gerenciador de Conexões do Excel** aponta.  
  
 **Exibir dados existentes**  
 Visualize os resultados usando a caixa de diálogo **Visualizar Resultados da Consulta** . A visualização pode exibir até 200 linhas.  
  
> [!WARNING]  
>  Se o **Gerenciador de conexões do Excel** que você selecionou apontar para um arquivo do Excel que não existe, você verá uma mensagem de erro ao clicar neste botão.  
  
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
  
 **Analisar Consulta**  
 Verifique a sintaxe do texto da consulta.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de Destinos do Excel &#40;página Mapeamentos&#41;](../../2014/integration-services/excel-destination-editor-mappings-page.md)   
 [Editor de Destinos do Excel &#40;Página Saída de Erro&#41;](../../2014/integration-services/excel-destination-editor-error-output-page.md)   
 [Loop através de arquivos e tabelas do Excel por meio de um contêiner do Loop Foreach](control-flow/foreach-loop-container.md)  
  
  
