---
title: Caixa de diálogo Editor de transformação de limpeza DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ssdqs.designer.cleansing.f1
- SQL12.SSDQS.DESIGNER.DQCONNECTION.F1
ms.assetid: 07e79641-71ee-45d0-a9ba-ed6f9f68f333
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f723e04c13dd16c6f872950652dba759f611cbf3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118184"
---
# <a name="dqs-cleansing-transformation-editor-dialog-box"></a>Caixa de diálogo Editor de Transformação de Limpeza DQS
  Use a caixa de diálogo **Editor de Transformação de Limpeza DQS** para corrigir os dados usando Data Quality Services (DQS). Para obter mais informações, consulte [Data Quality Services Concepts](../../2014/data-quality-services/data-quality-services-concepts.md).  
  
 Para saber mais sobre a transformação, consulte [DQS Cleansing Transformation](data-flow/transformations/dqs-cleansing-transformation.md).  
  
 **O que você deseja fazer?**  
  
-   [Abra o Editor de Transformação de Limpeza DQS.](#open)  
  
-   [Definir as opções na guia de Gerenciador de Conexões](#connection)  
  
-   [Definir as opções na guia Mapeamento](#mapping)  
  
-   [Definir as opções na guia Avançado](#advanced)  
  
-   [Definir as opções na caixa de diálogo Gerenciador de Conexões de Limpeza DQS.](#manager)  
  
##  <a name="open"></a> Abra o Editor de Transformação de Limpeza DQS.  
  
1.  Adicione a Transformação de Limpeza DQS ao pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  Clique com o botão direito do mouse no componente e clique em **Editar**.  
  
##  <a name="connection"></a> Definir as opções na guia de Gerenciador de Conexões  
 **Gerenciador de conexões de qualidade de dados**  
 Selecione um gerenciador de conexões DQS existente na lista ou crie uma nova conexão clicando em **Novo**.  
  
 **Novo**  
 Crie um novo gerenciador de conexões, usando a caixa de diálogo **Gerenciador de Conexões de Limpeza DQS** . Consulte [Definir as opções na caixa de diálogo Gerenciador de Conexões de Limpeza DQS.](#manager)  
  
 **Base de conhecimento de qualidade de dados**  
 Selecione uma base de dados de conhecimento do DQS para a fonte de dados conectada. Para obter mais informações sobre a base de dados de conhecimento do DQS, consulte [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
 **Criptografar conexão**  
 Especifique se é preciso criptografar a conexão para criptografar a transferência de dados entre o Servidor DQS e o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 **Domínios disponíveis**  
 Liste os domínios disponíveis para a base de conhecimento selecionada. Há dois tipos de domínios: domínios únicos e domínios compostos que contêm dois ou mais domínios únicos.  
  
 Para obter mais informações sobre como mapear colunas para domínios compostos, consulte [Map Columns to Composite Domains](data-flow/transformations/map-columns-to-composite-domains.md).  
  
 Para obter mais informações sobre domínios, consulte [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
 **Configurar Saída de Erro**  
 Especifique como tratar erros em nível de linha. Podem ocorrer erros quando a transformação corrige dados da fonte de dados conectada, devido a valores de dados inesperados ou restrições de validação.  
  
 Os valores válidos são os seguintes:  
  
-   **Falha no Componente**, que indica que houve falha na transformação e os dados de entrada não são inseridos no banco de dados do Data Quality Services. Este é o valor padrão.  
  
-   **Redirecionar Linha**, que indica que os dados de entrada não estão inseridos no banco de dados do Data Quality Services e são redirecionados para a saída do erro.  
  
##  <a name="mapping"></a> Definir as opções na guia Mapeamento  
 Para obter mais informações sobre como mapear colunas para domínios compostos, consulte [Map Columns to Composite Domains](data-flow/transformations/map-columns-to-composite-domains.md).  
  
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
  
##  <a name="advanced"></a> Definir as opções na guia Avançado  
 **Padronizar saída**  
 Indique se é preciso produzir os dados no formato padronizado com base no formato de saída definido para domínios. Para obter mais informações sobre o formato padronizado, consulte [Limpeza de dados](../../2014/data-quality-services/data-cleansing.md).  
  
 **Confiança**  
 Indique se é preciso incluir o nível de confiança para os dados corrigidos. O nível de confiança indica a extensão de certeza do DQS para a correção ou sugestão. Para obter mais informações sobre níveis de confiança, consulte [Limpeza de dados](../../2014/data-quality-services/data-cleansing.md).  
  
 **Reason**  
 Indique se é preciso incluir a razão para a correção de dados.  
  
 **Dados acrescentados**  
 Indique se é preciso produzir dados adicionais que são recebidos de um provedor de dados de referência existente. Para obter mais informações, consulte [Reference Data Services in DQS](../../2014/data-quality-services/reference-data-services-in-dqs.md).  
  
 **Esquema de dados acrescentado**  
 Indique se é preciso produzir o esquema de dados. Para obter mais informações, consulte [anexar um domínio ou domínio composto para dados de referência](../../2014/data-quality-services/attach-a-domain-or-composite-domain-to-reference-data.md).  
  
##  <a name="manager"></a> Definir as opções na caixa de diálogo Gerenciador de Conexões de Limpeza DQS.  
 **Nome do servidor**  
 Selecione ou digite o nome do servidor DQS ao qual você deseja se conectar. Para obter mais informações sobre o servidor, consulte [DQS Administration](../../2014/data-quality-services/dqs-administration.md).  
  
 **Testar Conexão**  
 Clique para confirmar se a conexão especificada é viável.  
  
 Você também pode abrir a caixa de diálogo **Gerenciador de Conexões de Limpeza DQS** da área de conexões, fazendo o seguinte:  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra um projeto existente do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ou crie um novo projeto.  
  
2.  Clique com o botão direito do mouse na área de conexões, clique em **Nova Conexão**e, em seguida, clique em **DQS**.  
  
3.  Clique em **Adicionar**.  
  
## <a name="see-also"></a>Consulte também  
 [Aplicar regras de qualidade de dados à fonte de dados](data-flow/transformations/apply-data-quality-rules-to-data-source.md)  
  
  