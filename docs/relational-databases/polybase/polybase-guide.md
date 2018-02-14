---
title: Guia do PolyBase | Microsoft Docs
ms.date: 05/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: polybase
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: get-started-article
f1_keywords:
- PolyBase
- PolyBase, guide
helpviewer_keywords:
- PolyBase
- PolyBase, overview
- "Hadoop import ×"
- Hadoop export
- Hadoop export, PolyBase overview
- Hadoop import, PolyBase overview
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: 13f4dc7e877341917ebf4f41694cb886c81c53f2
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="polybase-guide"></a>Guia do PolyBase
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
O PolyBase é uma tecnologia que acessa dados fora do banco de dados por meio da linguagem t-sql.  No SQL Server 2016, ela permite executar consultas em dados externos no Hadoop ou importar/exportar dados do Armazenamento de Blobs do Azure. As consultas são otimizadas para enviar por push o cálculo para o Hadoop. No SQL Data Warehouse do Azure, é possível importar/exportar dados do Armazenamento de Blobs do Azure e do Azure Data Lake Store.
  
  
 Para usar o PolyBase, veja [Introdução ao PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).  
  
 ![PolyBase lógico](../../relational-databases/polybase/media/polybase-logical.png "PolyBase lógico")  
  
## <a name="why-use-polybase"></a>Por que usar o PolyBase?  
Para tomar boas decisões, você deseja analisar os dados relacionais e outros dados que não são estruturados em tabelas – especialmente, no Hadoop. Essa é uma tarefa difícil, a menos que você encontre uma maneira de transferir dados entre os diferentes tipos de armazenamentos de dados. O PolyBase preenche essa lacuna, operando em dados externos ao SQL Server.  
  
Para simplificar, o PolyBase não exige instalação de software adicional no ambiente do Hadoop. A consulta de dados externos usa a mesma sintaxe que a consulta de uma tabela de banco de dados. Tudo isso acontece de forma transparente. O PolyBase cuida de todos os detalhes nos bastidores e não é necessário que o usuário final tenha qualquer conhecimento sobre o Hadoop para consultar tabelas externas. 
  
 O PolyBase pode:  
  
-   **Consultar dados armazenados no Hadoop do SQL Server ou do PDW.** Os usuários estão armazenando dados em sistemas escalonáveis e distribuídos mais econômicos, como o Hadoop. O PolyBase facilita a consulta dos dados com T-SQL.  
  
-   **Consulte os dados armazenados no Armazenamento de Blobs do Azure.** O armazenamento de blobs do Azure é um local conveniente para armazenar dados para uso dos serviços do Azure.  O PolyBase facilita o acesso aos dados com T-SQL.  
  
-   **Importar dados do Hadoop, do Armazenamento de Blobs do Azure ou do Azure Data Lake Store** Aproveite a velocidade das funcionalidades de análise e tecnologia de columnstore do Microsoft SQL importando dados do Hadoop, do Armazenamento de Blobs do Azure ou do Azure Data Lake Store para tabelas relacionais. Não é necessário ter uma ferramenta separada de ETL ou importação.  

-   **Exporte dados para o Hadoop, o Armazenamento de Blobs do Azure ou o Azure Data Lake Store.** Arquive dados no Hadoop, no Armazenamento de Blobs do Azure ou no Azure Data Lake Store para obter um armazenamento econômico e mantê-los online para fácil acesso.  
  
-   **Integre com ferramentas de BI.** Use o PolyBase com a business intelligence e a pilha de análise da Microsoft ou use as ferramentas de terceiros compatíveis com o SQL Server.  
  
## <a name="performance"></a>Desempenho  
  
-   **Enviar por push o cálculo para o Hadoop.**O otimizador de consulta toma uma decisão baseada em custo para enviar por push o cálculo para o Hadoop quando essa ação implica uma melhoria no desempenho da consulta.  Ele usa as estatísticas de tabelas externas para tomar a decisão baseada em custo. O envio por push do cálculo cria trabalhos MapReduce e aproveita os recursos computacionais distribuídos do Hadoop.  
  
-   **Escale os recursos de computação.** Para melhorar o desempenho da consulta, é possível usar os [grupos de escala horizontal do PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md)do SQL Server. Isso permite a transferência de dados em paralelo entre as instâncias do SQL Server e os nós do Hadoop, além de adicionar recursos de computação para operação em dados externos.  
  
## <a name="polybase-guide-topics"></a>Tópicos do Guia do PolyBase  
 Este guia inclui tópicos para ajudá-lo a usar o PolyBase com eficiência e eficácia.  
  
|||  
|-|-|  
|**Tópico**|**Descrição**|  
|[Introdução ao PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)|Etapas básicas para instalar e configurar o PolyBase. Mostra como criar objetos externos que apontam para os dados no Hadoop ou no armazenamento de blobs do Azure e fornece exemplos de consulta.|  
|[Resumo de recursos com controle de versão do PolyBase](../../relational-databases/polybase/polybase-versioned-feature-summary.md)|Descreve quais recursos do PolyBase têm suporte no SQL Server, Banco de Dados SQL e SQL Data Warehouse.|  
|[grupos de escala horizontal do PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md)|Expanda o paralelismo entre o SQL Server e o Hadoop usando grupos de escala horizontal do SQL Server.|  
|[Instalação do PolyBase](../../relational-databases/polybase/polybase-installation.md)|A referência e as etapas para instalação do PolyBase com o assistente de instalação ou com uma ferramenta de linha de comando.|  
|[Configuração do PolyBase](../../relational-databases/polybase/polybase-configuration.md)|Defina as configurações do SQL Server para o PolyBase.  Por exemplo, configure a aplicação de computação e a segurança do Kerberos.|  
|[Objetos T-SQL do PolyBase](../../relational-databases/polybase/polybase-t-sql-objects.md)|Crie os objetos do T-SQL usados pelo PolyBase para definir e acessar dados externos.|  
|[Consultas do PolyBase](../../relational-databases/polybase/polybase-queries.md)|Use instruções T-SQL para consultar, importar ou exportar dados externos.|  
|[Solucionando problemas do PolyBase](../../relational-databases/polybase/polybase-troubleshooting.md)|Técnicas para gerenciar consultas do PolyBase. Use DMVs (exibições de gerenciamento dinâmico) para monitorar consultas do PolyBase e saiba como ler um plano de consulta do PolyBase para encontrar gargalos de desempenho.|  
  
  
