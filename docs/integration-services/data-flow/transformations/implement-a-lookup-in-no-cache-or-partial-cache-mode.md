---
title: Implementar uma pesquisa no modo sem Cache ou Cache parcial | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Lookup transformation
- match exactly [Integration Services]
- lookups [Integration Services]
- exact matches [Integration Services]
ms.assetid: 01b7fbca-5181-4d47-9f75-7f25af6b40d2
caps.latest.revision: 67
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cb81f969cc30366489df367016c8096ea2ac1168
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="implement-a-lookup-in-no-cache-or-partial-cache-mode"></a>Implementar uma pesquisa no modo Sem Cache ou Cache Parcial
  Você pode configurar a transformação Pesquisa para usar o modo cache parcial ou sem-cache:  
  
-   Cache parcial  
  
     As linhas com entradas correspondentes no conjunto de dados de referência e, opcionalmente, as linhas sem entradas correspondentes no conjunto de dados são armazenadas em cache. Quando o tamanho da memória do cache é excedido, a transformação Pesquisa remove automaticamente as linhas usadas com menos frequência do cache.  
  
-   Não cache  
  
     Nenhum dado é carregado no cache.  
  
 Se selecionar cache parcial ou não cache, você usará um gerenciador de conexões OLE DB para conectar-se ao conjunto de dados de referência. O conjunto de dados de referência é gerado usando uma tabela, exibição ou consulta SQL durante a execução da transformação Pesquisa.  
  
### <a name="to-implement-a-lookup-transformation-in-no-cache-or-partial-cache-mode"></a>Como implementar uma transformação Pesquisa no modo Sem-Cache ou Cache Parcial  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] que contém o pacote que você deseja, e, então, abra o pacote.  
  
2.  Na guia **Fluxo de Dados** , adicione uma transformação Pesquisa.  
  
3.  Conecte a transformação Pesquisa ao fluxo de dados arrastando um conector de uma fonte ou transformação anterior para a transformação Pesquisa.  
  
    > [!NOTE]  
    >  Uma transformação Pesquisa que está configurada para usar o modo Sem-Cache talvez não fosse validada caso se conectasse a um arquivo simples que contém um campo de data vazio. A transformação será validada se o gerenciador de conexões para o arquivo simples tiver sido configurado para reter valores nulos. Para garantir a validação da transformação Pesquisa, no **Editor de Fonte de Arquivo Simples**, na página **Gerenciador de Conexões**, selecione a opção **Reter valores nulos da origem como valores nulos no fluxo de dados** .  
  
4.  Clique duas vezes na fonte ou transformação anterior para configurar o componente.  
  
5.  Clique duas vezes na transformação Pesquisa e em **Editor de Transformação Pesquisa**e, na página **Geral** , selecione **Cache parcial** ou **Sem cache**.  
  
6.  Para a lista **Especificar como lidar com linhas sem entradas correspondentes** , selecione uma opção de tratamento de erros da lista.  
  
7.  Na página **Conexão** , selecione um gerenciador de conexões da lista **Gerenciador de conexões OLE DB** ou clique em **Novo** para criar um novo gerenciador de conexões. Para obter mais informações, consulte [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
8.  Siga um destes procedimentos:  
  
    -   Clique em **Usar uma tabela ou uma exibição**e selecione uma tabela ou exibição ou clique em **Nova** para criar uma tabela ou exibição.  
  
    -   Clique em **Use os resultados de uma consulta SQL**e crie uma consulta na janela **Comando SQL** .  
  
         — ou —  
  
         Clique em **Criar Consulta** para criar uma consulta usando as ferramentas gráficas que o **Construtor de Consultas** fornece.  
  
         — ou —  
  
         Clique em **Procurar** para importar uma instrução SQL de um arquivo.  
  
     Para validar a consulta SQL, clique em **Analisar Consulta**.  
  
     Para exibir um exemplo dos dados, clique em **Visualização**.  
  
9. Clique na página **Colunas** e, então, arraste pelo menos uma coluna da lista **Colunas de Entrada Disponíveis** para uma coluna na lista **Coluna de Pesquisa Disponível** .  
  
    > [!NOTE]  
    >  A transformação Pesquisa mapeia automaticamente colunas que têm o mesmo nome e o mesmo tipo de dados.  
  
    > [!NOTE]  
    >  Estas colunas devem ter tipos de dados correspondentes a serem mapeados. Para obter mais informações, consulte [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
10. Inclua colunas de pesquisa na saída realizando as etapas seguintes:  
  
    1.  Na lista **Colunas de Pesquisa Disponíveis** , selecione colunas.  
  
    2.  Na lista **Operação de Pesquisa** , especifique se os valores das colunas de pesquisa devem substituir os valores na coluna de entrada ou ser gravados em uma nova coluna.  
  
11. Se você selecionou **Cache parcial** na etapa 5, na página **Avançado** , defina as opções de cache seguintes:  
  
    -   Na lista **Tamanho de cache (32 bits)** , selecione o tamanho de cache para ambientes de 32 bits.  
  
    -   Na lista **Tamanho de cache (64 bits)** , selecione o tamanho de cache para ambientes de 64 bits.  
  
    -   Para armazenar as linhas em cache sem entradas correspondentes na referência, selecione **Habilitar cache para linhas sem entradas correspondentes**.  
  
    -   Na lista **Alocação do cache** , selecione a porcentagem do cache a ser usado para armazenar as linhas sem entradas correspondentes.  
  
12. Para modificar a instrução SQL que gera os conjuntos de dados de referência, selecione **Modificar a instrução SQL**e altere a instrução SQL exibida na caixa de texto.  
  
     Se a instrução incluir parâmetros, clique em **Parâmetros** para mapear os parâmetros para colunas de entrada.  
  
    > [!NOTE]  
    >  A instrução SQL opcional especificada nesta página substituirá o nome da tabela especificado na página **Conexão** do **Editor da Transformação Pesquisa**.  
  
13. Para configurar a saída de erro, clique na página **Saída de Erro** e defina as opções de tratamento de erros. Para obter mais informações, consulte [Editor de Transformação Pesquisa &#40;página Saída de Erro&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md).  
  
14. Clique em **OK** para salvar suas alterações na transformação Pesquisa e, então, execute o pacote.  
  
## <a name="see-also"></a>Consulte também  
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  

