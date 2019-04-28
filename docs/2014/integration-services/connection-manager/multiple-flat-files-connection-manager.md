---
title: Gerenciador de Conexões de Vários Arquivos Simples | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Multiple Flat Files connection manager
- connections [Integration Services], flat files
- flat files
- flat file connections [Integration Services]
- connection managers [Integration Services], Multiple Flat Files
- multiple flat file connections
ms.assetid: 31fc3f7a-d323-44f5-a907-1fa3de66631a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7235f5f333ac7bb4520a6244e103baafba343ea3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833697"
---
# <a name="multiple-flat-files-connection-manager"></a>Gerenciador de conexões de vários arquivos simples
  Um gerenciador de conexões de Vários Arquivos Simples permite que um pacote acesse dados em vários arquivos simples. Por exemplo, uma fonte de Arquivo Simples pode usar um gerenciador de conexões de Vários Arquivos Simples quando a tarefa Fluxo de Dados está dentro de um contêiner de loop, como o contêiner Loop For. Em cada loop do contêiner, a fonte de Arquivo Simples carrega dados do nome de arquivo seguinte fornecido pelo gerenciador de conexões de Vários Arquivos Simples.  
  
 Quando você adiciona um Gerenciador de conexão de vários arquivos simples a um pacote [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria uma conexão Gerenciador que resolverá uma conexão de vários arquivos simples no tempo de execução, define as propriedades no Gerenciador de conexão de vários arquivos simples, e Adiciona o Gerenciador de conexão de vários arquivos simples para o `Connections` coleção do pacote.  
  
 A propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `MULTIFLATFILE`.  
  
 Você pode configurar o gerenciador de conexões de Vários Arquivos Simples da seguinte maneira:  
  
-   Especifique os arquivos, a localidade e a página de código que serão usados. A localidade é usada para interpretar dados confidenciais de localidade como datas, e a página de código é usada para converter dados de cadeia de caracteres para Unicode.  
  
-   Especifique o formato de arquivo. Você pode usar um formato delimitado, de largura fixa ou irregular à direita.  
  
-   Especifique uma linha de cabeçalho, fila de dados e delimitadores de coluna. Delimitadores de coluna podem ser definidos no nível de arquivo e ser sobrescritos no nível de coluna.  
  
-   Indique se a primeira linha nos arquivos contém nomes de coluna.  
  
-   Especifique um caractere de qualificador de texto. Cada coluna pode ser configurada para reconhecer um qualificador de texto.  
  
-   Defina as propriedades, como o nome, o tipo de dados e a largura máxima em colunas individuais.  
  
 Quando o gerenciador de conexões de Vários Arquivos Simples se refere a vários arquivos, os caminhos dos arquivos são separados pelo caractere de pipe (|). A propriedade `ConnectionString` do gerenciador de conexões tem o seguinte formato:  
  
 \<*path*>|\<*path*>  
  
 Você também pode especificar vários arquivos usando curingas. Por exemplo, a unidade de todos os arquivos de texto em C, o valor de referência a `ConnectionString` propriedade pode ser definida como c:\\*. txt.  
  
 Se um gerenciador de conexões de Vários Arquivos Simples se referir a vários arquivos, todos os arquivos deverão ter o mesmo formato.  
  
 Por padrão, o gerenciador de conexões de Vários Arquivos Simples define o comprimento de colunas de cadeia de caracteres em 50 caracteres. Na caixa de diálogo do **Editor de Gerenciador de Conexões de Vários Arquivos Simples** , você pode avaliar dados de amostra e redimensionar automaticamente o comprimento dessas colunas para evitar truncamento de dados ou excesso de largura de coluna. A menos que você redimensione o comprimento de coluna na fonte de Arquivo Simples ou na transformação, o comprimento da coluna permanecerá o mesmo ao longo do fluxo de dados. Se essas colunas mapearem para colunas de destino mais estreitas, serão exibidos avisos na interface do usuário, e poderão ocorrer erros no tempo de execução, devido a truncamento de dados. Você pode redimensionar as colunas para que sejam compatíveis com as colunas de destino no gerenciador de conexões de Vários Arquivo, na fonte de Arquivo Simples ou em uma transformação. Para modificar o comprimento das colunas de saída, você deve definir a `Length` propriedade da coluna de saída na **propriedades de entrada e saída** guia o **Editor Avançado** caixa de diálogo.  
  
 Se você atualizar os comprimentos de coluna no gerenciador de conexões de Vários Arquivos Simples depois de adicionar e configurar a fonte de Arquivo Simples que usa o gerenciador de conexões, não será necessário redimensionar as colunas de saída manualmente na fonte de Arquivo Simples. Quando você abre a caixa de diálogo **Origem de Arquivo Simples** , a origem de arquivo simples fornece uma opção para sincronizar os metadados da coluna.  
  
## <a name="configuration-of-the-multiple-flat-files-connection-manager"></a>Configuração do gerenciador de conexões de vários arquivos simples  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Geral&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Colunas&#41;](../multiple-flat-files-connection-manager-editor-columns-page.md)  
  
-   [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Avançado&#41;](../multiple-flat-files-connection-manager-editor-advanced-page.md)  
  
-   [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Visualização&#41;](../multiple-flat-files-connection-manager-editor-preview-page.md)  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Consulte também  
 [Origem de Arquivo Simples](../data-flow/flat-file-source.md)   
 [Destino de arquivo simples](../data-flow/flat-file-destination.md)   
 [Conexões do SSIS &#40;Integration Services&#41;](integration-services-ssis-connections.md)  
  
  
