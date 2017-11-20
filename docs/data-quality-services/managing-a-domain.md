---
title: "Gerenciando um domínio | Microsoft Docs"
ms.custom: 
ms.date: 07/31/2012
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c5ab71a3-0dac-45b1-be8e-93bf7e0e03ce
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 13743e56a9965e9a417b7c8222a7fa534b7feced
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="managing-a-domain"></a>Gerenciando um domínio
  Este tópico descreve o uso de domínios no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Um domínio contém uma representação semântica dos dados em um campo específico na fonte de dados que será analisada. Um domínio faz parte da base de dados de conhecimento que você cria para uma fonte de dados e o conhecimento que acumula analisando uma amostra da fonte de dados ou importando dados é adicionado aos domínios definidos na base de dados de conhecimento. O conhecimento nesses domínios é usado depois para executar a limpeza e a correspondência em um projeto de qualidade de dados. Os domínios estão ao núcleo de todas as atividades no Data Quality Services.  
  
 Um domínio é mapeado para um campo de fonte de dados e é populado nas atividades de descoberta da base de dados de conhecimento, gerenciamento de domínio e correspondência. O modo como você carrega dados a partir da fonte de dados e dos dados da saída em um relatório é definido nas propriedades de domínio. Quando você usa um provedor de dados de referência para limpar dados, associa um serviço de dados de referência a um domínio único ou composto. Você cria regras para serem aplicadas nos dados em um domínio e pode criar relações baseadas em termos para um domínio. Você pode exibir e corrigir dados no domínio.  
  
 Também pode criar um domínio composto que abrange dois ou mais domínios individuais que contêm conhecimentos sobre dados comuns. Para obter mais informações, consulte [Gerenciando um domínio de composição](../data-quality-services/managing-a-composite-domain.md).  
  
## <a name="domain-properties"></a>Propriedades do Domínio  
 Quando você cria um domínio, tem as opções a seguir para populá-lo a partir da fonte de dados e apresentar a saída dos valores de domínio. Para obter mais informações, consulte [Definir propriedades de domínio](../data-quality-services/set-domain-properties.md).  
  
-   Selecione o tipo dos dados com o qual você popula o domínio. Para obter informações sobre tipos de dados com suporte para cada tipo de dados de domínio, consulte [O SQL Server com suporte e tipos de dados do SSIS para domínios do DQS](../data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md).  
  
-   Especifique que apenas valores principais, não seus sinônimos, sairão do domínio.  
  
-   Especifique que valores de domínio serão apresentados em um certo formato, dependendo do tipo de dados.  
  
-   Se o tipo de dados for uma cadeia de caracteres, você poderá normalizar a cadeia de caracteres removendo caracteres especiais quando a cadeia de caracteres for carregada a partir da fonte de dados para o domínio.  
  
-   Se o tipo de dados for uma cadeia de caracteres, você poderá executar o Verificador Ortográfico do DQS para verificar a sintaxe, a ortografia e a estrutura de sentença da cadeia de caracteres e indicar os erros em potencial na página **Valores de Domínio** do **Gerenciamento de Domínio**. Isso inclui especificar o idioma em que o Verificador Ortográfico será executado.  
  
-   Se o tipo de dados for uma cadeia de caracteres, você poderá especificar que o DQS não identificará erros de sintaxe quando souber que erros de sintaxe não ocorrerão nas cadeias de caracteres.  
  
## <a name="in-this-section"></a>Nesta seção  
 O uso de um domínio permite a você o seguinte:  
  
|||  
|-|-|  
|Criar uma representação semântica de um campo de dados com um tipo de dados específico, especificar como o domínio é populado e formatar a saída do domínio|[Criar um domínio](../data-quality-services/create-a-domain.md)|  
|Vincular um domínio a outro, permitindo o compartilhamento das mesmas configurações e valores|[Criar um domínio vinculado](../data-quality-services/create-a-linked-domain.md)|  
|Associar um serviço de dados de referência a um domínio único ou composto|[Anexar domínio ou domínio de composição para dados de referência](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)|  
|Alterar ou aumentar os valores em uma base de dados de conhecimento|[Alterar valores de domínio](../data-quality-services/change-domain-values.md)|  
|Usar regras de validação e padronização|[Criar uma regra de domínio](../data-quality-services/create-a-domain-rule.md)|  
|Usar relações para corrigir um termo que faz parte de um valor em um domínio|[Criar relações baseadas em termos](../data-quality-services/create-term-based-relations.md)|  
|Concluir, fechar ou cancelar a atividade de gerenciamento de domínio|[Encerrar a atividade Gerenciamento de Domínio](http://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0)|  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Criar uma base de dados de conhecimento executando a descoberta da base de dados de conhecimento e gerenciando o conhecimento de modo interativo|[Criar uma base de dados de conhecimento](../data-quality-services/building-a-knowledge-base.md)|  
|Importar ou exportar conhecimento para/de uma base de dados de conhecimento.|[Importar e exportar conhecimento](../data-quality-services/importing-and-exporting-knowledge.md)|  
|Criar um domínio composto e adicionar conhecimento ao domínio.|[Gerenciar um domínio de composição](../data-quality-services/managing-a-composite-domain.md)|  
  
  

