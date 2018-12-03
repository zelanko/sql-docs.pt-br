---
title: Transformação Pesquisa em modo de cache cheio – Gerenciador de conexões OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Lookup transformation [Integration Services]
ms.assetid: c4150e1b-bdff-4f7a-af4c-3401c34def83
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 43edd7fbdaf744ae9c5ea401e28ccef930d91f2d
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52506976"
---
# <a name="lookup-transformation-full-cache-mode---ole-db-connection-manager"></a>Transformação Pesquisa em modo de cache cheio – Gerenciador de conexões OLE DB
  Você pode configurar a transformação Pesquisa para usar o modo cache cheio e um gerenciador de conexões OLE DB. No modo cache cheio, o conjunto de dados de referência é carregado no cache antes que a transformação Pesquisa seja executada.  
  
 A transformação Pesquisa executa pesquisas ao unir dados em colunas de entradas através de uma fonte de dados conectada com colunas em um conjunto de dados de referência. Para obter mais informações, consulte [Lookup Transformation](../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
 Ao configurar a transformação Pesquisa para usar o gerenciador de conexões OLE DB, selecione uma tabela, exibição ou consulta SQL para gerar o conjunto de dados de referência.  
  
### <a name="to-implement-a-lookup-transformation-in-full-cache-mode-by-using-ole-db-connection-manager"></a>Para implementar uma transformação Pesquisa em modo cache cheio usando o gerenciador de conexões OLE DB  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote que você deseja e, então, clique duas vezes no pacote no Gerenciador de Soluções.  
  
2.  Na guia **Fluxo de Dado** , na **Caixa de Ferramentas**, arraste a transformação Pesquisa até a superfície de design.  
  
3.  Conecte a transformação Pesquisa ao fluxo de dados arrastando um conector de uma fonte ou transformação anterior para a transformação Pesquisa.  
  
    > [!NOTE]  
    >  Uma transformação Pesquisa talvez não seja validada se essa transformação se conectar a um arquivo simples que contém um campo de data vazio. A transformação será validada se o gerenciador de conexões para o arquivo simples tiver sido configurado para reter valores nulos. Para garantir a validação da transformação Pesquisa, no **Editor de Fonte de Arquivo Simples**, na página **Gerenciador de Conexões**, selecione a opção **Reter valores nulos da origem como valores nulos no fluxo de dados** .  
  
4.  Clique duas vezes na fonte ou transformação anterior para configurar o componente.  
  
5.  Clique duas vezes na transformação Pesquisa e, então, em **Editor de Transformação Pesquisa**, na página **Geral** , selecione **Cache cheio**.  
  
6.  Na área **Tipo de conexão** , selecione **Gerenciador de conexões OLE DB**.  
  
7.  Na lista **Especificar como lidar com linhas sem entradas correspondentes** , selecione uma opção de tratamento de erro para as linhas sem entradas correspondentes.  
  
8.  Na página Conexão, selecione um gerenciador de conexões da lista **Gerenciador de conexões OLE DB** ou clique em **Novo** para criar um novo gerenciador de conexões. Para obter mais informações, consulte [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
9. Execute uma dessas tarefas:  
  
    -   Clique em **Usar uma tabela ou uma exibição**e selecione uma tabela ou exibição ou clique em **Nova** para criar uma tabela ou exibição.  
  
         -ou-  
  
    -   Clique em **Use os resultados de uma consulta SQL**e crie uma consulta na janela **Comando SQL** ou clique em **Criar Consulta** para criar uma consulta usando as ferramentas gráficas que o **Construtor de Consultas** fornece.  
  
         -ou-  
  
    -   Se preferir, clique em **Procurar** para importar uma instrução SQL de um arquivo.  
  
     Para validar a consulta SQL, clique em **Analisar Consulta**.  
  
     Para exibir um exemplo dos dados, clique em **Visualização**.  
  
10. Clique na página **Colunas** e, então, na lista **Colunas de Entrada Disponíveis** , arraste pelo menos uma coluna para a coluna na lista **Coluna de Pesquisa Disponível** .  
  
    > [!NOTE]  
    >  A transformação Pesquisa mapeia automaticamente colunas que têm o mesmo nome e o mesmo tipo de dados.  
  
    > [!NOTE]  
    >  Estas colunas devem ter tipos de dados correspondentes a serem mapeados. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
11. Inclua colunas de pesquisa na saída realizando as etapas tarefas:  
  
    1.  Na lista **Colunas de Consulta Disponíveis** . selecione colunas  
  
    2.  Na lista **Operação de Pesquisa** , especifique se os valores das colunas de pesquisa devem substituir os valores na coluna de entrada ou ser gravados em uma nova coluna.  
  
12. Para configurar a saída de erro, clique na página **Saída de Erro** e defina as opções de tratamento de erros. Para obter mais informações, consulte [Editor de Transformação Pesquisa &#40;página Saída de Erro&#41;](../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md).  
  
13. Clique em **OK** para salvar suas alterações na transformação Pesquisa e, então, execute o pacote.  
  
## <a name="see-also"></a>Consulte Também  
 [Implementar uma Transformação Pesquisa em modo cache cheio usando o Gerenciador de Conexões do Cache](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md)   
 [Implementar uma pesquisa no modo Sem Cache ou Cache Parcial](../../integration-services/data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md)   
 [Transformações do Integration Services](../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
