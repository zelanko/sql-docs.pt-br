---
title: Importar valores de projeto de limpeza para um domínio
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.importprojectvalues.f1
ms.assetid: f23e38e2-39e0-42d7-abd5-34d8fcca5d2a
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 34060c3fc5416f7244b400b506faad9097d66880
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241798"
---
# <a name="import-cleansing-project-values-into-a-domain"></a>Importar valores de projeto de limpeza para um domínio

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS), você pode importar conhecimento de qualidade de dados coletado durante o processo de limpeza em um projeto de limpeza de qualidade de dados ou um pacote do Integration Services que contém o componente de limpeza DQS em um domínio. Isto assegura que o conhecimento confiável não seja perdido, e que a base de dados de conhecimento seja aprimorada continuamente.  
  
##  <a name="BeforeYouBegin"></a>Antes de começar  
  
###  <a name="Prerequisites"></a>Pré-requisitos  
  
-   Para importar valores de projeto de limpeza para dentro de um domínio, o domínio deverá ter sido usado no projeto de limpeza no Cliente Data Quality ou no pacote do Integration Services que contém o componente de limpeza DQS.  
  
-   O projeto de limpeza no Cliente Data Quality ou o pacote do Integration Services contendo o componente de limpeza DQS deve ter sido concluído com sucesso.  
  
###  <a name="Security"></a>Segurança  
  
####  <a name="Permissions"></a>Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para importar o conhecimento de qualidade de dados reunido durante o processo de limpeza para um domínio.  
  
##  <a name="Import"></a>Importar valores de projeto de limpeza  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Execute o aplicativo Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra uma base de dados de conhecimento na atividade Gerenciamento de Domínio.  
  
3.  Se estiver adicionando valores a um domínio existente, selecione o domínio na lista de domínios.  
  
4.  Clique na guia **Valores de Domínio** , clique no ícone **Importar Valores** na barra de ícones e clique em **Importar valores do projeto**. A caixa de diálogo **Importar Valores do Projeto** é exibida com uma lista de projetos de qualidade de dados e pacotes do Integration Services que foram limpos usando o domínio.  
  
    > [!NOTE]  
    >  Se nenhum projeto tiver sido criado com o uso do domínio ou qualquer um de seus domínios vinculados ou o projeto não tiver sido terminado, a opção **Importar valores do projeto** não estará disponível.  
  
5.  Na caixa de diálogo **Importar Valores do Projeto** :  
  
    -   Selecione **Todos** na lista suspensa **Importado** para exibir todos os projetos ou **Nenhum** para exibir apenas os projetos cujos valores ainda não foram importados.  
  
    -   Selecione o projeto a partir do qual você importará valores.  
  
    -   Selecione **Adicionar valores da guia Novo** para importar valores na guia Novo além dos valores nas guias **Corrigir** e **Corrigido** .  
  
    -   Clique em **OK**.  
  
6.  Você retorna à guia **Valores do Domínio** e uma mensagem é exibida após a importação bem-sucedida dos valores. Valores que foram importados e, portanto, são novos para o domínio serão exibidos na tabela **Valores** .  
  
7.  Desmarque **Mostrar Somente Novo** para exibir todos os valores no domínio.  
  
8.  Selecione **Corrigir**, **Erro**ou **Inválido** para exibir apenas os valores do tipo selecionado.  
  
9. Para procurar uma cadeia de caracteres específica, insira essa cadeia de caracteres na caixa **Localizar** . Clique na seta para cima ou para baixo para percorrer os valores que atendem os critérios de pesquisa. Eles serão realçados em amarelo.  
  
10. Clique em **Concluir**.  
  
    > [!NOTE]  
    >  Para obter mais informações sobre como trabalhar com valores na página **Valores de Domínio** , consulte [Change Domain Values](../data-quality-services/change-domain-values.md).  
  
##  <a name="FollowUp"></a>Acompanhamento: depois de importar valores de projeto para um domínio  
 Depois que você importar o conhecimento de qualidade de dados reunido durante o processo de limpeza para um domínio, você pode executar outras tarefas de gerenciamento de domínio no domínio e seus valores. Para obter mais informações, consulte [Gerenciando um domínio](../data-quality-services/managing-a-domain.md).  
  
##  <a name="Values"></a>Valores que serão importados  
 Os seguintes valores serão importados de um projeto para um domínio:  
  
-   Somente valores da cadeia de caracteres são importados para o domínio.  
  
-   Apenas valores das guias **Correto**, **Corrigido**e **Novo** na página **Gerenciar e Exibir resultados** da atividade **Limpeza** serão importados. Os valores da guia **Novo** serão importados apenas se a caixa de seleção **Adicionar valores da guia Novo** estiver marcada na caixa de diálogo **Importar Valores do Projeto** .  
  
-   Os valores serão importados como corretos ou como um erro com sua correção. Somente um valor de erro com um valor de correção será importado.  
  
-   O valor de correção será um novo valor que não existe na base de dados de conhecimento ou um valor correto existente.  
  
-   Somente as correções executadas no nível do valor, não no nível do registro serão importadas para a base de dados de conhecimento.  
  
-   Valores inválidos serão criados se o valor importado contrariar uma regra de domínio.  
  
-   Se você importar valores de vários projetos de uma vez, os valores serão importados em sequência.  
  
-   Uma correção feita em virtude de uma relação baseada em termo em um domínio é importada como um valor correto (não como um erro).  
  
##  <a name="ValuesNot"></a>Valores que não serão importados  
 Os seguintes valores não serão importados de um projeto para um domínio:  
  
-   Valores das guias **Sugerido** e **Inválido** na página **Gerenciar e exibir resultados** da atividade **Limpeza** não serão importados.  
  
-   Se um valor encontrado no projeto de limpeza contrariar um valor existente no domínio, o valor encontrado no projeto será ignorado. Isso incluirá conflitos entre os valores da base de dados de conhecimento e de limpeza.  
  
-   As correções executadas no nível do registro não serão importadas para a base de dados de conhecimento.  
  
-   Nenhum valor será importado para um domínio se o valor que ele substituiria fosse corrigido ou aprovado como correto por um serviço de dados de referência.  
  
-   Se um valor de correção aparecer na base de dados de conhecimento como um valor inválido ou com erro, nem o valor com erro, nem o valor de correção serão importados.  
  
-   Se o domínio fizer parte de um domínio composto e a limpeza fosse executada no domínio composto, nenhum valor será importado.  
  
-   Você pode importar valores de um projeto somente quando a base de dados de conhecimento tem um estado de em funcionamento e está bloqueada pelo usuário realizando a importação.  
  
## <a name="see-also"></a>Consulte Também  
 [Limpeza de dados](../data-quality-services/data-cleansing.md)   
 [Transformação de limpeza DQS](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)  
  
  
