---
title: Guia do PolyBase | Microsoft Docs
ms.date: 05/31/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: polybase
ms.tgt_pltfrm: ''
ms.topic: quickstart
f1_keywords:
- PolyBase
- PolyBase, guide
helpviewer_keywords:
- PolyBase
- PolyBase, overview
- Hadoop import
- Hadoop export
- Hadoop export, PolyBase overview
- Hadoop import, PolyBase overview
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c31f9538f3429ff4ae1182ee0cd974996cc705a6
ms.sourcegitcommit: 82bb56269faf3fb5dd1420418e32a0a6476780cc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2018
ms.locfileid: "43694719"
---
# <a name="polybase-guide"></a>Guia do PolyBase

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]

O PolyBase permite que a instância do SQL Server 2016 processar consultas Transact-SQL que leem dados do Hadoop. A mesma consulta também pode acessar tabelas relacionais no SQL Server. O PolyBase permite que a mesma consulta também unir os dados do Hadoop e do SQL Server. No SQL Server, um [tabela externa](../../t-sql/statements/create-external-table-transact-sql.md) ou [fonte de dados externa](../../t-sql/statements/create-external-data-source-transact-sql.md) fornece a conexão para o Hadoop.

O PolyBase fornece essas mesmas funcionalidades para os seguintes produtos SQL da Microsoft:

- SQL Server 2016 e versões posteriores
- O Analytics Platform System (anteriormente conhecido como Parallel Data Warehouse)
- Azure SQL Data Warehouse

O PolyBase envia alguns cálculos para o nó de Hadoop para otimizar a consulta geral. No entanto, o acesso externo do PolyBase não é limitado ao Hadoop. Outras tabelas relacionais não estruturadas também são suportadas, como arquivos de texto delimitado.

#### <a name="data-import-and-export"></a>Exportação e Importação de Dados

Com a Ajuda subjacente do PolyBase, consultas T-SQL também podem importar e exportar dados do Armazenamento de Blobs do Azure. Além disso, o PolyBase permite que o SQL Data Warehouse do Azure importe/exporte dados do Armazenamento de Blobs do Azure e do Azure Data Lake Store.

Para usar o PolyBase, veja [Introdução ao PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).
  
![PolyBase lógico](../../relational-databases/polybase/media/polybase-logical.png "PolyBase lógico")

## <a name="why-use-polybase"></a>Por que usar o PolyBase?

No passado, era mais difícil unir os dados do SQL Server com dados externos. Você tinha estas duas opções desagradáveis:

- Transferir metade os dados para que todos os seus dados ficassem em um formato ou em outro.
- Consultar ambas as fontes de dados, então escrever lógica de consulta personalizada para ingressar e integrar os dados no nível do cliente.

O PolyBase evita essas opções desagradáveis usando T-SQL para unir os dados

Para simplificar, o PolyBase não exige instalação de software adicional no ambiente do Hadoop. Você pode consultar dados externos usando a mesma sintaxe do T-SQL usada para consultar uma tabela de banco de dados. As ações de suporte implementadas pelo PolyBase todos ocorrem de maneira transparente. O autor da consulta não precisa de nenhum conhecimento sobre o Hadoop.

O PolyBase pode:

- **Consultar dados armazenados no Hadoop do SQL Server ou do PDW.** Os usuários estão armazenando dados em sistemas escalonáveis e distribuídos mais econômicos, como o Hadoop. O PolyBase facilita a consulta dos dados com T-SQL.

- **Consulte os dados armazenados no Armazenamento de Blobs do Azure.** O armazenamento de blobs do Azure é um local conveniente para armazenar dados para uso dos serviços do Azure.  O PolyBase facilita o acesso aos dados com T-SQL.

- **Importe dados do Hadoop, do Armazenamento de Blobs do Azure ou do Azure Data Lake Store.** Aproveite a velocidade das funcionalidades de análise e tecnologia de columnstore do Microsoft SQL, com a importação de dados do Hadoop, do Armazenamento de Blobs do Azure ou do Azure Data Lake Store em tabelas relacionais. Não é necessário ter uma ferramenta separada de ETL ou importação.

- **Exporte dados para o Hadoop, o Armazenamento de Blobs do Azure ou o Azure Data Lake Store.** Arquive dados no Hadoop, no Armazenamento de Blobs do Azure ou no Azure Data Lake Store para obter um armazenamento econômico e mantê-los online para fácil acesso.

- **Integre com ferramentas de BI.** Use o PolyBase com a business intelligence e a pilha de análise da Microsoft ou use as ferramentas de terceiros compatíveis com o SQL Server.

## <a name="performance"></a>Desempenho

- **Enviar por push de computação para Hadoop.** O otimizador de consulta faz uma decisão baseada em custo para enviar por push computação para Hadoop, quando então será melhorar desempenho da consulta.  Ele usa as estatísticas de tabelas externas para tomar a decisão baseada em custo. O envio por push do cálculo cria trabalhos MapReduce e aproveita os recursos computacionais distribuídos do Hadoop.

- **Escale os recursos de computação.** Para melhorar o desempenho da consulta, é possível usar os [grupos de escala horizontal do PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md)do SQL Server. Isso permite a transferência de dados em paralelo entre as instâncias do SQL Server e os nós do Hadoop, além de adicionar recursos de computação para operação em dados externos.

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
| &nbsp; | &nbsp; |
  
