---
title: Localizar em Arquivos
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Find in Files dialog box
ms.assetid: bf92770a-33df-43ef-85ad-5a9223649b98
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b3b3ccbab2d77f92fe9d28ae616939b8fa02ea4c
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245174"
---
# <a name="find-in-files"></a>Localizar em Arquivos
  A guia **localizar nos arquivos** da janela Localizar e substituir permite que você pesquise o código de um conjunto especificado de arquivos para uma cadeia de caracteres ou expressão. As correspondências encontradas e as ações tomadas são listadas na janela Localizar Resultados selecionada nas **Opções de Resultados**.  
  
 Também há botões da barra de ferramentas e teclas de atalho disponíveis para abrir a caixa de diálogo **Localizar e Substituir** .  
  
 As seções a seguir listam os controles disponíveis na guia **Localizar nos Arquivos** .  
  
## <a name="find-what"></a>Localizar  
 Esses controles da guia **Localizar nos Arquivos** permitem especificar a cadeia de caracteres ou expressão que será procurada.  
  
 **Localizar**  
 Digite o texto a procurar. A caixa de diálogo tenta preencher um texto de pesquisa provável, usando o texto selecionado com o cursor antes de a caixa de diálogo ser aberta, um texto próximo a ele ou um texto pesquisado anteriormente. Você pode reutilizar uma das últimas 20 cadeias de caracteres pesquisadas selecionando-a nessa lista suspensa.  
  
 **[cadeia de caracteres com curingas]**  
 Para usar curingas, como asteriscos (`*`) e pontos de interrogação (`?`), em sua cadeia de caracteres de pesquisa, marque a caixa de seleção **Usar** em **Opções de Busca** e clique em **Curingas**.  
  
 **[expressão regular]**  
 Para fazer com que o mecanismo de pesquisa interprete a sua cadeia de caracteres de pesquisa como uma expressão regular, marque a caixa de seleção **Usar** em **Opções de Busca** e clique em **Expressões regulares**.  
  
 **Construtor de expressões**  
 Esse botão triangular ao lado da caixa **Localizar** torna-se disponível quando a caixa de seleção **Usar** é selecionada nas **Opções de Busca**. Clique nesse botão para exibir uma lista de curingas ou expressões regulares, dependendo da opção **Usar** selecionada. A escolha de qualquer item nessa lista o adiciona à cadeia de caracteres em **Localizar** .  
  
## <a name="look-in"></a>Examinar  
 A opção escolhida na lista suspensa **Examinar** determina se a opção **Localizar nos Arquivos** só pesquisará em arquivos ativos ou em todos os arquivos armazenados em determinadas pastas. Selecione um escopo da pesquisa na lista, digite um caminho da pasta ou clique no botão **Procurar** para exibir a caixa de diálogo **Personalizar Conjunto de Diretórios** e escolha um conjunto de pastas a ser pesquisado.  
  
> [!NOTE]  
>  Se a opção **Examinar** selecionada fizer você pesquisar um arquivo do qual foi efetuado check-out do controle do código-fonte, será pesquisada apenas a versão desse arquivo que foi baixada em seu computador local.  
  
 **Examinar**  
 Selecione um escopo da pesquisa predefinido nessa lista ou use a caixa de diálogo **Personalizar Conjunto de Diretórios** para inserir seu próprio conjunto de diretórios.  
  
 **Documento atual**  
 Essa opção fica disponível quando um documento está aberto em um editor. Ela pesquisa apenas o documento ativo para a cadeia de caracteres em **Localizar**.  
  
 **Todos os documentos abertos**  
 Pesquisa todos os arquivos abertos para edição atualmente.  
  
 **Projeto atual**  
 Pesquisa todos os arquivos no projeto ativo.  
  
 **Solução inteira**  
 Pesquisa todos os arquivos na solução ativa.  
  
 **Incluir subpastas**  
 Especifica que serão pesquisadas as subpastas da pasta especificada em **Examinar** . Isso requer um conjunto de diretórios personalizados.  
  
 **Procurar**  
 Clique nesse botão para exibir a caixa de diálogo **Personalizar Conjunto de Diretórios** , na qual é possível reunir, editar, salvar e selecionar conjuntos nomeados de diretórios a serem inseridos na caixa **Examinar** .  
  
