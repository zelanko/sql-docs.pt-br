---
title: Substituir em Arquivos
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Replace in Files dialog box
ms.assetid: 51191c0a-e022-41d6-8473-5cb3c6596862
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d2881ed683a067a65b3ccc068223460dd89f3f9
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243678"
---
# <a name="replace-in-files"></a>Substituir em Arquivos
  A guia **substituir nos arquivos** da janela Localizar e substituir permite que você pesquise o código de um conjunto especificado de arquivos para uma cadeia de caracteres ou expressão e altere algumas ou todas as correspondências encontradas. As correspondências encontradas e as ações tomadas são listadas na janela Localizar Resultados selecionada nas **Opções de Resultados**.  
  
 Também há botões da barra de ferramentas e teclas de atalho disponíveis para abrir a caixa de diálogo **Localizar e Substituir** .  
  
## <a name="find-what"></a>Localizar  
 Esses controles na guia **Substituir nos Arquivos** permitem especificar a cadeia de caracteres ou expressão que será correspondente.  
  
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
 Para substituir instâncias da cadeia de caracteres especificadas em **Localizar** por outra cadeia de caracteres, digite a cadeia de caracteres de substituição nesse campo. Para excluir instâncias da cadeia de caracteres especificadas em **Localizar**, deixe essa caixa em branco. Selecione a lista suspensa para exibir os últimos 20 itens digitados. Para incluir expressões regulares na cadeia de caracteres especificada na caixa **Substituir por** , clique na caixa de seleção **Usar** e na opção **Expressões regulares** .  
  
 **Construtor de expressões**  
 Esse botão triangular ao lado da caixa **Substituir por** torna-se disponível quando a caixa de seleção **Usar** está selecionada nas **Opções de Busca**. Clique nesse botão para exibir uma lista de curingas ou expressões regulares, dependendo da opção **Usar** selecionada. Clicar em qualquer item nessa lista o adiciona à cadeia de caracteres especificada na caixa **Substituir por** .  
  
 **Substitua**  
 Clique nesse botão para substituir a instância atual da cadeia de caracteres especificada em **Localizar** pela cadeia de caracteres especificada na caixa **Substituir por** e localize a próxima instância dentro do escopo especificado em **Examinar**.  
  
 **Substituir tudo**  
 Clique nesse botão para substituir todas as instâncias da cadeia de caracteres especificada em **Localizar** pela cadeia de caracteres especificada na caixa **Substituir por** , em todos os arquivos dentro do escopo especificado em **Examinar**.  
  
> [!CAUTION]  
>  Verifique se **Examinar** está definido para incluir somente os arquivos que você deseja modificar.  
  
 É exibido um lembrete, incluindo uma opção **Manter arquivos modificados abertos** . Para reter a opção **Desfazer** , você deve selecionar essa opção. O recurso **desfazer** só está disponível em arquivos que permanecem abertos para edição depois que eles são modificados.  
  
 **Ignorar arquivo**  
 Torna-se disponível quando **Examinar** inclui vários arquivos. Clique nesse botão se você não quiser pesquisar ou modificar o arquivo atual. A pesquisa continuará no arquivo seguinte na lista em **Examinar**.  
  
## <a name="look-in"></a>Examinar  
 A opção escolhida na lista suspensa **Examinar** determina se a opção **Substituir nos Arquivos** só pesquisará em arquivos ativos ou em todos os arquivos armazenados em determinadas pastas. Selecione um escopo de pesquisa na lista, digite um caminho de pasta ou clique no botão **procurar** para exibir a caixa de diálogo **conjunto de diretórios personalizados** e escolha um conjunto de pastas a serem pesquisadas.  
  
> [!NOTE]  
>  Se a opção **Examinar** selecionada fizer você pesquisar um arquivo do qual foi efetuado check-out do controle do código-fonte, será pesquisada apenas a versão desse arquivo que foi baixada em seu computador local.  
  
 **Examinar**  
 Selecione um escopo da pesquisa predefinido nessa lista ou use a caixa de diálogo **Personalizar Conjunto de Diretórios** para inserir seu próprio conjunto de diretórios.  
  
 **Documento atual**  
 Essa opção fica disponível quando um documento está aberto em um editor. Pesquisa somente o documento ativo para a cadeia de caracteres especificada em **Localizar**.  
  
 **Todos os documentos abertos**  
 Pesquisa todos os arquivos abertos para edição atualmente.  
  
 **Projeto atual**  
 Pesquisa todos os arquivos no projeto ativo.  
  
 **Solução inteira**  
 Pesquisa todos os arquivos na solução ativa.  
  
 **Incluir subpastas**  
 Especifica que serão pesquisadas as subpastas da pasta especificada em **Examinar** . Isso requer um conjunto de diretórios personalizados.  
  
 **Procurar (...)**  
 Clique nesse botão para exibir a caixa de diálogo **Escolher Pastas de Pesquisa**, na qual é possível reunir, editar, salvar e selecionar conjuntos nomeados de diretórios para digitar na caixa **Examinar**.  
  
