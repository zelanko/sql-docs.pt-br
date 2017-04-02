---
title: "Editor de Origem XML (p&#225;gina Gerenciador de Conex&#245;es) | Microsoft Docs"
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
  - "sql13.dts.designer.xmlsourceadapter.connectionmanager.f1"
helpviewer_keywords: 
  - "Editor de Origem XML"
ms.assetid: e6507403-a3ce-4b6f-91fc-a7de9f7b6283
caps.latest.revision: 20
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 20
---
# Editor de Origem XML (p&#225;gina Gerenciador de Conex&#245;es)
  Use a página **Gerenciador de Conexões** do **Editor de Origem XML** para especificar um arquivo XML e o XSD que transforma os dados XML.  
  
 Para obter mais informações sobre a origem XML, consulte [XML Source](../../integration-services/data-flow/xml-source.md).  
  
## Opções estáticas  
 **Modo de acesso aos dados**  
 Especifique o método para selecionar os dados da origem.  
  
|Value|Description|  
|-----------|-----------------|  
|Localização do arquivo XML|Recupera dados de um arquivo XML.|  
|Arquivo XML de variável|Especifica o nome de arquivo XML em uma variável.<br /><br /> **Informações relacionadas**: [Usar variáveis em pacotes](../Topic/Use%20Variables%20in%20Packages.md)|  
|Dados XML de variável|Recupera dados XML de uma variável.|  
  
 **Usar esquema embutido**  
 Especifique se os próprios dados de origem XML contêm o esquema XSD que define e valida sua estrutura e dados.  
  
 **Local de XSD**  
 Digite o caminho e nome de arquivo do esquema de arquivo XSD ou localize o arquivo clicando em **Procurar**.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para localizar o arquivo de esquema XSD.  
  
 **Gerar XSD**  
 Use a caixa de diálogo **Salvar Como** para selecionar um local para o arquivo de esquema XSD gerado automaticamente. O editor infere o esquema da estrutura dos dados XML.  
  
## Opções dinâmicas de modo de acesso aos dados  
  
### Modo de acesso aos dados = local de arquivo XML  
 **Local de XML**  
 Digite o caminho e nome de arquivo do arquivo de dados XML ou localize o arquivo clicando em **Procurar**.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para localizar o arquivo de dados XML.  
  
### Modo de acesso aos dados = arquivo XML de variável  
 **Nome da variável**  
 Selecione a variável que contém o caminho e o nome de arquivo do arquivo XML.  
  
### Modo de acesso aos dados = dados XML de variável  
 **Nome da variável**  
 Selecione uma variável que contenha os dados XML.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de Origem XML &#40;Página Colunas&#41;](../../integration-services/data-flow/xml-source-editor-columns-page.md)   
 [Editor de Origem XML &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/xml-source-editor-error-output-page.md)   
 [Extrair dados por meio da origem XML](../../integration-services/data-flow/extract-data-by-using-the-xml-source.md)  
  
  