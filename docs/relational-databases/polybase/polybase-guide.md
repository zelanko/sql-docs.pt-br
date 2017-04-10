---
title: "Guia do PolyBase | Microsoft Docs"
ms.date: "12/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-polybase"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
f1_keywords: 
  - "PolyBase"
  - "PolyBase, guide"
helpviewer_keywords: 
  - "PolyBase"
  - "PolyBase, visão geral"
  - "Importação do Hadoop ×"
  - "Exportação do Hadoop"
  - "Exportação do Hadoop, visão geral do PolyBase"
  - "Importação do Hadoop, visão geral do PolyBase"
ms.assetid: b42b7d48-328a-4046-abe9-f73fd83212dc
caps.latest.revision: 26
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 24
---
# Guia do PolyBase
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  O PolyBase é uma tecnologia que acessa e combina dados relacionais e não relacionais, tudo no próprio SQL Server.   Ele permite executar consultas em dados externos no Hadoop ou no armazenamento de blobs do Azure.   As consultas são otimizadas para enviar por push o cálculo para o Hadoop  
  
 Apenas usando instruções Transact-SQL (T-SQL), você realiza a importação e exportação de dados alternadamente entre tabelas relacionais no SQL Server e de dados não relacionais armazenados no Hadoop ou no Armazenamento de Blobs do Azure. Você também pode consultar os dados externos em uma consulta T-SQL e uni-los aos dados relacionais.  
  
 Para usar o PolyBase, veja [Introdução ao PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).  
  
 ![PolyBase logical](../../relational-databases/polybase/media/polybase-logical.png "PolyBase logical")  
  
## Por que usar o PolyBase?  
 Para tomar boas decisões, os tomadores de decisões de negócios precisam analisar dados relacionais e outros dados que não são estruturados em tabelas – especialmente, do Hadoop e de outras tecnologias NoSQL. Essa é uma tarefa difícil, a menos que você encontre uma maneira de transferir dados entre os diferentes tipos de armazenamentos de dados. O PolyBase preenche essa lacuna, operando em dados externos ao SQL Server.  
  
 Para simplificar, o PolyBase não exige a instalação de software adicional no ambiente do Azure ou do Hadoop.         A consulta de dados externos usa a mesma sintaxe que a consulta de uma tabela de banco de dados. Tudo isso acontece de forma transparente. O PolyBase cuida de todos os detalhes nos bastidores e, para usá-lo bem, não é necessário ter nenhum conhecimento sobre o Hadoop ou Azure.  
  
 O PolyBase pode:  
  
-   **Consulte os dados armazenados no Hadoop.** Os usuários estão armazenando dados em sistemas escalonáveis e distribuídos mais econômicos, como o Hadoop. O PolyBase facilita a consulta dos dados com T-SQL.  
  
-   **Consulte os dados armazenados no armazenamento de blobs do Azure.** O armazenamento de blobs do Azure é um local conveniente para armazenar dados para uso dos serviços do Azure.  O PolyBase facilita o acesso aos dados com T-SQL.  
  
-   **Importe dados de um armazenamento de blobs do Azure ou do Hadoop.** Aproveite a velocidade das funcionalidades de análise e tecnologia de columnstore do Microsoft SQL, com a importação de dados do Hadoop ou do armazenamento de blobs do Azure em tabelas relacionais. Não é necessário ter uma ferramenta separada de ETL ou importação.  
  
-   **Exporte os dados para o Hadoop ou um armazenamento de blobs do Azure.** Arquive dados no Hadoop ou no armazenamento de blobs do Azure para obter um armazenamento econômico e mantê-lo online para fácil acesso.  
  
-   **Integre com ferramentas de BI.** Use o PolyBase com a business intelligence e pilha de análise da Microsoft, ou use as ferramentas de terceiros compatíveis com o SQL Server.  
  
## Desempenho  
  
-   **Enviar por push o cálculo para o Hadoop.**O otimizador de consulta toma uma decisão baseada em custo para enviar por push o cálculo para o Hadoop quando essa ação implica uma melhoria no desempenho da consulta.  Ele usa as estatísticas de tabelas externas para tomar a decisão baseada em custo.   O envio por push do cálculo cria trabalhos MapReduce e aproveita os recursos computacionais distribuídos do Hadoop.  
  
-   **Escale os recursos de computação.** Para melhorar o desempenho da consulta, é possível usar os [grupos de escala horizontal do PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md) do SQL Server. Isso permite a transferência de dados em paralelo entre as instâncias do SQL Server e os nós do Hadoop, além de adicionar recursos de computação para operação em dados externos.  
  
## Tópicos do Guia do PolyBase  
 Este guia inclui tópicos para ajudá-lo a usar o PolyBase com eficiência e eficácia.  
  
|||  
|-|-|  
|**Tópico**|**Descrição**|  
|[Introdução ao PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)|Etapas básicas para instalar e configurar o PolyBase. Mostra como criar objetos externos que apontam para os dados no Hadoop ou no armazenamento de blobs do Azure e fornece exemplos de consulta.|  
|[Resumo de recursos com controle de versão do PolyBase](../../relational-databases/polybase/polybase-versioned-feature-summary.md)|Descreve quais recursos do PolyBase têm suporte no SQL Server, Banco de Dados SQL e SQL Data Warehouse.|  
|[Grupos de escala horizontal do PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md)|Expanda o paralelismo entre o SQL Server e o Hadoop usando grupos de escala horizontal do SQL Server.|  
|[Instalação do PolyBase](../../relational-databases/polybase/polybase-installation.md)|A referência e as etapas para instalação do PolyBase com o assistente de instalação ou com uma ferramenta de linha de comando.|  
|[Configuração do PolyBase](../../relational-databases/polybase/polybase-configuration.md)|Defina as configurações do SQL Server para o PolyBase.  Por exemplo, configure a aplicação de computação e a segurança do Kerberos.|  
|[Objetos T-SQL do PolyBase](../../relational-databases/polybase/polybase-t-sql-objects.md)|Crie os objetos do T-SQL usados pelo PolyBase para definir e acessar dados externos.|  
|[Consultas do PolyBase](../../relational-databases/polybase/polybase-queries.md)|Use instruções T-SQL para consultar, importar ou exportar dados externos.|  
|[Solucionando problemas do PolyBase](../../relational-databases/polybase/polybase-troubleshooting.md)|Técnicas para gerenciar consultas do PolyBase. Use DMVs (exibições de gerenciamento dinâmico) para monitorar consultas do PolyBase e saiba como ler um plano de consulta do PolyBase para encontrar afunilamentos de desempenho.|  
  
  