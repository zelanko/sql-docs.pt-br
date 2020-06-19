---
title: Editor de origem ADO NET (página Gerenciador de conexões) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.adonetsource.connection.f1
ms.assetid: 7de3f438-bdd6-49b5-937a-47369e754943
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 7d6dc089acb1d15491817d8876dee82951e4495d
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84925847"
---
# <a name="ado-net-source-editor-connection-manager-page"></a>Editor de origem ADO NET (Página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem ADO NET** para selecionar o gerenciador de conexões [!INCLUDE[vstecado](../includes/vstecado-md.md)] para a origem. Essa página também permite que você selecione uma tabela ou exibição a partir do banco de dados.  
  
 Para obter mais informações sobre a origem ADO NET, consulte [ADO NET Source](data-flow/ado-net-source.md).  
  
 **Para abrir a página Gerenciador de Conexões**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que tenha a origem ADO NET.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na origem ADO NET.  
  
3.  No **Editor de Origem ADO NET**, clique em **Gerenciador de Conexões**.  
  
## <a name="static-options"></a>Opções estáticas  
 **Gerenciador de conexões ADO.NET**  
 Selecione um gerenciador de conexões existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Novo**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Configurar Gerenciador de Conexões ADO NET** .  
  
 **Modo de acesso a dados**  
 Especifique o método para selecionar os dados da origem.  
  
|Opção|Descrição|  
|------------|-----------------|  
|Tabela ou exibição|Recupere os dados de uma tabela ou visualize na fonte de dados [!INCLUDE[vstecado](../includes/vstecado-md.md)] .|  
|Comando SQL|Recupere os dados da fonte de dados [!INCLUDE[vstecado](../includes/vstecado-md.md)] usando uma consulta SQL.|  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Exibição de Dados** . A**visualização** pode exibir até 200 linhas.  
  
> [!NOTE]  
>  Quando você visualiza os dados, as colunas com um tipo de dado CLR definido pelo usuário não contêm dados. Em vez disso, os valores \<value too big to display> ou System. Byte [] são exibidos. O primeiro é exibido quando a fonte de dados é acessada usando o provedor [!INCLUDE[vstecado](../includes/vstecado-md.md)] , o último ao usar o provedor Native Client do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="data-access-mode-dynamic-options"></a>Opções dinâmicas de modo de acesso aos dados  
  
### <a name="data-access-mode--table-or-view"></a>Modo de acesso aos dados = Tabela ou exibição  
 **Nome da tabela ou da exibição**  
 Selecione o nome da tabela ou da exibição na lista de tabelas ou exibições disponíveis na fonte de dados.  
  
### <a name="data-access-mode--sql-command"></a>Modo de acesso aos dados = Comando SQL  
 **Texto do comando SQL**  
 Digite o texto de uma consulta SQL, crie a consulta clicando em **Construir Consulta**ou localize o arquivo que contém o texto da consulta clicando em **Procurar**.  
  
 **Compilar consulta**  
 Use a caixa de diálogo **Construtor de Consultas** para construir a consulta SQL visualmente.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para localizar o arquivo com contém o texto da consulta SQL.  
  
## <a name="see-also"></a>Consulte Também  
 [Editor de origem ADO NET &#40;página colunas&#41;](../../2014/integration-services/ado-net-source-editor-columns-page.md)   
 [Editor de origem ADO NET &#40;página saída de erro&#41;](../../2014/integration-services/ado-net-source-editor-error-output-page.md)   
 [Gerenciador de conexões ADO.NET](connection-manager/ado-net-connection-manager.md)  
  
  
