---
title: "Editor de origem ADO NET (P&#225;gina Gerenciador de Conex&#245;es) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.adonetsource.connection.f1"
ms.assetid: 7de3f438-bdd6-49b5-937a-47369e754943
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# Editor de origem ADO NET (P&#225;gina Gerenciador de Conex&#245;es)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem ADO NET** para selecionar o gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] para a origem. Essa página também permite que você selecione uma tabela ou exibição a partir do banco de dados.  
  
 Para obter mais informações sobre a origem ADO NET, consulte [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).  
  
 **Para abrir a página Gerenciador de Conexões**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que tenha a origem ADO NET.  
  
2.  Na guia **Fluxo de Dados**, clique duas vezes na origem ADO NET.  
  
3.  No **Editor de Origem ADO NET**, clique em **Gerenciador de Conexões**.  
  
## Opções estáticas  
 **Gerenciador de conexões ADO.NET**  
 Selecione um gerenciador de conexões existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Configurar Gerenciador de Conexões ADO NET**.  
  
 **Modo de acesso aos dados**  
 Especifique o método para selecionar os dados da origem.  
  
|Opção|Description|  
|------------|-----------------|  
|Tabela ou exibição|Recupere os dados de uma tabela ou visualize na fonte de dados [!INCLUDE[vstecado](../../includes/vstecado-md.md)] .|  
|Comando SQL|Recupere os dados da fonte de dados [!INCLUDE[vstecado](../../includes/vstecado-md.md)] usando uma consulta SQL.|  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Exibição de Dados**. A**visualização** pode exibir até 200 linhas.  
  
> [!NOTE]  
>  Quando você visualiza os dados, as colunas com um tipo de dado CLR definido pelo usuário não contêm dados. Em vez disso, os valores \<valor muito grande para ser exibido> ou exibição de Byte[] de Sistema. O primeiro é exibido quando a fonte de dados é acessada usando o provedor [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , o último ao usar o provedor Native Client do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## Opções dinâmicas de modo de acesso aos dados  
  
### Modo de acesso aos dados = Tabela ou exibição  
 **Nome da tabela ou da exibição**  
 Selecione o nome da tabela ou da exibição na lista de tabelas ou exibições disponíveis na fonte de dados.  
  
### Modo de acesso aos dados = Comando SQL  
 **Texto do comando SQL**  
 Digite o texto de uma consulta SQL, crie a consulta clicando em **Construir Consulta** ou localize o arquivo que contém o texto da consulta clicando em **Procurar**.  
  
 **Construir consulta**  
 Use a caixa de diálogo **Construtor de Consultas** para construir a consulta SQL visualmente.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para localizar o arquivo com contém o texto da consulta SQL.  
  
## Consulte também  
 [Editor de Origem ADO NET &#40;Página Colunas&#41;](../../integration-services/data-flow/ado-net-source-editor-columns-page.md)   
 [Editor de Origem ADO NET &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/ado-net-source-editor-error-output-page.md)   
 [Gerenciador de conexões ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)  
  
  