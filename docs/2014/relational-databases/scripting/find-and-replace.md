---
title: Localizar e Substituir
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Find and Replace dialog box
ms.assetid: 09297893-d80b-4c88-86b4-52bfb639e521
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c3d96670edc599a1f16456b862922dc6378b1362
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245150"
---
# <a name="find-and-replace"></a>Localizar e Substituir
  Use a caixa de diálogo **Localizar e substituir** para localizar texto em um arquivo e, opcionalmente, substituí-lo. Versões da caixa de diálogo **Localizar e Substituir** com opções ligeiramente diferentes podem aparecer, dependendo da maneira como a caixa de diálogo foi aberta. No menu **Editar** , aponte para **Localizar e Substituir**e clique em **Localização Rápida** para abrir a caixa de diálogo com opções de localização, mas sem opções de substituição. No menu **Editar** , aponte para **Localizar e Substituir**e clique em **Substituição Rápida** para abrir a caixa de diálogo com opções de localização e de substituição.  
  
 Também há botões da barra de ferramentas e teclas de atalho disponíveis para abrir a caixa de diálogo **Localizar e Substituir** .  
  
## <a name="find-what"></a>Localizar  
 Esses controles lhe permitem especificar a cadeia de caracteres ou expressão para as quais haverá correspondência.  
  
 **Localizar**  
 Digite o texto a procurar. A caixa de diálogo tenta preencher um texto de pesquisa provável, usando o texto selecionado com o cursor antes de a caixa de diálogo ser aberta, um texto próximo a ele ou um texto pesquisado anteriormente. Você pode reutilizar uma das últimas 20 cadeias de caracteres pesquisadas selecionando-a nessa lista suspensa.  
  
 **[cadeia de caracteres com curingas]**  
 Para usar curingas, como asteriscos (`*`) e pontos de interrogação (`?`), em sua cadeia de caracteres de pesquisa, marque a caixa de seleção **Usar** em **Opções de Busca** e clique em **Curingas**.  
  
 **[expressão regular]**  
 Para fazer com que o mecanismo de pesquisa interprete a sua cadeia de caracteres de pesquisa como uma expressão regular, marque a caixa de seleção **Usar** em **Opções de Busca** e clique em **Expressões regulares**.  
  
 **Construtor de expressões**  
 Esse botão triangular ao lado da caixa **Localizar** torna-se disponível quando a caixa de seleção **Usar** é selecionada nas **Opções de Busca**. Clique nesse botão para exibir uma lista de curingas ou expressões regulares, dependendo da opção **Usar** selecionada. Escolher qualquer item dessa lista o adiciona à cadeia de caracteres especificada na caixa **Localizar** .  
  
## <a name="replace-with"></a>Substitua por  
 Esses controles permitem que você especifique o que será inserido no lugar da cadeia de caracteres ou expressão correspondente.  
  
 **Substituir por**  
 Para substituir instâncias da cadeia de caracteres especificadas em **Localizar** por outra cadeia de caracteres, digite a cadeia de caracteres de substituição nesse campo. Para excluir instâncias do texto especificadas em **Localizar**, deixe esse espaço em branco. Selecione a lista suspensa para exibir os últimos 20 itens digitados. Para incluir expressões regulares na cadeia de caracteres especificada na caixa **Substituir por** clique na caixa de seleção **Usar** e, então, clique em **Expressões regulares**. Essa caixa aparece apenas se essa caixa de diálogo foi aberta clicando-se em **Substituição Rápida**.  
  
 **Substituir por**  
 Para substituir instâncias da cadeia de caracteres especificadas na caixa **Localizar** por outra cadeia de caracteres, digite a cadeia de caracteres substituta nesse campo. Para excluir instâncias da cadeia de caracteres especificadas na caixa **Localizar** deixe esse campo em branco. Selecione a lista suspensa para exibir os últimos 20 itens digitados. Para incluir expressões regulares na cadeia de caracteres especificada na caixa **Substituir por** clique na caixa de seleção **Usar** e, então, clique em **Expressões regulares**.  
  
 **Construtor de expressões**  
 Esse botão triangular ao lado da caixa **Substituir por** torna-se disponível quando a caixa de seleção **Usar** está selecionada nas **Opções de Busca**. Clique nesse botão para exibir uma lista de curingas ou expressões regulares, dependendo da opção **Usar** selecionada. Clicar em qualquer item nessa lista o adiciona à cadeia de caracteres especificada na caixa **Substituir por** .  
  
 **Substitua**  
 Clique nesse botão para substituir a instância atual da cadeia de caracteres especificada na caixa **Localizar** pela cadeia de caracteres especificada na caixa **Substituir por** e localize a próxima instância dentro do escopo especificado em **Examinar**.  
  
 **Substituir tudo**  
 Clique nesse botão para substituir todas as instâncias da cadeia de caracteres especificada na caixa **Localizar** pela cadeia de caracteres especificada na caixa **Substituir por** em todos os arquivos dentro do escopo especificado na caixa **Examinar** .  
  
