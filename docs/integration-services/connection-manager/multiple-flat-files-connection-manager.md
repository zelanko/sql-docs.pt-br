---
title: "Gerenciador de conex&#245;es de v&#225;rios arquivos simples | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Gerenciador de conexões de vários arquivos simples"
  - "conexões [Integration Services], arquivos simples"
  - "arquivos simples"
  - "conexões de arquivo simples [Integration Services]"
  - "gerenciadores de conexões [Integration Services], vários arquivos simples"
  - "conexões de vários arquivos simples"
ms.assetid: 31fc3f7a-d323-44f5-a907-1fa3de66631a
caps.latest.revision: 41
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 41
---
# Gerenciador de conex&#245;es de v&#225;rios arquivos simples
  Um gerenciador de conexões de Vários Arquivos Simples permite que um pacote acesse dados em vários arquivos simples. Por exemplo, uma fonte de Arquivo Simples pode usar um gerenciador de conexões de Vários Arquivos Simples quando a tarefa Fluxo de Dados está dentro de um contêiner de loop, como o contêiner Loop For. Em cada loop do contêiner, a fonte de Arquivo Simples carrega dados do nome de arquivo seguinte fornecido pelo gerenciador de conexões de Vários Arquivos Simples.  
  
 Quando você adiciona um gerenciador de conexões de Vários Arquivos Simples a um pacote, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que resolverá uma conexão de Vários Arquivos Simples no tempo de execução, define as propriedades no gerenciador de conexões de Vários Arquivos Simples e adiciona o gerenciador de conexões de Arquivos Simples Múltiplos à coleção **Connections** do pacote.  
  
 A propriedade **ConnectionManagerType** do gerenciador de conexões é definida como **MULTIFLATFILE**.  
  
 Você pode configurar o gerenciador de conexões de Vários Arquivos Simples da seguinte maneira:  
  
-   Especifique os arquivos, a localidade e a página de código que serão usados. A localidade é usada para interpretar dados confidenciais de localidade como datas, e a página de código é usada para converter dados de cadeia de caracteres para Unicode.  
  
-   Especifique o formato de arquivo. Você pode usar um formato delimitado, de largura fixa ou irregular à direita.  
  
-   Especifique uma linha de cabeçalho, fila de dados e delimitadores de coluna. Delimitadores de coluna podem ser definidos no nível de arquivo e ser sobrescritos no nível de coluna.  
  
-   Indique se a primeira linha nos arquivos contém nomes de coluna.  
  
-   Especifique um caractere de qualificador de texto. Cada coluna pode ser configurada para reconhecer um qualificador de texto.  
  
-   Defina as propriedades, como o nome, o tipo de dados e a largura máxima em colunas individuais.  
  
 Quando o gerenciador de conexões de Vários Arquivos Simples se refere a vários arquivos, os caminhos dos arquivos são separados pelo caractere de pipe (|). A propriedade **ConnectionString** do gerenciador de conexões tem o seguinte formato:  
  
 \<*path*>|\<*path*>  
  
 Você também pode especificar vários arquivos usando curingas. Por exemplo, para fazer referência a todos os arquivos de texto na unidade C, o valor da propriedade **ConnectionString** pode ser definido como C:\\*.txt.  
  
 Se um gerenciador de conexões de Vários Arquivos Simples se referir a vários arquivos, todos os arquivos deverão ter o mesmo formato.  
  
 Por padrão, o gerenciador de conexões de Vários Arquivos Simples define o comprimento de colunas de cadeia de caracteres em 50 caracteres. Na caixa de diálogo do **Editor de Gerenciador de Conexões de Vários Arquivos Simples** , você pode avaliar dados de amostra e redimensionar automaticamente o comprimento dessas colunas para evitar truncamento de dados ou excesso de largura de coluna. A menos que você redimensione o comprimento de coluna na fonte de Arquivo Simples ou na transformação, o comprimento da coluna permanecerá o mesmo ao longo do fluxo de dados. Se essas colunas mapearem para colunas de destino mais estreitas, serão exibidos avisos na interface do usuário, e poderão ocorrer erros no tempo de execução, devido a truncamento de dados. Você pode redimensionar as colunas para que sejam compatíveis com as colunas de destino no gerenciador de conexões de Vários Arquivo, na fonte de Arquivo Simples ou em uma transformação. Para modificar o comprimento de colunas de saída, você define a propriedade **Length** da coluna de saída na guia **Propriedades de Entrada e Saída** na caixa de diálogo **Editor Avançado** .  
  
 Se você atualizar os comprimentos de coluna no gerenciador de conexões de Vários Arquivos Simples depois de adicionar e configurar a fonte de Arquivo Simples que usa o gerenciador de conexões, não será necessário redimensionar as colunas de saída manualmente na fonte de Arquivo Simples. Quando você abre a caixa de diálogo **Origem de Arquivo Simples** , a origem de arquivo simples fornece uma opção para sincronizar os metadados da coluna.  
  
## Configuração do gerenciador de conexões de vários arquivos simples  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Geral&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)  
  
-   [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Colunas&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)  
  
-   [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Avançado&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)  
  
-   [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Visualização&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## Consulte também  
 [Fonte de Arquivo Simples](../../integration-services/data-flow/flat-file-source.md)   
 [Destino de arquivo simples](../../integration-services/data-flow/flat-file-destination.md)   
 [Conexões do SSIS &#40;Integration Services&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  