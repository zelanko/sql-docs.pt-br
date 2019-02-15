---
title: Visualizando relatórios no Construtor de Relatórios | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ba6b5bdd-d8c6-4aa8-ba32-3a10b11969d4
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: adbe8e9271ad3f8d71c3463222c5970f367e1286
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56292604"
---
# <a name="previewing-reports-in-report-builder"></a>Visualizando relatórios no Construtor de Relatórios
  Durante a criação de um relatório, é útil visualizar o relatório frequentemente para verificar se o relatório exibe o que você deseja. Para visualizar o relatório, clique em **Executar**. O relatório é renderizado no modo de visualização.  
  
 O Construtor de Relatórios melhora a experiência de visualização usando sessões de edição quando conectado a um servidor de relatório. A sessão de edição cria um cache de dados e torna os conjuntos de dados no cache disponíveis para visualizações de relatório repetidas. Uma sessão de edição não é um recurso com o qual você interage diretamente, mas entender quando o conjunto de dados armazenado em cache é atualizado o ajudará a melhorar desempenho durante a visualização de um relatório e para entender por que o relatório é renderizado mais rapidamente ou mais lentamente.  
  
 Outros benefícios das sessões de edição são os recursos de edição de relatórios que usam fontes de dados inseridas ou itens de referência, como imagens ou sub-relatórios armazenados no servidor de relatório.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="improving-preview-performance"></a>Aprimorando o desempenho da visualização  
 O modo como você cria e atualiza relatórios afeta a rapidez com que o relatório é renderizado na visualização. A primeira vez que você visualiza um relatório que depende de uma referência de servidor, uma sessão de edição é criada e os dados usados durante a execução do relatório são adicionados a um cache de dados armazenado no servidor de relatório. Quando você fizer alterações no relatório que não afetem os dados, a cópia armazenada em cache dos dados será usada pelo relatório. Isso significa que você não visualizará a alteração de dados cada vez que visualiza o relatório. Se você desejar novos dados, clique no botão **Atualizar** na faixa de opções.  
  
 As ações seguintes fazem com que o cache seja atualizado e tornam a renderização de relatório mais lenta na próxima vez que você visualiza o relatório:  
  
-   Adicione, altere ou exclua um banco de dados. O conjunto de dados armazenado em cache contém todos os conjuntos de dados que um relatório usa e a modificação de qualquer conjunto de dados invalida o conjunto de dados armazenado em cache. Isso inclui alterar o nome, a consulta ou os campos no conjunto de dados.  
  
    > [!NOTE]  
    >  Se o conjunto de dados tiver um número grande de campos que você não espera usar, considere atualizar o conjunto de dados para omitir esses campos. Embora isso crie uma nova sessão de edição e a primeira visualização do relatório seja mais lento, o conjunto de dados armazenado em cache menor será benéfico em geral para o desempenho do servidor de relatório.  
  
-   Adicione, altere ou exclua uma fonte de dados. Isso inclui alterar o nome ou as propriedades da fonte de dados, a extensão de dados da fonte de dados ou as propriedades de conexão com a fonte de dados.  
  
-   Altere a fonte de dados compartilhada que o relatório usa para diferenciar a fonte de dados.  
  
-   Altere o idioma do relatório.  
  
-   Altere os assemblies ou o código personalizado usado pelo relatório.  
  
-   Adicione, altere ou exclua os parâmetros de consulta no relatório ou nos valores de parâmetros.  
  
 As alterações feitas no layout de relatório e na formatação de dados não afeta o conjunto de dados armazenado em cache. Você pode executar as seguintes ações sem atualizar o conjunto de dados armazenado em cache:  
  
-   Adicione ou remova regiões de dados como tabelas, matrizes ou gráficos.  
  
-   Adicione ou exclua colunas do relatório. Todos os campos no conjunto de dados estão disponíveis para uso no relatório. A adição ou a remoção de campos no relatório não tem nenhum efeito no conjunto de dados.  
  
-   Altere a ordem dos campos em tabelas e matrizes.  
  
-   Adicione, altere ou exclua grupos de linhas e colunas.  
  
-   Adicione, altere ou exclua a formatação de valores de dados em campos.  
  
-   Adicione, altere ou exclua imagens, linhas ou caixas de texto.  
  
-   Altere as quebras de página.  
  
 A sessão de edição é criada na primeira vez que você visualiza um relatório. Por padrão, uma sessão de edição dura 7200 segundos (2 horas). A sessão é reiniciada a cada duas horas sempre que você executa o relatório. Quando a sessão de edição expira, o cache de dados é excluído. Se a sessão de edição expirar, uma sessão será criada automaticamente de novo, na próxima vez que você visualiza o relatório. A hora de expiração das sessões de edição é configurável. Se você achar que duas horas constituem um tempo muito grande ou muito pequeno, entre em contato com o administrador do servidor de relatório.  
  
 Por padrão, o cache de dados pode conter até cinco conjuntos de dados. Se você usar muitas combinações diferentes de valores de parâmetros, o relatório poderá precisar de mais dados. Isso requer que o cache seja atualizado e o relatório é renderizado mais lentamente na próxima visualização. O número de entradas no cache pode ser configurado pelo administrador do servidor de relatório.  
  
## <a name="concurrency-of-report-updates"></a>Simultaneidade de atualizações de relatório  
 Frequentemente, você visualiza um relatório como uma etapa na atualização e depois o salva em um servidor de relatório. Quando você estiver atualizando um relatório, é possível que outra pessoa esteja atualizando e salvando-o ao mesmo tempo. O relatório que é salvo por último é a versão de relatório que está disponível para futuras exibições e atualizações. Isso significa que a versão do relatório que você visualizou pode não ser a versão que você irá abrir novamente. Você tem a opção para salvar o relatório com um novo nome usando a opção **Salvar como** no menu Construtor de Relatórios.  
  
## <a name="external-report-items"></a>Itens de relatório externos  
 Seu relatório pode incluir itens como fontes de dados compartilhadas, imagens externas e sub-relatórios armazenadas separadamente do relatório. Como os itens são armazenados separadamente, é possível que eles sejam movidos para um local diferente no servidor de relatório ou excluídos. Se isso acontecer, a visualização do relatório poderá falhar. Você poderá atualizar o relatório para indicar o local atualizado do item ou, se o item for excluído, substituí-lo por um item existente ou remover a referência ao item do relatório.  
  
 Se um sub-relatório usado por seu relatório for alterado depois que sua sessão de edição for criada, o relatório não será renderizado na visualização. Para visualizar o relatório com êxito, salve-o ou clique em **Atualizar** para obter dados atualizados.  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar dados a um relatório &#40;relatórios e SSRS&#41;](../report-data/report-datasets-ssrs.md)   
 [Formatando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../report-design/charts-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Salvando relatórios &#40;Construtor de Relatórios&#41;](saving-reports-report-builder.md)  
  
  
