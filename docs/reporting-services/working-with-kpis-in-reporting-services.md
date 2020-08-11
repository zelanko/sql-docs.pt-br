---
title: Trabalhando com KPIs no Reporting Services | Microsoft Docs
description: Saiba como você pode medir com facilidade o status e o desempenho usando KPIs no SQL Server Reporting Services.
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.date: 07/02/2017
ms.openlocfilehash: b92f19c74e5b5e3215836e174bf895f7cb61c36b
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247435"
---
# <a name="working-with-kpis-in-reporting-services"></a>Trabalhando com KPIs no Reporting Services

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Um *KPI (indicador chave de desempenho)* é uma indicação visual que informa o progresso feito em relação a uma meta.  Os KPIs são valiosos para que equipes, gerentes e empresas avaliem rapidamente o progresso feito em relação a objetivos mensuráveis.
  
Ao usar os KPIs no SQL Server Reporting Services, você pode visualizar respostas rapidamente para as seguintes perguntas:  
  
- Em que estou adiantado ou atrasado?  
  
- O quanto estou adiantado ou atrasado?  
  
- Quais são os valores mínimos que conclui?  

> [!NOTE]
> Os KPIs só podem ser acessados nas edições Enterprise (Developer) do portal do SSRS.

## <a name="creating-a-dataset"></a>Criando um conjunto de dados

Um KPI usa apenas a primeira linha de dados de um conjunto de dados compartilhado. Verifique se os dados que pretende usar estão localizados na primeira linha. Para criar um conjunto de dados compartilhado, você pode usar o Construtor de Relatórios ou o SQL Server Data Tools.  
  
> **Observação**: o conjunto de dados não precisa estar na mesma pasta que o KPI.  
  
## <a name="placement-of-kpis"></a>Posicionamento de KPIs  
  
Os KPIs podem ser criados em qualquer pasta no servidor de relatório.  Antes de criar um KPI, convém escolher o local certo para colocá-lo. Você pode colocá-lo em uma pasta que seja visível para os usuários e, ao mesmo tempo, seja relevante para outros relatórios e KPIs relacionados.  
## <a name="adding-a-kpi"></a>Adicionando um KPI
  
Depois de determinar o local do KPI, vá para essa pasta e escolha **Novo** > **KPI** no menu superior.  
  
![rsCreateKPI1](../reporting-services/media/rscreatekpi1.png)  
  
A tela **Novo KPI** será exibida.  
  
![rsCreateKPI2](../reporting-services/media/rscreatekpi2.png)  
  
Você pode atribuir valores estáticos ou usar dados de um conjunto de dados compartilhado. Quando você cria um novo KPI, ele é preenchido com um conjunto aleatório de dados manual.  
  
| Campo | Descrição |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| Formato de valor | Usado para alterar o formato do valor que está em exibição. |
| Valor | O valor a ser exibido para o KPI. |
| Goal | Usado como uma comparação para um valor numérico e mostrado como uma diferença percentual. |
| Status | Valor numérico usado para determinar a cor do bloco do KPI. Os valores válidos são 1 (verde), 0 (âmbar) e -1 (vermelho). |
| Conjunto de tendências | Valores numéricos separados por vírgula usados para visualizações de gráfico. Pode ser definido também como a coluna de um conjunto de dados com valores que representam a tendência. |
| Conteúdo relacionado | A capacidade de definir um link de detalhamento. Esse link pode ser um relatório móvel publicado no portal ou uma URL personalizada. |
  
> **Aviso**: embora você possa usar o valor textual para o campo **Status** em tempo de design, use o valor numérico quando atualizar um conjunto de dados. Se atualizar um conjunto de dados com o valor textual em vez do valor numérico, ele pode corromper os KPIs no servidor.  
>
> **Observação**: os campos **Valor**, **Meta** e **Status** só podem escolher um valor na primeira linha do resultado de um conjunto de dados. No entanto, o campo **Conjunto de tendências** pode escolher a coluna que reflete a tendência.  
  
Para usar os dados de conjunto de dados compartilhado, execute as seguintes etapas.
  
1. Mude a caixa suspensa de campos de **Definido manualmente**ou **Não definido**para **Campo de conjunto de dados**.  
  
    ![rsCreateKPI3](../reporting-services/media/rscreatekpi3.png)  
  
2. Selecione as **reticências (...)** na caixa de dados. A tela **Escolher um Conjunto de Dados** será exibida.  
  
    ![rsCreateKPI4](../reporting-services/media/rscreatekpi4.png)  
  
3. Escolha o conjunto de dados com os dados que deseja exibir.  
  
4. Escolha o campo que pretende usar. Selecione **OK**.  
  
    ![rsCreateKPI5](../reporting-services/media/rscreatekpi5.png)  
  
5. Altere o **Formato do Valor** que deve corresponder ao formato do seu valor. Neste exemplo, o valor é uma moeda.  
  
    ![rsCreateKPI6](../reporting-services/media/rscreatekpi6.png)  
  
6. Escolha **Aplicar**.  
  
    ![rsCreateKPI7](../reporting-services/media/rscreatekpi7.png)

## <a name="configuring-related-content"></a>Configurando o conteúdo relacionado

Ao escolher **Relatório Móvel**, você pode escolher o destino em uma caixa de diálogo.

   ![Relatório móvel](media/rscreatekpi-related-content-mobile-report.png)

Ao clicar no KPI no portal, uma miniatura do relatório móvel será exibida na lista suspensa do conteúdo relacionado. Ao clicar nessa miniatura você poderá navegar diretamente para o relatório em questão.

Você também poderá especificar uma URL personalizada. Essa tarefa pode ser qualquer coisa: um site, um site do SharePoint, uma URL para um relatório do SSRS (que lhe permita transmitir parâmetros embutidos no código).

![URL personalizada](media/rscreatekpi-related-content-custom-url.png)

Agora, quando você clica no KPI, a URL é mostrada em conteúdo relacionado.

Só é possível adicionar um relatório móvel ou uma URL personalizada.
  
## <a name="removing-a-kpi"></a>Removendo um KPI  
  
Para remover um KPI, execute as seguintes etapas.
  
1. Selecione as **reticências (...)** do KPI que deseja remover. Selecione **Gerenciar**.  
  
    ![rsRemoveKPI1](../reporting-services/media/rsremovekpi1.png)  
  
2. Selecione **Excluir**. Escolha **Excluir** novamente na caixa de diálogo de confirmação.  
  
    ![rsRemoveKPI2](../reporting-services/media/rsremovekpi2.png)  
  
## <a name="refreshing-a-kpi"></a>Atualizando um KPI  
  
Para atualizar o KPI, você precisará configurar um cache para o conjunto de dados compartilhado. Para obter mais informações sobre planos de atualização do cache, consulte [Trabalhar com conjuntos de dados compartilhados](../reporting-services/work-with-shared-datasets-web-portal.md).  
  
## <a name="next-steps"></a>Próximas etapas
  
[Portal da Web](../reporting-services/web-portal-ssrs-native-mode.md)  
[Trabalhar com conjuntos de dados compartilhados](../reporting-services/work-with-shared-datasets-web-portal.md)

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