## <a name="find-options"></a>Opções de Busca  
 Você pode expandir ou recolher a seção **Opções de Busca** . As opções seguintes podem ser marcadas ou desmarcadas.  
  
 **Diferenciar caso**  
 Quando essa caixa é selecionada, as janelas Localizar Resultados só exibem instâncias da cadeia de caracteres especificada em **Localizar** que correspondam tanto no conteúdo como nas letras maiúsculas e minúsculas. Por exemplo, uma pesquisa por **MyObject** com a caixa de seleção **Diferenciar maiúsculas de minúsculas** retornará “MyObject”, mas não “myobject” nem “MYOBJECT”.  
  
 **Coincidir palavra inteira**  
 Quando essa caixa é selecionada, as janelas Localizar Resultados só exibem instâncias da cadeia de caracteres especificada em **Localizar** que correspondam a palavras completas. Por exemplo, uma pesquisa por **MyObject** retornará "MyObject" mas não "CMyObject" nem "MyObjectC".  
  
 **Utilizá**  
 Indica como interpretar caracteres especiais digitados nas caixas de texto **Localizar** ou **Substituir por** . As opções incluem **Curingas** e **Expressões Regulares**.  
  
 **Expressões regulares**  
 Notações especiais definem padrões de texto para correspondência. Para obter uma lista, veja [Pesquisar texto com expressões regulares](search-text-with-regular-expressions.md).  
  
 **Caracteres curinga**  
 Caracteres especiais, como asteriscos (`*`) e pontos de interrogação (`?`) representam um ou mais caracteres. Para obter uma lista, veja [Pesquisar texto com curingas](search-text-with-wildcards.md).  
  
 **Examinar esses tipos de arquivo**  
 Essa lista indica os tipos de arquivos a serem pesquisados nos diretórios especificados em **Examinar**. Se esse campo ficar em branco, serão pesquisados todos os arquivos nos diretórios especificados em **Examinar** .  
  
```  
*.[ext]; *.[ext] (manual)  
```  
  
 Para localizar arquivos de um determinado tipo, insira um curinga asterisco (`*`) para o nome do arquivo, seguido de um ponto final (`.`) e a extensão do arquivo. Para localizar mais de um tipo de arquivo, insira várias cadeias de caracteres de pesquisa separadas por ponto-e-vírgula (`;`).  
  
```  
*.[ext]; *.[ext] (from list)  
```  
  
 Selecione qualquer item na lista para inserir uma cadeia de caracteres de pesquisa pré-configurada que localizará arquivos de tipos específicos.  
  
## <a name="result-options"></a>Opções de Resultados  
 Determina o local dos resultados quando você clica em **Localizar Tudo**. Você pode expandir ou recolher a seção **Opções de Resultados** . As opções seguintes podem ser marcadas ou desmarcadas.  
  
 **Janela Localizar resultados 1**  
 Quando essa caixa de seleção estiver marcada, os resultados da pesquisa atual serão anexados ao conteúdo da janela Localizar Resultados 1. Essa janela será aberta automaticamente para exibir seus resultados de pesquisa. Para abrir essa janela manualmente, clique em **Outras Janelas** no menu **Exibir** e clique em **Localizar Resultados 1**.  
  
 **Janela Localizar resultados 2**  
 Quando essa caixa for selecionada, os resultados da pesquisa atual serão anexados ao conteúdo da janela Localizar Resultados 2. Essa janela será aberta automaticamente para exibir seus resultados de pesquisa. Para abrir essa janela manualmente, clique em **Outras Janelas** no menu **Exibir** e clique em **Localizar Resultados 2**.  
  
 **Exibir somente nomes de arquivos**  
 Exibe uma entrada por arquivo contendo uma correspondência de pesquisa em vez de uma entrada por correspondência de pesquisa na janela Localizar Resultados 1 ou Localizar Resultados 2. Essa opção não está disponível no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Manter arquivos modificados abertos depois de substituir tudo**  
 Quando selecionada, essa opção deixa abertos todos os arquivos em que foram feitas substituições, para você poder desfazer ou salvar as alterações. Restrições de memória podem limitar o número de arquivos que podem permanecer abertos após uma operação de substituição.  
  
> [!CAUTION]  
>  Você só pode usar o comando **Desfazer** em arquivos que permaneçam abertos para edição. Se essa opção não for selecionada, os arquivos que ainda não estiverem abertos para edição continuarão fechados e nenhuma opção **Desfazer** ficará disponível para eles.  
  
## <a name="find-and-replace-views"></a>Localizar e substituir exibições  
 As guias no topo da janela Localizar e Substituir incluem menus **Exibir** . Esses menus permitem escolher um conjunto de campos para serem exibidos no painel ativo. Você pode deixar a janela Localizar e Substituir encaixada em um local conveniente e depois mudar de guia para guia e de exibição para exibição a fim de fazer qualquer tipo de operação de localizar e substituir.  
  
 **Alternar para localização rápida**  
 Essa barra de ferramentas altera a caixa de diálogo para uma caixa de diálogo **Localização Rápida** .  
  
 **Alternar para localizar nos arquivos**  
 Essa barra de ferramentas altera a caixa de diálogo para uma caixa de diálogo **Localizar nos Arquivos** .  
  
 **Alternar para localizar símbolos**  
 Essa barra de ferramentas altera a caixa de diálogo para uma caixa de diálogo **Localizar Símbolos** .  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Management Studio atalhos de teclado](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)  
