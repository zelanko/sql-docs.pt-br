---
title: Nível de compatibilidade para modelos tabulares no Analysis Services | Microsoft Docs
ms.date: 06/10/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 19c69aa1a1ab27e7498d3c9d6a0d52c25b9f0020
ms.sourcegitcommit: c2a5bed031b14f66562f792a3afaefab8c759fda
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66826825"
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Nível de compatibilidade para modelos tabulares do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  O *nível de compatibilidade* refere-se aos aprimoramentos de recursos e funcionalidades no mecanismo do Analysis Services e nos metadados do modelo de tabela. Em geral, você deve escolher o nível de compatibilidade mais recente com suporte pelos servidores. 

  **O nível de compatibilidade com suporte mais recente é 1400** 
  
Os principais recursos no nível de compatibilidade 1400 incluem:

*  Nova infraestrutura para conectividade de dados e importação para modelos de tabela com suporte para APIs de TOM e scripts de TMSL. Isso habilita o suporte para fontes de dados adicionais, como o armazenamento de BLOBs do Azure. Dados adicionais de fontes será incluíam nas futuras atualizações.
*  Transformação de dados e recursos de mashup de dados usando expressões obter dados e M no SSDT SQL Server Data Tools ().
*  Mede agora suporte a uma propriedade de linhas de detalhes com uma expressão DAX, habilitando o BI de ferramentas, como simulação do Microsoft Excel para baixo até mais dados do relatório agregado. Por exemplo, quando os usuários visualizam o total de vendas de uma região e mês, eles podem exibir os detalhes do pedido associados. 
*  Segurança em nível de objeto para nomes de tabela e coluna, além dos dados dentro deles.
*  Suporte aprimorado para hierarquias desbalanceadas.
*  Monitoramento de desempenho e melhorias.

  
## <a name="supported-compatibility-levels-by-version"></a>Níveis de compatibilidade com suporte por versão
  
Níveis mais baixos de compatibilidade com versões anteriores têm suporte para compatibilidade. 

|||  
|-|-|- 
|**Nível de compatibilidade**|**Versão do servidor __**| 
|1470|2019 do SQL Server (CTP 2.3 e posteriores) | 
|1400|Azure Analysis Services, SQL Server 2019, SQL Server 2017 |  
|1200|Azure Analysis Services, SQL Server 2019, SQL Server 2017, SQL Server 2016| 
|1103|SQL Server 2017*, SQL Server 2016, SQL Server 2014, SQL Server 2012 SP1|  
|1100|SQL Server 2017*, SQL Server 2016, SQL Server 2014, SQL Server 2012 SP1, SQL Server 2012| 

\* níveis de compatibilidade 1100 e 1103 foram preteridos no SQL Server 2017 e versões posteriores.
  
## <a name="set-compatibility-level"></a>Definir nível de compatibilidade 
 Ao criar um novo projeto de modelo de tabela no SSDT SQL Server Data Tools (), você pode especificar o nível de compatibilidade sobre o **designer de modelo Tabular** caixa de diálogo. 
  
 ![ssas_tabularproject_compat1200](../../analysis-services/tabular-models/media/ssas-tabularproject-compat1200.png)  
  
 Se você selecionar o **não mostrar esta mensagem novamente** opção, todos os projetos subsequentes usarão o nível de compatibilidade especificada como padrão. É possível alterar o nível de compatibilidade padrão no SSDT em **Ferramentas** > **Opções**.  
  
 Para atualizar um projeto de modelo de tabela no SSDT, defina as **nível de compatibilidade** propriedade no modelo **propriedades** janela. Tenha em mente, o nível de compatibilidade de atualização é irreversível.
  
## <a name="check-compatibility-level-for-a-database-in-ssms"></a>Verificar o nível de compatibilidade de um banco de dados no SSMS  
 No SSMS, clique no nome do banco de dados > **propriedades** > **nível de compatibilidade**.  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>Verificar o nível de compatibilidade com suporte para um servidor no SSMS  
 No SSMS, clique com o botão direito do mouse no nome do servidor > **Propriedades** > **Nível de Compatibilidade com Suporte**.  

 Esta propriedade especifica o nível de compatibilidade mais alto de um banco de dados que serão executados no servidor. O nível de compatibilidade com suporte é somente leitura e não pode ser alterado.
 
> [!NOTE]  
>  No SSMS, quando conectado a um servidor SQL Server Analysis Services, o servidor Azure Analysis Services ou o espaço de trabalho do Power BI Premium, a propriedade de nível de compatibilidade com suporte mostrará 1200. Isso é um problema conhecido e será resolvido no SSMS futuro atualização. Quando resolvido, essa propriedade será mostrada o mais alto nível de compatibilidade com suporte. 
  
## <a name="see-also"></a>Confira também  
 [Nível de compatibilidade de um banco de dados multidimensional](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [What's new in Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [Criar um novo projeto de modelo de tabela](../../analysis-services/tabular-models/create-a-new-tabular-model-project-analysis-services.md)  
  
  
