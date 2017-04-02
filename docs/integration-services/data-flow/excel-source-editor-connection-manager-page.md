---
title: "Editor de Origem do Excel (p&#225;gina Gerenciador de Conex&#245;es) | Microsoft Docs"
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
  - "sql13.dts.designer.excelsourceadapter.connection.f1"
helpviewer_keywords: 
  - "Editor de Origem do Excel"
ms.assetid: 428e04e0-ad98-45d0-8345-12ec1b67b2eb
caps.latest.revision: 39
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 39
---
# Editor de Origem do Excel (p&#225;gina Gerenciador de Conex&#245;es)
  Use o nó **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem do Excel** para selecionar a pasta de trabalho do [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] para a origem que será usada. A origem do Excel lê os dados de uma planilha ou intervalo nomeado em uma pasta de trabalho existente.  
  
> [!NOTE]  
>  A propriedade **CommandTimeout** da origem do Excel não está disponível no **Editor de Origem do Excel**, mas ela pode ser definida usando o **Editor Avançado**. Para obter mais informações sobre esta propriedade, consulte a seção Origem do Excel em [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md).  
  
 Para obter mais informações sobre origem do Excel, consulte [Excel Source](../../integration-services/data-flow/excel-source.md).  
  
## Opções estáticas  
 **gerenciador de conexões OLE DB**  
 Selecione um gerenciador de conexões do Excel existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Gerenciador de Conexões do Excel**.  
  
 **Modo de acesso aos dados**  
 Especifique o método para selecionar os dados da origem.  
  
|Value|Description|  
|-----------|-----------------|  
|Tabela ou exibição|Recupere dados de uma planilha ou intervalo nomeado no arquivo do Excel.|  
|Nome da tabela ou variável do nome de exibição|Especifique a planilha ou o nome do intervalo em uma variável.<br /><br /> **Informações relacionadas:** [Usar variáveis em pacotes](../Topic/Use%20Variables%20in%20Packages.md)|  
|Comando SQL|Recupere os dados do arquivo do Excel usando uma consulta SQL. Para obter mais informações sobre a sintaxe da consulta, consulte [Excel Source](../../integration-services/data-flow/excel-source.md).|  
|Comando SQL a partir da variável|Especifique o texto da consulta SQL em uma variável.|  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Exibição de Dados**. A visualização pode exibir até 200 linhas.  
  
## Opções dinâmicas de modo de acesso aos dados  
  
### Modo de acesso aos dados = Tabela ou exibição  
 **Nome da planilha do Excel**  
 Selecione o nome da planilha ou o intervalo nomeado na lista disponível na pasta de trabalho do Excel.  
  
### Modo de acesso aos dados = Variável do nome da tabela ou do nome de exibição  
 **Nome da variável**  
 Selecione a variável que contém o nome da planilha ou do intervalo nomeado.  
  
### Modo de acesso aos dados = Comando SQL  
 **Texto do comando SQL**  
 Insira o texto de uma consulta SQL, crie a consulta clicando em **Construir Consulta** ou procure o arquivo que contém o texto da consulta clicando em **Procurar**.  
  
 **Parâmetros**  
 Se você inseriu uma consulta parametrizada usando ? como um espaço reservado para o parâmetro no texto da consulta, use a caixa de diálogo **Definir Parâmetros da Consulta** para mapear os parâmetros de entrada da consulta para as variáveis do pacote.  
  
 **Construir consulta**  
 Use a caixa de diálogo **Construtor de Consultas** para construir a consulta SQL visualmente.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para localizar o arquivo com contém o texto da consulta SQL.  
  
 **Analisar consulta**  
 Verifique a sintaxe do texto da consulta.  
  
### Modo de acesso aos dados = Comando SQL a partir da variável  
 **Nome da variável**  
 Selecione a variável que contém o texto da consulta SQL.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de Fonte do Excel &#40;Página Colunas&#41;](../../integration-services/data-flow/excel-source-editor-columns-page.md)   
 [Editor de Origem do Excel &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/excel-source-editor-error-output-page.md)   
 [Gerenciador de conexões do Excel](../../integration-services/connection-manager/excel-connection-manager.md)   
 [Loop através de arquivos e tabelas do Excel por meio de um contêiner Loop Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  