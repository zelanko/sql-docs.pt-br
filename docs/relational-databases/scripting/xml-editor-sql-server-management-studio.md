---
title: Editor XML (SQL Server Management Studio) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.editor.xml.f1
- sql13.swb.editorxml.f1
- vs.xmleditor
- sql13.swb.xmleditor.f1
helpviewer_keywords: XML Designer [SQL Server Management Studio]
ms.assetid: 0824a5ce-e67b-4b53-98d9-d371faf2d23c
caps.latest.revision: "27"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: bc3cfd22e1bff42f4ea4730337d01da0c2d5f6a7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="xml-editor-sql-server-management-studio"></a>Editor XML (SQL Server Management Studio)
  Fornece um conjunto de ferramentas visuais para trabalhar com Esquemas XML, conjuntos de dados ADO.NET e documentos XML. O XML Designer oferece suporte para a linguagem de definição de esquema XML (XSD) definida pelo World Wide Web Consortium (WC3). O designer não oferece suporte para DTDs (definições de tipo de documento) ou outras linguagens de esquema XML, como XDR (XML-Data Reduced).  
  
 Para exibir o designer, adicione um conjunto de dados, esquema XML ou arquivo XML a seu projeto ou abra qualquer um dos tipos de arquivo listados na tabela abaixo.  
  
> [!CAUTION]  
>  Não há nenhum comando **Desfazer** ao trabalhar em exibição de Esquema. Planeje seu trabalho cuidadosamente e salve frequentemente seus arquivos.  
  
 O designer fornece as três exibições (ou modos) a seguir, para se trabalhar em arquivos XML, esquemas XML e conjuntos de dados:  
  
|Exibição|Descrição|Tipos de arquivos com suporte|  
|----------|-----------------|--------------------------|  
|**Esquema**|Para criar visualmente e modificar esquemas XML e conjuntos de dados ADO.NET.|.xsd|  
|**Dados**|Para modificar visualmente arquivos de dados XML em uma grade de dados estruturada.|.xml|  
|**XML**|Para editar XML; o editor de fonte fornece codificação de cor e IntelliSense, incluindo Complete Word e List Members.|.xml .xsd .xslt .wsdl.web.resx.tdl.wsf.hta.disco.vsdisco.config|  
|**Plano de Execução**|Exibe planos de consulta xml criados, usando-se a opção SET SHOWPLAN_XML ON.|.showplan|  
  
## <a name="schema-view"></a>Exibição de esquema  
 A exibição de esquema fornece uma representação visual dos elementos, atributos, tipos e assim por diante, que compõem o conjunto de esquemas XML e ADO.NET.  
  
 Em exibição de esquema é possível construir esquemas e conjuntos de dados descartando elementos na superfície do design tanto da guia de esquema XML da caixa de ferramentas quanto do Gerenciador de servidores. Além disso, é possível adicionar elementos ao designer, clicando-se com o botão direito do mouse na superfície de design e selecionando Adicionar no menu de atalho.  
  
 Em exibição de esquema pode você:  
  
-   Construir e modificar esquemas XML e conjuntos de dados ADO.NET existentes  
  
-   Criar e editar relações entre tabelas  
  
-   Criar e editar chaves  
  
-   Gerar conjuntos de dados ADO.NET a partir de esquemas XML  
  
> [!NOTE]  
>  O layout de elementos em exibição de esquema é armazenado no arquivo .xsx, que pode ser visto clicando-se em **Mostrar Todos os Arquivos** na barra de ferramentas Gerenciador de Soluções e, então, expandindo-se o arquivo .xsd. Se não houver nenhum arquivo .xsx, isso significa que o arquivo .xsd nunca foi aberto no XML Designer.  
  
### <a name="customizing-schema-view"></a>Personalizando a exibição de esquema  
 Os recursos a seguir modificam o layout visual de elementos em exibição de esquema:  
  
-   Zoom  
  
-   Expandindo ou recolhendo elementos aninhados  
  
-   Organizando automaticamente layout de elementos  
  
-   Reajustando o estado padrão de elementos recolhidos  
  
##### <a name="to-expand-hidden-nested-elements"></a>Para expandir elementos aninhados ocultos  
  
-   Clique no ícone mais na parte inferior do elemento.  
  
##### <a name="to-collapse-nested-elements"></a>Para recolher elementos aninhados  
  
-   Clique no ícone menos no elemento posicionada na parte mais inferior que você deseja que apareça no designer.  
  
## <a name="data-view"></a>Exibição de dados  
 Exibição de dados fornece uma grade de dados que pode ser usada para modificar arquivos .xml. Somente o conteúdo (mas não as marcas e estrutura) em um arquivo XML pode ser editado em exibição de dados.  
  
 Há duas áreas separadas na Exibição de Dados: **Tabelas de Dados** e **Dados**. A área **Tabela de Dados** é uma lista de relações definidas no arquivo XML, na ordem de seu aninhamento (do mais externo para o mais interno). A área **Dados** é uma grade de dados que exibe dados com base na seleção na área tabela de dados.  
  
> [!NOTE]  
>  Arquivos XML recentemente criados não contêm nenhum dado e, assim, não podem ser exibidos na exibição de Dados. Há também algumas instâncias de documentos XML nas quais a exibição de dados não pode ser invocada. Embora o XML seja considerado bem formado, se não for estruturado dados tentando mudar para exibição de dados irão gerar a seguinte mensagem: "Embora esse documento seja bem formado, ele contém estrutura que a exibição de dados não pode exibir".  
  
 Na exibição de Dados você pode:  
  
-   Popular manualmente tabelas de dados  
  
-   Editar tabelas de dados existentes  
  
-   Gerar um esquema XML a partir de um documento XML  
  
## <a name="xml-view"></a>Exibição XML  
 A exibição XML fornece um editor para edição de XML bruto e, ainda, codificação IntelliSense e de cores. A conclusão de instrução está disponível ao se trabalhar em arquivos .xsd e arquivos .xml que tenham um esquema associado. Digite < para iniciar uma marca e você terá uma lista de elementos válidos naquele local. Depois de digitar o nome do elemento e pressionar SPACEBAR, você terá uma lista de atributos para os quais os elementos oferecem suporte.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense não estão disponíveis na barra de ferramentas. Quando estiver no Editor de XML, clique em **IntelliSense** no menu **Editar**para acessar as opções.  
  
## <a name="showplan-view"></a>Exibição de SHOWPLAN  
 Planos de consulta podem ser salvos em formato XML quando forem criados usando-se a opção SET SHOWPLAN_XML ON. Clique duas vezes em um arquivo com a extensão .showplan para abrir o plano de consulta.  
  
## <a name="see-also"></a>Consulte também  
 [Salvar um plano de execução em formato XML](../../relational-databases/performance/save-an-execution-plan-in-xml-format.md)  
  
  
