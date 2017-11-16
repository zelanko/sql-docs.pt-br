---
title: "Criar um conjunto de dados compartilhado ou um conjunto de dados inserido (Construtor de Relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 10/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d1d7bc71-f0e9-4ce5-b3ad-6fee54388a31
caps.latest.revision: "9"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 77d880d77a10c5082f3818674876c5ac0336bcc3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs"></a>Criar um conjunto de dados compartilhado ou um conjunto de dados inserido (Construtor de Relatórios e SSRS)
Os conjuntos de dados inseridos são para uso em um único relatório do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] . Os conjuntos de dados compartilhados em um servidor de relatório podem ser usados por vários relatórios, móveis e paginados. Para criar um conjunto de dados, é necessária uma fonte de dados inserida ou compartilhada.  
  
 Use o **Construtor de Relatórios** para executar as seguintes tarefas:  
  
1.  Crie um conjunto de dados compartilhado no modo de exibição Design de Conjunto de Dados. Os conjuntos de dados compartilhados devem usar fontes de dados compartilhadas publicadas.  
  
2.   Crie um conjunto de dados inserido no modo de exibição Design de Relatório.  
  
3.   Salve o conjunto de dados diretamente no servidor de relatório ou no site do SharePoint.  
  
 Use o **Designer de Relatórios** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para as seguintes tarefas:  
  
1.  Crie um conjunto de dados compartilhado no Gerenciador de Soluções. Conjuntos de dados compartilhados devem usar fontes de dados da pasta Fontes de Dados Compartilhadas no Gerenciador de Soluções.  
  
2.  Crie um conjunto de dados inserido no painel de dados do relatório.  
  
3.  Outra opção é implantar os conjuntos de dados compartilhados e a fonte de dados compartilhada com o relatório. Para cada tipo de item, use Propriedades do Projeto para especificar caminhos para pastas no servidor de relatório ou no site do SharePoint.  
  
 Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-open-report-builder-and-create-a-shared-dataset"></a>Para abrir o Construtor de Relatórios e criar um conjunto de dados compartilhado  
  
1.  Abra o Construtor de Relatórios. O **Painel de novo relatório ou conjunto de dados** abre, como mostrado na figura seguinte:  
  
     ![rs_NewSharedDataset](../../reporting-services/report-data/media/rs-newshareddataset.gif "rs_NewSharedDataset")  
  
    > [!NOTE]  
    >  Se o **painel Novo relatório ou conjunto de dados** não for exibido, no botão Construtor de Relatórios, clique em **Novo**.  
  
2.  No painel esquerdo, sob **Criar um conjunto de dados**, clique em **Conjunto de Dados Compartilhado**.  
  
3.  No painel direito, clique em **Procurar** para selecionar uma fonte de dados compartilhada no servidor de relatório e clique em **Criar**. O designer de consulta associado à fonte de dados compartilhada é aberto.  
  
4.  No designer de consulta, especifique os campos a serem incluídos no conjunto de dados.  
  
5.  Clique em **Executar** (**!**) para executar a consulta.  
  
6.  No botão **Construtor de Relatórios** , clique em **Salvar** ou em **Salvar como** para salvar o conjunto de dados compartilhado no servidor de relatório.  
  
7.  Para sair do Construtor de Relatórios, clique em **Construtor de Relatórios**e em **Sair do Construtor de Relatórios**. Para trabalhar com relatórios, clique em **Construtor de Relatórios**e em **Novo** ou **Abrir**.  
  
## <a name="to-set-query-parameter-options"></a>Para definir opções de parâmetro de consulta  
  
1.  Abra o Construtor de Relatórios.  
  
2.  Clique em **Abrir**.  
  
3.  Navegue até o servidor de relatório e selecione a pasta da fonte de dados compartilhada.  
  
4.  Em **Itens de tipo**, clique em Conjuntos de Dados (*.rsd) na lista suspensa.  
  
5.  Selecione o conjunto de dados compartilhado e clique em **Abrir**. O designer de consulta associado é aberto.  
  
6.  No Faixa de Opções, clique em **Propriedades do Conjunto de Dados**.  
  
7.  Clique em **Parâmetros**. Nessa página, defina um valor padrão como uma constante ou uma expressão, marque o parâmetro como somente leitura, anulável ou **Omitir da Consulta**. Para obter mais informações, consulte [Parâmetros de Relatório](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

  
## <a name="to-create-a-dataset-from-a-sql-server-relational-database"></a>Para criar um conjunto de dados a partir de um banco de dados relacional do SQL Server  
  
1.  No painel de dados do relatório, clique com o botão direito do mouse no nome da fonte de dados e clique em **Adicionar Conjunto de Dados**. A página **Consulta** da caixa de diálogo **Propriedades do Conjunto de Dados** é aberta.  
  
2.  Em **Nome**, digite um nome para o conjunto de dados ou aceite o nome padrão.  
  
    > [!NOTE]  
    >  O nome do conjunto de dados é usado internamente no relatório. Para maior clareza, é recomendável que o nome do conjunto de dados descreva os dados retornados pela consulta.  
  
3.  Em **Fonte de dados**, navegue até o nome de uma fonte de dados compartilhada existente e selecione-o, ou clique em **Nova** para criar uma nova fonte de dados inserida.  
  
4.  Selecione uma opção de **Tipo de consulta** . As opções dependem do tipo de fonte de dados.  
  
    -   Selecione **Texto** para gravar uma consulta usando a linguagem de consulta da fonte de dados.  
  
    -   Selecione **Tabela** para retornar todos os campos em uma tabela de banco de dados relacional.  
  
    -   Selecione **StoredProcedure** para executar um procedimento armazenado pelo nome.  
  
5.  Em **Consulta**, digite o nome da consulta, do procedimento armazenado ou da tabela. Se quiser, clique em **Designer de Consulta** para abrir a ferramenta de designer gráfico ou com base em texto, ou clique em **Importar** para importar a consulta por meio de um relatório existente.  
  
     Em alguns casos, a coleção de campos especificada pela consulta só pode ser determinada ao executar a consulta na fonte de dados. Por exemplo, um procedimento armazenado pode retornar um conjunto de campos variável no conjunto de resultados. Clique em **Atualizar Campos** para executar a consulta na fonte de dados e recuperar os nomes de campo que são necessários para preencher a coleção de campos do conjunto de dados no painel de dados do relatório. A coleção de campos é exibida abaixo do nó do conjunto de dados depois que a caixa de diálogo **Propriedades do Conjunto de Dados** é fechada.  
  
6.  Em **Tempo Limite**, digite o número de segundos que o servidor de relatórios deve aguardar para receber uma resposta do banco de dados. O valor padrão é 0 segundos. Quando o valor do tempo limite for 0, a consulta não terá um tempo limite.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     O conjunto de dados e sua coleção de campos aparecerão no painel de dados do relatório abaixo do nó da fonte de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Conjuntos de dados de relatório &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Conexões de dados, fontes de dados e cadeias de conexão &#40;Construtor de Relatórios e SSRS&#41;](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)   
 [Conjuntos de dados inseridos e compartilhados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
