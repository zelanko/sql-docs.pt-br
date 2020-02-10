---
title: Editor de origem XML (página Gerenciador de conexões) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmlsourceadapter.connectionmanager.f1
helpviewer_keywords:
- XML Source Editor
ms.assetid: e6507403-a3ce-4b6f-91fc-a7de9f7b6283
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5965c48f91387944f223e1d0cfe666b19aba0e63
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66054303"
---
# <a name="xml-source-editor-connection-manager-page"></a>Editor de Origem XML (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** do **Editor de Origem XML** para especificar um arquivo XML e o XSD que transforma os dados XML.  
  
 Para obter mais informações sobre a origem XML, consulte [XML Source](data-flow/xml-source.md).  
  
## <a name="static-options"></a>Opções estáticas  
 **Modo de acesso aos dados**  
 Especifique o método para selecionar os dados da origem.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|Localização do arquivo XML|Recupera dados de um arquivo XML.|  
|Arquivo XML de variável|Especifica o nome de arquivo XML em uma variável.<br /><br /> **Informações relacionadas**: [usar variáveis em pacotes](../../2014/integration-services/use-variables-in-packages.md)|  
|Dados XML de variável|Recupera dados XML de uma variável.|  
  
 **Usar esquema embutido**  
 Especifique se os próprios dados de origem XML contêm o esquema XSD que define e valida sua estrutura e dados.  
  
 **Local XSD**  
 Digite o caminho e nome de arquivo do esquema de arquivo XSD ou localize o arquivo clicando em **Procurar**.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para localizar o arquivo de esquema XSD.  
  
 **Gerar XSD**  
 Use a caixa de diálogo **Salvar Como** para selecionar um local para o arquivo de esquema XSD gerado automaticamente. O editor infere o esquema da estrutura dos dados XML.  
  
## <a name="data-access-mode-dynamic-options"></a>Opções dinâmicas de modo de acesso aos dados  
  
### <a name="data-access-mode--xml-file-location"></a>Modo de acesso aos dados = local de arquivo XML  
 **Local do XML**  
 Digite o caminho e nome de arquivo do arquivo de dados XML ou localize o arquivo clicando em **Procurar**.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para localizar o arquivo de dados XML.  
  
### <a name="data-access-mode--xml-file-from-variable"></a>Modo de acesso aos dados = arquivo XML de variável  
 **Nome da variável**  
 Selecione a variável que contém o caminho e o nome de arquivo do arquivo XML.  
  
### <a name="data-access-mode--xml-data-from-variable"></a>Modo de acesso aos dados = dados XML de variável  
 **Nome da variável**  
 Selecione uma variável que contenha os dados XML.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de origem XML &#40;página colunas&#41;](../../2014/integration-services/xml-source-editor-columns-page.md)   
 [Editor de origem XML &#40;página saída de erro&#41;](../../2014/integration-services/xml-source-editor-error-output-page.md)   
 [Extrair dados por meio da origem XML](data-flow/extract-data-by-using-the-xml-source.md)  
  
  
