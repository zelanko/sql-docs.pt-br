---
title: "Limpar dados usando o conhecimento (externo) dos dados de refer&#234;ncia | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 158009e9-8069-4741-8085-c14a5518d3fc
caps.latest.revision: 15
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 15
---
# Limpar dados usando o conhecimento (externo) dos dados de refer&#234;ncia
  Este tópico descreve como limpar dados usando o conhecimento dos provedores de dados de referência. Enquanto todas as etapas de execução, uma atividade de limpeza permanece o mesmo para limpar os dados usando conhecimento dos provedores de dados de referência, conforme explicado no [Limpar dados usando o DQS & 40; interno & 41; Conhecimento](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md), este tópico fornece informações específicas para limpeza de dados usando o serviço de dados de referência no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS).  
  
 Quando você usa o recurso do serviço de dados de referência no DQS para limpar os dados, o processo de limpeza do DQS envia os valores de domínio mapeados ao provedor de serviço de dados de referência como uma solicitação em lote. O serviço de dados de referência responde com as seguintes informações:  
  
-   Correção sugerida  
  
-   Confiança  
  
-   Informações adicionais sobre o domínio mapeado. Os dados de referência também podem padronizar, analisar ou enriquecer a origem com dados adicionais. Essas informações adicionais são fornecidas nos campos adicionais da resposta.  
  
 Após obter a resposta de serviço de dados de referência, acontecerá o seguinte no DQS durante a atividade de limpeza:  
  
-   Com base nos valores de **Limite de Correção Automática** e **Confiança Mínima** especificados durante o mapeamento dos domínios com serviço de dados de referência, os valores do domínio serão corrigidos automaticamente ou sugeridos com base no nível de confiança.  
  
    > [!NOTE]  
    >  Os valores de limite especificados durante o mapeamento de um domínio para um serviço de dados de referência são aplicados durante a limpeza dos dados através do conhecimento no serviço de dados de referência, e não os especificados na guia **Configurações Gerais** da seção **Configuração** . Para obter informações sobre como especificar valores de limite para limpeza de dados de referência, consulte a etapa 9 na [Anexar domínio ou domínio composto para dados de referência](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md).  
  
-   Os valores de domínio são categorizados da seguinte maneira: **Sugerido**, **Novo**, **Inválido**, **Corrigido**e **Correto**.  
  
-   Os dados adicionais são acrescentados à origem, e as informações estão disponíveis junto com os dados limpos para exportação.  
  
## Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Os domínios necessários de uma base de dados de conhecimento do DQS precisam ser mapeados para o serviço de dados de referência apropriado. Além disso, a base de dados de conhecimento deve conter conhecimento sobre o tipo de dados que você deseja limpar. Por exemplo, se você quiser limpar a fonte de dados que contém endereços americanos, mapeie os domínios para um provedor de serviço de dados de referência que fornece dados de alta qualidade sobre endereços americanos. Para obter mais informações, consulte [Anexar domínio ou domínio composto para dados de referência](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_kb_operator no banco de dados DQS_MAIN para executar a limpeza de dados.  
  
##  <a name="Cleanse"></a> Limpar os dados usando o conhecimento dos dados de referência  
 Continuaremos com o mesmo exemplo de uso dos domínios que Mapeamos no tópico anterior, [Anexar domínio ou domínio composto para dados de referência](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md), com o serviço Melissa Data no Windows Azure Marketplace. Agora, usaremos os mesmos domínios para limpar alguns endereços de exemplo americanos. As etapas para limpar os dados são os mesmos conforme descrito em [Limpar dados usando o DQS & 40; interno & 41; Conhecimento](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md). No entanto, chamaremos sua atenção sempre que necessário durante o processo.  
  
1.  Crie um projeto de qualidade de dados e selecione a atividade **Limpeza** . Consulte [Create a Data Quality Project](../data-quality-services/create-a-data-quality-project.md).  
  
2.  Na página **Mapa** , mapeie os quatro domínios a seguir com as colunas apropriadas da fonte de dados: **Linha de Endereço**, **Cidade**, **Estado**e **CEP**. Clique em **Avançar**.  
  
    > [!NOTE]  
    >  Como você mapeou todos os domínios dentro de 4 a **verificação de endereço** domínio composto, a limpeza de dados será feita no nível do domínio composto e não no nível do domínio individual.  
  
3.  Sobre o **Limpar** página, execute o processo de limpeza auxiliada por computador clicando **Iniciar**. Após o processo de limpeza, clique em **Avançar**.  
  
    > [!NOTE]  
    >  Sobre o **Limpar** página, o DQS exibe informações sobre os domínios que estão anexados a referência de serviço de dados a seguir duas maneiras:  
    >   
    >  -   Uma mensagem é exibida abaixo do **Iniciar** botão: "domínios \< domínio1>, \< domínio2>,... \< Domínion> são limpos com o provedor de serviços de dados de referência. " Neste exemplo, a seguinte mensagem será exibida: "A verificação de domínio de endereço é limpa com o provedor de serviços de dados de referência".  
    > -   Um ícone, ![O domínio está conectado ao RDS](../data-quality-services/media/dqs-rdsindicator.png "O domínio está conectado ao RDS"), é exibido no **Profiler** área nos domínios anexados ao provedor de serviço de dados de referência. Neste exemplo, o ícone será exibido no domínio composto **Verificação de Endereço** .  
  
4.  Na página **Gerenciar e exibir resultados** , revise seus valores de domínio. O serviço de dados de referência pode exibir mais de uma sugestão, se disponível, para um valor, dependendo do número máximo de sugestões especificado na caixa **Candidatos Sugeridos** durante o mapeamento do domínio para o serviço de dados de referência. Por exemplo, são exibidas duas sugestões para os seguintes endereços americanos:  
  
     **Valor original:**  
  
    |Linha de Endereço|Cidade|Estado|CEP|  
    |------------------|----------|-----------|---------|  
    |1 msft way|Redmond||98052|  
  
     **Valores sugeridos:**  
  
    |Linha de Endereço|Cidade|Estado|CEP|  
    |------------------|----------|-----------|---------|  
    |1 Microsoft Way|Redmond|WA|98052|  
    |PO Box 1|Redmond|WA|98073|  
  
     ![Limpeza usando serviços de dados de referência](../data-quality-services/media/dqs-rdscleansing.JPG "Limpeza usando serviços de dados de referência")  
  
    > [!NOTE]  
    >  Para domínios compostos, o DQS realça também os domínios individuais com uma cor diferente, que foram corrigidos durante o processo de limpeza assistido por computador. Por exemplo, neste caso, os domínios **Linha de Endereço** e **Estado** foram corrigidos e, portanto, são realçados em ciano.  
  
5.  Depois que você revisar todos os valores de domínio, clique em **Avançar** para exportar os dados.  
  
6.  Sobre o **exportar** página, você notará que além das informações normais sobre a atividade de limpeza para cada domínio (origem, razão, confiança e Status), há informações adicionais fornecidas pela referência de Melissa Data service dados sobre os dados de endereço, como latitude e longitude do endereço, nome do município, endereço digite (edifício, Rua etc.) e assim por diante.  
  
7.  Exportar dados para o destino necessário (SQL Server, CSV ou Excel) e clique em **Concluir** para fechar o projeto.  
  
    > [!IMPORTANT]  
    >  Se você estiver usando uma versão de 64 bits do Excel, não poderá exportar os dados limpos para um arquivo do Excel; você só poderá exportar para um banco de dados do SQL Server ou para um arquivo .csv.  
  
  