---
title: "Nível de compatibilidade para modelos de tabela no Analysis Services | Microsoft Docs"
ms.custom: 
ms.date: 10/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.bidtoolset.versioncompat.f1
ms.assetid: 8943d78d-4a73-4be8-ad14-3d428f5abd06
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: d194cdfa2771b96f2ae1880f474b8a0107e0b67c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Nível de compatibilidade para modelos de tabela do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  O *nível de compatibilidade* refere-se a comportamentos específicos à versão no mecanismo do Analysis Services. Por exemplo, o DirectQuery e os metadados de objeto de tabela têm implementações diferentes dependendo do nível de compatibilidade. Em geral, você deve escolher o nível de compatibilidade mais recente com suporte pelos servidores.

  **O nível de compatibilidade mais recente é 1400** 
  
Os principais recursos do nível de compatibilidade 1400 incluem:

*  Nova infraestrutura para conectividade de dados e importar para modelos de tabela com suporte para APIs de TOM e scripts de TMSL. Isso habilita o suporte para fontes de dados adicionais, como armazenamento de BLOBs do Azure. Dados adicionais fontes será incluído nas futuras atualizações.
*  Transformação de dados e recursos de mashup de dados usando expressões de obter dados e M.
*  Medidas agora oferecem suporte a uma propriedade de linhas de detalhes com uma expressão DAX, permitindo que as ferramentas de BI como o Microsoft Excel drill-down dados detalhados de um relatório agregado. Por exemplo, quando os usuários finais exibe o total de vendas de uma região e mês, ele podem exibir os detalhes do pedido associado. 
*  Segurança em nível de objeto para nomes de tabela e coluna, além dos dados dentro deles.
*  Suporte aprimorado para hierarquias desbalanceadas.
*  Monitoramento de desempenho e melhorias.

  
## <a name="supported-compatibility-levels-by-version"></a>Níveis de compatibilidade com suporte pela versão
  
|||  
|-|-|- 
|**Nível de compatibilidade**|**Versão do servidor __**| 
|1400|Serviços de análise do Azure, SQL Server de 2017 |  
|1200|Serviços de análise do Azure, SQL Server de 2017, SQL Server 2016| 
|1103|SQL Server 2017 *, SQL Server 2016, SQL Server 2014, SQL Server 2012 SP1|  
|1100|SQL Server 2017 *, SQL Server 2016, SQL Server 2014, SQL Server 2012 SP1, SQL Server 2012| 

\*níveis de compatibilidade 1100 e 1103 foram preteridos no SQL Server 2017.
  
## <a name="set-compatibility-level"></a>Definir o nível de compatibilidade 
 Ao criar um novo projeto de modelo de tabela no SQL Server Data Tools (SSDT), você pode especificar o nível de compatibilidade no **designer de modelo Tabular** caixa de diálogo. 
  
 ![ssas_tabularproject_compat1200](../../analysis-services/tabular-models/media/ssas-tabularproject-compat1200.png)  
  
 Se você selecionar o **não mostrar esta mensagem novamente** opção, todos os projetos subsequentes usarão o nível de compatibilidade é especificado como o padrão. É possível alterar o nível de compatibilidade padrão no SSDT em **Ferramentas** > **Opções**.  
  
 Para atualizar um projeto de modelo de tabela no SSDT, defina o **nível de compatibilidade** propriedade no modelo **propriedades** janela. Tenha em mente, o nível de compatibilidade de atualização é irreversível.
  
## <a name="check-compatibility-level-for-a-database-in-ssms"></a>Verificar o nível de compatibilidade de um banco de dados no SSMS  
 No SSMS, clique no nome do banco de dados > **propriedades** > **nível de compatibilidade**.  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>Verificar o nível de compatibilidade com suporte para um servidor no SSMS  
 No SSMS, clique com o botão direito do mouse no nome do servidor > **Propriedades** > **Nível de Compatibilidade com Suporte**.  
  
 Essa propriedade especifica o nível de compatibilidade mais alto de um banco de dados que será executado no servidor. O nível de compatibilidade com suporte é somente leitura e não pode ser alterado.  
  
## <a name="see-also"></a>Consulte também  
 [Nível de compatibilidade de um banco de dados multidimensional](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [Novidades no Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [Criar um novo projeto de modelo de tabela](../../analysis-services/tabular-models/create-a-new-tabular-model-project-analysis-services.md)  
  
  