## <a name="find-options"></a>Opções de Busca  
 Você pode expandir ou recolher a seção **Opções de Busca** . As opções seguintes podem ser marcadas ou desmarcadas.  
  
 **Diferenciar caso**  
 Quando essa caixa é selecionada, as janelas Localizar Resultados só exibem instâncias da cadeia de caracteres especificada em **Localizar** que correspondam tanto no conteúdo como nas letras maiúsculas e minúsculas. Por exemplo, uma pesquisa por **MyObject** com a caixa de seleção **diferenciar maiúsculas de minúsculas** retornará "MyObject", mas não "MYOBJECT" ou "MyObject".  
  
 **Coincidir palavra inteira**  
 Quando essa caixa é selecionada, as janelas Localizar Resultados só exibem instâncias da cadeia de caracteres especificada em **Localizar** que correspondam a palavras completas. Por exemplo, uma pesquisa por **MyObject** retornará "MyObject" mas não "CMyObject" nem "MyObjectC".  
  
 **Utilizá**  
 Indica como interpretar caracteres especiais digitados nas caixas de texto **Localizar** ou **Substituir por** . As opções incluem **Curingas** e **Expressões Regulares**.  
  
 **Expressões regulares**  
 Notações especiais definem padrões de texto para correspondência. Para obter uma lista, veja [Pesquisar texto com expressões regulares](search-text-with-regular-expressions.md).  
  
 **Caracteres curinga**  
 Caracteres especiais, como asteriscos (`*`) e pontos de interrogação (`?`) representam um ou mais caracteres. Para obter uma lista, veja [Pesquisar texto com curingas](search-text-with-wildcards.md).  
  
 **Examinar esses tipos de arquivo**  
 Essa lista indica os tipos de arquivos a serem pesquisados nos diretórios especificados em **Examinar**. Se essa caixa ficar em branco, todos os arquivos nos diretórios especificados em **Examinar** serão pesquisados.  
  
```  
*.[ext]; *.[ext] (manual)  
```  
  
 Para localizar arquivos de um determinado tipo, insira um curinga asterisco (`*`) para o nome do arquivo, seguido de um ponto final (`.`) e a extensão do arquivo. Para localizar mais de um tipo de arquivo, insira várias cadeias de caracteres de pesquisa separadas por ponto-e-vírgula (`;`).  
  
```  
*.[ext]; *.[ext] (from list)  
```  
  
 Selecione qualquer item na lista para inserir uma cadeia de caracteres de pesquisa pré-configurada que localizará arquivos de tipos específicos.  
  
## <a name="result-options"></a>Opções de Resultados  
 Você pode expandir ou recolher a seção **Opções de Resultados** . As opções seguintes podem ser marcadas ou desmarcadas.  
  
 **Janela Localizar resultados 1**  
 Quando essa caixa de seleção estiver marcada, os resultados da pesquisa atual serão anexados ao conteúdo da janela Localizar Resultados 1. Essa janela será aberta automaticamente para exibir seus resultados de pesquisa. Para abrir essa janela manualmente, clique em **Outras Janelas** no menu **Exibir** e clique em **Localizar Resultados 1**.  
  
 **Janela Localizar resultados 2**  
 Quando essa caixa está selecionada, os resultados da pesquisa atual são anexados ao conteúdo da janela Localizar Resultados 2. Essa janela será aberta automaticamente para exibir seus resultados de pesquisa. Para abrir essa janela manualmente, clique em **Outras Janelas** no menu **Exibir** e clique em **Localizar Resultados 2**.  
  
 **Exibir somente nomes de arquivos**  
 Exibe uma entrada por arquivo contendo uma correspondência de pesquisa em vez de uma entrada por correspondência de pesquisa na janela Localizar Resultados 1 ou Localizar Resultados 2. Essa opção não está disponível no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Manter arquivos modificados abertos depois de substituir tudo**  
 Quando selecionada, essa opção deixa abertos todos os arquivos em que foram feitas substituições, para você poder desfazer ou salvar as alterações. Restrições de memória podem limitar o número de arquivos que podem permanecer abertos após uma operação de substituição.  
  
> [!CAUTION]  
>  Você só pode usar o comando **Desfazer** em arquivos que permaneçam abertos para edição. Se essa opção não for selecionada, os arquivos que ainda não estiverem abertos para edição continuarão fechados e nenhuma opção **Desfazer** ficará disponível para eles.  
  
## <a name="find-and-replace-views"></a>Localizar e substituir exibições  
 As guias no topo da janela Localizar e Substituir incluem menus **Exibir** . Esses menus permitem escolher um conjunto de campos para serem exibidos no painel ativo. É possível deixar a janela Localizar e Substituir encaixada em um local conveniente e mudar de guia para guia e de exibição para exibição a fim de executar qualquer tipo de operação de localização e substituição.  
  
 **Alternar para localização rápida**  
 Essa barra de ferramentas altera a caixa de diálogo para uma caixa de diálogo **Localização Rápida** .  
  
 **Alternar para localizar nos arquivos**  
 Essa barra de ferramentas altera a caixa de diálogo para uma caixa de diálogo **Localizar nos Arquivos** .  
  
 **Alternar para localizar símbolos**  
 Essa barra de ferramentas altera a caixa de diálogo para uma caixa de diálogo **Localizar Símbolos** .  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Management Studio atalhos de teclado](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)  