> [!CAUTION]  
>  Verifique se **Examinar** está definido para incluir somente os arquivos que você deseja modificar.  
  
 É exibido um lembrete, incluindo uma opção **Manter arquivos modificados abertos** . Para reter a opção **Desfazer** , você deve selecionar essa opção. O recurso **desfazer** só está disponível em arquivos que permanecem abertos para edição depois que eles são modificados.  
  
 **Ignorar arquivo**  
 Fica disponível quando o valor especificado para **Examinar** incluir vários arquivos. Clique nesse botão se você não quiser pesquisar ou modificar o arquivo atual. A pesquisa continuará no arquivo seguinte na lista em **Examinar**.  
  
## <a name="look-in"></a>Examinar  
 **Examinar**  
 Selecione o local para procurar o texto especificou em **Localizar**. As opções são **Documento Atual**, que pesquisa a janela do documento em foco quando a caixa de diálogo estava aberta, e **Todos os Documentos Abertos**, que pesquisa todas as janelas de documentos abertas no momento no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="find-options"></a>Opções de Busca  
 Você pode expandir ou recolher a seção **Opções de Busca** . As opções seguintes podem ser marcadas ou desmarcadas.  
  
 **Diferenciar caso**  
 Quando essa caixa é selecionada, as janelas Localizar Resultados só exibem instâncias da cadeia de caracteres especificada em **Localizar** que correspondam tanto no conteúdo como nas letras maiúsculas e minúsculas. Por exemplo, uma pesquisa por "**MyObject**" com a caixa de seleção **diferenciar maiúsculas de minúsculas** retornará "MyObject", mas não "MYOBJECT" ou "MyObject".  
  
 **Coincidir palavra inteira**  
 Quando essa caixa é selecionada, as janelas Localizar Resultados só exibem instâncias da cadeia de caracteres especificada em **Localizar** que coincidam em palavras completas. Por exemplo, uma pesquisa por **MyObject** retornará "MyObject" mas não "CMyObject" nem "MyObjectC".  
  
 **Pesquisar acima**  
 Pesquise a partir do local do cursor em direção ao início do documento.  
  
 **Pesquisar texto oculto**  
 Localize instâncias do texto que sejam texto oculto e recolhido.  
  
 **Utilizá**  
 Indica como interpretar caracteres especiais digitados nas caixas de texto **Localizar** ou **Substituir por** . As opções incluem **Curingas** e **Expressões Regulares**.  
  
 **Expressões regulares**  
 Notações especiais definem padrões de texto para correspondência. Para obter uma lista, veja [Pesquisar texto com expressões regulares](search-text-with-regular-expressions.md).  
  
 **Caracteres curinga**  
 Caracteres especiais, como asteriscos (`*`) e pontos de interrogação (`?`) representam um ou mais caracteres. Para obter uma lista, veja [Pesquisar texto com curingas](search-text-with-wildcards.md).  
  
 **Localizar próximo**  
 Começa a procurar pelo texto na caixa **Localizar** .  
  
 **Substitua**  
 Clique nesse botão para substituir a instância atual da cadeia de caracteres especificada em **Localizar** pela cadeia de caracteres especificada em **Substituir por**e localize a próxima instância dentro do escopo especificado em **Examinar**.  
  
 **Substituir tudo**  
 Escolha esse botão para substituir todas as instâncias da cadeia de caracteres especificada em **Localizar** pela cadeia de caracteres especificada em **Substituir por**em todos os arquivos dentro do escopo especificado em **Examinar**.  
  
> [!CAUTION]  
>  Verifique se **Examinar** está definido para incluir somente os arquivos que você deseja modificar.  
  
## <a name="find-and-replace-views"></a>Localizar e substituir exibições  
 As guias no topo da janela Localizar e Substituir incluem menus **Exibir** . Esses menus permitem escolher um conjunto de campos para serem exibidos no painel ativo. Você pode deixar a janela **Localizar e Substituir** encaixada em um local conveniente e depois mudar de guia para guia e de exibição para exibição a fim de fazer qualquer tipo de operação de localizar e substituir.  
  
 **Localização rápida**  
 Essa barra de ferramentas altera a caixa de diálogo para uma caixa de diálogo **Localização Rápida** .  
  
 **Localizar nos arquivos**  
 Essa barra de ferramentas altera a caixa de diálogo para uma caixa de diálogo **Localizar nos Arquivos** .  
  
 **Substituição rápida**  
 Essa barra de ferramentas altera a caixa de diálogo para uma caixa de diálogo **Substituição Rápida**  
  
 **Substituir nos arquivos**  
 Essa barra de ferramentas altera a caixa de diálogo para uma caixa de diálogo **Substituir nos Arquivos**  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Management Studio atalhos de teclado](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)  
