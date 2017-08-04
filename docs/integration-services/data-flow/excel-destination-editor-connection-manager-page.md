---
title: "Editor de destino do Excel (página Gerenciador de Conexão) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.exceldestadapter.connection.f1
helpviewer_keywords:
- Excel Destination Editor
ms.assetid: fc13f725-963c-488e-91e2-20627133e842
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a1627a4907b35522a4c3bcbc03f366f77706ac87
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="excel-destination-editor-connection-manager-page"></a>Editor de Destinos do Excel (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destinos do Excel** para especificar informações da fonte de dados e visualizar os resultados. O destino do Excel carrega dados em uma planilha ou um intervalo nomeado em uma pasta de trabalho do [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] .  
  
> [!NOTE]  
>  A propriedade **CommandTimeout** do destino do Excel não está disponível no **Editor de Destinos do Excel**, mas pode ser definida com o **Editor Avançado**. Além disso, determinadas opções de carregamento rápido só estarão disponíveis no **Editor Avançado**. Para obter mais informações sobre essas propriedades, consulte a seção Destino do Excel em [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md).  
  
 Para obter mais informações sobre destinos do Excel, consulte [Excel Destination](../../integration-services/data-flow/excel-destination.md).  
  
## <a name="static-options"></a>Opções estáticas  
 **Gerenciador de conexões do Excel**  
 Selecione um gerenciador de conexões do Excel existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Gerenciador de Conexões do Excel** .  
  
 **Modo de acesso aos dados**  
 Especifique o método para selecionar os dados da origem.  
  
|Opção|Description|  
|------------|-----------------|  
|Tabela ou exibição|Carregue dados em uma planilha ou intervalo nomeado na fonte de dados do Excel.|  
|Nome da tabela ou variável do nome de exibição|Especifique a planilha ou o nome do intervalo em uma variável.<br /><br /> **Informações relacionadas**: [Usar variáveis em pacotes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
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
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de destino do Excel &#40; Página mapeamentos &#41;](../../integration-services/data-flow/excel-destination-editor-mappings-page.md)   
 [Editor de destino do Excel &#40; Página de saída de erro &#41;](../../integration-services/data-flow/excel-destination-editor-error-output-page.md)   
 [Loop por meio do Excel arquivos e tabelas usando um contêiner Loop Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  
