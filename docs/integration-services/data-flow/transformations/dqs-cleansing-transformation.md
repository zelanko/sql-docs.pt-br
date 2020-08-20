---
description: Transformação de Limpeza DQS
title: Transformação de Limpeza DQS | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssdqs.designer.cleansing.f1
- sql13.SSDQS.DESIGNER.DQCONNECTION.F1
helpviewer_keywords:
- data correction
- correct data
ms.assetid: d2ec1b1a-c745-4741-b57c-6fdb524a154c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ce6e3f36d8216f08493933798cdab558274e0cb5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495687"
---
# <a name="dqs-cleansing-transformation"></a>Transformação de Limpeza DQS

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  A transformação de Limpeza DQS usa o DQS (Data Quality Services) para corrigir dados de uma fonte de dados conectada com a aplicação de regras aprovadas, que foram criadas para a fonte de dados conectada ou uma fonte de dados semelhante. Para obter informações sobre regras de correção de dados, consulte [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md). Para obter mais informações sobre o DQS, consulte [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md).  
  
 Para determinar se os dados precisam ser corrigidos, a transformação de Limpeza DQS processa dados de uma coluna de entrada quando as seguintes condições são verdadeiras:  
  
-   A coluna é selecionada para correção de dados.  
  
-   O tipo de dados da coluna tem suporte da correção de dados.  
  
-   A coluna é mapeada para um domínio que tem um tipo de dados compatível.  
  
 A transformação também inclui uma saída de erro que você configura para tratar erros em nível de linha. Para configurar a saída de erro, use o **Editor de Transformação de Limpeza DQS**.  
  
 Você pode incluir [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md) no fluxo de dados para identificar linhas de dados que são provavelmente duplicadas.  
  
## <a name="data-quality-projects-and-values"></a>Projetos de qualidade de dados e valores  
 Quando você processar dados com a transformação de limpeza DQS, um projeto de limpeza é criado no Data Quality Server. Você usa o Cliente Data Quality para gerenciar o projeto. Além disso, você pode usar o Cliente Data Quality para importar os valores de projeto em um domínio da base de dados de conhecimento do DQS. Você só pode importar os valores para um domínio (ou domínio vinculado) que a transformação de limpeza DQS tiver configurado para usar.  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Abrir projetos do Integration Services no cliente Data Quality](../../../data-quality-services/open-integration-services-projects-in-data-quality-client.md)  
  
-   [Importar valores de projeto de limpeza para um domínio](../../../data-quality-services/import-cleansing-project-values-into-a-domain.md)  
  
-   [Aplicar regras de qualidade de dados à fonte de dados](../../../integration-services/data-flow/transformations/apply-data-quality-rules-to-data-source.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Abrir, desbloquear, renomear e excluir um projeto do Data Quality](../../../data-quality-services/open-unlock-rename-and-delete-a-data-quality-project.md)  
  
