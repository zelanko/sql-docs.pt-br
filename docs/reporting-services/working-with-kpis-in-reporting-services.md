---
title: "Trabalhando com KPIs no Reporting Services | Microsoft Docs"
ms.date: "02/24/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a28cf500-6d47-4268-a248-04837e7a09eb
caps.latest.revision: 13
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 8
---
# Trabalhando com KPIs no Reporting Services
Um KPI (indicador chave de desempenho) é uma indicação visual que informa o progresso feito em relação a um objetivo.  Os KPIs são valiosos para que equipes, gerentes e empresas avaliem rapidamente o progresso feito em relação a objetivos mensuráveis.   
  
Ao usar os KPIs no SSRS para SQL Server 2016, você pode obter respostas rapidamente para as seguintes perguntas:  
  
-   Em que estou adiantado ou atrasado?  
  
-   O quanto estou adiantado ou atrasado?  
  
-   Qual foi o mínimo que eu concluí?  
  
## Criando um conjunto de dados  
Um KPI usa apenas a primeira linha de dados de um conjunto de dados compartilhado. Verifique se os dados que pretende usar estão localizados na primeira linha. Para criar um conjunto de dados compartilhado, você pode usar o Construtor de Relatórios ou o SQL Server Data Tools.  
  
> **Observação**: o conjunto de dados não precisa estar na mesma pasta que o KPI.  
  
## Posicionamento de KPIs  
  
Os KPIs podem ser criados em qualquer pasta no servidor de relatório.  Antes de criar um KPI, convém escolher o local certo para colocá-lo. Você pode colocá-lo em uma pasta que seja visível para os usuários e, ao mesmo tempo, seja relevante para outros relatórios e KPIs relacionados.  
  
## Adicionando um KPI  
  
Depois de determinar o local do KPI, vá para essa pasta e escolha **Novo** > **KPI** no menu superior.  
  
![rsCreateKPI1](../reporting-services/media/rscreatekpi1.png)  
  
A tela **Novo KPI** será exibida.  
  
![rsCreateKPI2](../reporting-services/media/rscreatekpi2.png)  
  
Você pode atribuir valores estáticos ou usar dados de um conjunto de dados compartilhado. Quando você cria um novo KPI, ele é preenchido com um conjunto aleatório de dados manual.  
  
|Campo|Description|  
|---|---|  
|Formato do valor|  Usado para alterar o formato do valor que está em exibição.|   
|Value|O valor a ser exibido para o KPI.|  
|Meta|Usado como uma comparação para um valor numérico e mostrado como uma diferença percentual.|  
|Status|Valor numérico usado para determinar a cor do bloco do KPI. Os valores válidos são 1 (verde), 0 (âmbar) e -1 (vermelho).|  
|Conjunto de tendências|Valores numéricos separados por vírgula usados para visualizações de gráfico. Pode ser definido também como a coluna de um conjunto de dados com valores que representam a tendência.|  
  
> **Aviso**: embora você possa usar o valor textual para o campo **Status** em tempo de design, use o valor numérico quando atualizar um conjunto de dados. Se atualizar um conjunto de dados com o valor textual em vez do valor numérico, ele pode corromper os KPIs no servidor.  
  
> **Observação**: os campos **Valor**, **Meta** e **Status** só podem escolher um valor na primeira linha do resultado de um conjunto de dados. No entanto, o campo **Conjunto de tendências** pode escolher a coluna que reflete a tendência.  
  
Para usar os dados de conjunto de dados compartilhado, faça o seguinte:  
  
1.  Mude a caixa suspensa de campos de **Definido manualmente** ou **Não definido** para **Campo de conjunto de dados**.  
  
    ![rsCreateKPI3](../reporting-services/media/rscreatekpi3.png)  
  
2.  Selecione as **reticências (...)** na caixa de dados. A tela **Escolher um Conjunto de Dados** será exibida.  
  
    ![rsCreateKPI4](../reporting-services/media/rscreatekpi4.png)  
  
3.  Escolha o conjunto de dados com os dados que deseja exibir.  
  
4.  Escolha o campo que pretende usar. Escolha **OK**.  
  
    ![rsCreateKPI5](../reporting-services/media/rscreatekpi5.png)  
  
5.  Altere o **Formato do Valor** que deve corresponder ao formato do seu valor. Neste exemplo, o valor é uma moeda.  
  
    ![rsCreateKPI6](../reporting-services/media/rscreatekpi6.png)  
  
6.  Escolha **Aplicar**.  
  
    ![rsCreateKPI7](../reporting-services/media/rscreatekpi7.png)  
  
## Removendo um KPI  
  
Para remover um KPI, você pode fazer o seguinte:  
  
1.  Selecione as **reticências (...)** do KPI que pretende remover. Escolha **Gerenciar**.  
  
    ![rsRemoveKPI1](../reporting-services/media/rsremovekpi1.png)  
  
2.  Escolha **Excluir**. Escolha **Excluir** novamente na caixa de diálogo de confirmação.  
  
    ![rsRemoveKPI2](../reporting-services/media/rsremovekpi2.png)  
  
## Atualizando um KPI  
  
Para atualizar o KPI, configure um **plano de atualização do cache** para o conjunto de dados compartilhado. Atualmente, não é possível configurar um plano de atualização do cache no portal da Web. Para fazer isso, vá para o Gerenciador de Relatórios anterior.   
  
Esse recurso explica como configurar um plano de atualização do cache com algumas configurações básicas. Para saber mais sobre planos de atualização do cache, confira o artigo [Opções de Atualização do Cache (Gerenciador de Relatórios)](Cache%20Refresh%20Options%20(Report%20Manager).xml).  
  
1.  Abra o Gerenciador de Relatórios e localize o conjunto de dados compartilhado cujas propriedades do plano de atualização do cache você deseja configurar.   
  
2.  Passe o cursor sobre o relatório ou conjunto de dados compartilhado e escolha a seta suspensa.  
  
3.  Na lista suspensa, escolha **Gerenciar**. A página **Propriedades Gerais** é exibida.  
  
4.  Escolha a guia **Opções de Atualização do Cache**.  
  
5.  Para criar um novo plano do cache, escolha **Novo Plano de Atualização do Cache**.  
  
    ![rsRefreshKPI1](../reporting-services/media/rsrefreshkpi1.png)  
  
6.  Você receberá uma mensagem perguntando se deseja habilitar cache para esse item com as opções padrão. Selecione **OK**.  
  
    > **Observação**: você deve habilitar e iniciar o serviço SQL Server Agent para criar um plano de atualização do cache.  
  
7.  Você pode optar por um agendamento específico ou escolher uma agenda compartilhada, se houver.  
  
8.  Os valores do KPI serão atualizados quando o agendamento do plano de atualização do cache for executado.  
  
    ![rsRefreshKPI2](../reporting-services/media/rsrefreshkpi2.png)  
  
## Consulte também  
  
- [Portal da Web (modo nativo do SSRS)](../reporting-services/web-portal-ssrs-native-mode.md)  
  
- [Opções de Atualização do Cache (Gerenciador de Relatórios)](Cache%20Refresh%20Options%20(Report%20Manager).xml)  
  
    
  
  
  