-   Artigo [Dados complexos de limpeza usando domínios compostos](https://social.technet.microsoft.com/wiki/contents/articles/13324.using-dqs-cleansing-complex-data-using-composite-domains.aspx)em social.technet.microsoft.com.  
  
## <a name="dqs-cleansing-transformation-editor-dialog-box"></a>Caixa de diálogo Editor de Transformação de Limpeza DQS
  Use a caixa de diálogo **Editor de Transformação de Limpeza DQS** para corrigir os dados usando Data Quality Services (DQS). Para obter mais informações, consulte [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md).  
  
 **O que você deseja fazer?**  
  
-   [Abra o Editor de Transformação de Limpeza DQS.](#open)  
  
-   [Definir as opções na guia de Gerenciador de Conexões](#connection)  
  
-   [Definir as opções na guia Mapeamento](#mapping)  
  
-   [Definir as opções na guia Avançado](#advanced)  
  
-   [Definir as opções na caixa de diálogo Gerenciador de Conexões de Limpeza DQS.](#manager)  
  
###  <a name="open-the-dqs-cleansing-transformation-editor"></a><a name="open"></a> Abra o Editor de Transformação de Limpeza DQS.  
  
1.  Adicione a Transformação de Limpeza DQS ao pacote do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
2.  Clique com o botão direito do mouse no componente e clique em **Editar**.  
  
###  <a name="set-options-on-the-connection-manager-tab"></a><a name="connection"></a> Definir as opções na guia de Gerenciador de Conexões  
 **Gerenciador de conexões de qualidade de dados**  
 Selecione um gerenciador de conexões DQS existente na lista ou crie uma nova conexão clicando em **Novo**.  
  
 **Novo**  
 Crie um novo gerenciador de conexões, usando a caixa de diálogo **Gerenciador de Conexões de Limpeza DQS** . Consulte [Definir as opções na caixa de diálogo Gerenciador de Conexões de Limpeza DQS.](#manager)  
  
 **Base de conhecimento de qualidade de dados**  
 Selecione uma base de dados de conhecimento do DQS para a fonte de dados conectada. Para obter mais informações sobre a base de dados de conhecimento do DQS, consulte [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
 **Criptografar a conexão**  
 Especifique se é preciso criptografar a conexão para criptografar a transferência de dados entre o Servidor DQS e o [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
 **Domínios disponíveis**  
 Liste os domínios disponíveis para a base de conhecimento selecionada. Há dois tipos de domínios: domínios únicos e domínios compostos que contêm dois ou mais domínios únicos.  
  
 Para obter mais informações sobre como mapear colunas para domínios compostos, consulte [Map Columns to Composite Domains](../../../integration-services/data-flow/transformations/map-columns-to-composite-domains.md).  
  
 Para obter mais informações sobre domínios, consulte [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
 **Configurar Saída de Erro**  
 Especifique como tratar erros em nível de linha. Podem ocorrer erros quando a transformação corrige dados da fonte de dados conectada, devido a valores de dados inesperados ou restrições de validação.  
  
 Os valores válidos são os seguintes:  
  
-   **Falha no Componente**, que indica que houve falha na transformação e os dados de entrada não são inseridos no banco de dados do Data Quality Services. Este é o valor padrão.  
  
-   **Redirecionar Linha**, que indica que os dados de entrada não estão inseridos no banco de dados do Data Quality Services e são redirecionados para a saída do erro.  
  
###  <a name="set-options-on-the-mapping-tab"></a><a name="mapping"></a> Definir as opções na guia Mapeamento  
 Para obter mais informações sobre como mapear colunas para domínios compostos, consulte [Map Columns to Composite Domains](../../../integration-services/data-flow/transformations/map-columns-to-composite-domains.md).  
  
 **Colunas de Entrada Disponíveis**  
 Lista as colunas da fonte de dados conectada. Selecione uma ou mais colunas que contêm os dados que você quer corrigir.  
  
 **Coluna de Entrada**  
 Lista uma coluna de entrada que você selecionou na área **Colunas de Entrada Disponíveis** .  
  
 **Domínio**  
 Selecione um domínio para mapear para a coluna de entrada.  
  
 **Alias de origem**  
 Lista a coluna de origem que contém o valor de coluna original.  
  
 Clique no campo para modificar o nome da coluna.  
  
 **Alias de Saída**  
 Lista a coluna que é enviada pela **Transformação de Limpeza DQS**. A coluna contém o valor de coluna original ou o valor corrigido.  
  
 Clique no campo para modificar o nome da coluna.  
  
 **Alias de status**  
 Lista a coluna que contém informações de status para os dados corrigidos. Clique no campo para modificar o nome da coluna.  
  
###  <a name="set-options-on-the-advanced-tab"></a><a name="advanced"></a> Definir as opções na guia Avançado  
 **Padronizar saída**  
 Indique se é preciso produzir os dados no formato padronizado com base no formato de saída definido para domínios. Para obter mais informações sobre o formato padronizado, consulte [Limpeza de dados](../../../data-quality-services/data-cleansing.md).  
  
 **Confiança**  
 Indique se é preciso incluir o nível de confiança para os dados corrigidos. O nível de confiança indica a extensão de certeza do DQS para a correção ou sugestão. Para obter mais informações sobre níveis de confiança, consulte [Limpeza de dados](../../../data-quality-services/data-cleansing.md).  
  
 **Motivo**  
 Indique se é preciso incluir a razão para a correção de dados.  
  
 **Dados acrescentados**  
 Indique se é preciso produzir dados adicionais que são recebidos de um provedor de dados de referência existente. Para obter mais informações, consulte [Reference Data Services in DQS](../../../data-quality-services/reference-data-services-in-dqs.md).  
  
 **Esquema de dados acrescentado**  
 Indique se é preciso produzir o esquema de dados. Para obter mais informações, consulte [Anexar domínio ou domínio composto para dados de referência](../../../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md).  
  
###  <a name="set-the-options-in-the-dqs-cleansing-connection-manager-dialog-box"></a><a name="manager"></a> Definir as opções na caixa de diálogo Gerenciador de Conexões de Limpeza DQS.  
 **Nome do servidor**  
 Selecione ou digite o nome do servidor DQS ao qual você deseja se conectar. Para obter mais informações sobre o servidor, consulte [DQS Administration](../../../data-quality-services/dqs-administration.md).  
  
 **Testar Conexão**  
 Clique para confirmar se a conexão especificada é viável.  
  
 Você também pode abrir a caixa de diálogo **Gerenciador de Conexões de Limpeza DQS** da área de conexões, fazendo o seguinte:  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], abra um projeto existente do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] ou crie um novo projeto.  
  
2.  Clique com o botão direito do mouse na área de conexões, clique em **Nova Conexão**e, em seguida, clique em **DQS**.  
  
3.  Clique em **Adicionar**.  
  
