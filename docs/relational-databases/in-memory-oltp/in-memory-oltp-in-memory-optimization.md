---
title: OLTP in-memory (otimização na memória) | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- In-Memory OLTP
- memory-optimized tables
ms.assetid: e1d03d74-2572-4a55-afd6-7edf0bc28bdb
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 87ad093d5be6f4fa394e934e6c0d88796a22e196
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74401649"
---
# <a name="in-memory-oltp-and-memory-optimization"></a>OLTP in-memory e otimização de memória

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

 O[!INCLUDE[hek_2](../../includes/hek-2-md.md)] pode melhorar significativamente o desempenho de processamento de transações, inclusão de dados e carregamento de dados, e cenários de dados temporário.  Para ir diretamente para o código básico e o conhecimento necessário para testar rapidamente sua própria tabela com otimização de memória e o procedimento armazenado nativamente, veja
 -  [Início rápido 1: tecnologias do OLTP in-memory para um desempenho mais rápido do Transact-SQL](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md).  
 
Carregamos no YouTube um [**vídeo de 17 minutos**](#anchorname-17minute-video) explicando o OLTP in-memory no SQL Server e demonstrando os benefícios de desempenho.

Para obter uma visão geral mais detalhada do OLTP in-memory e uma análise de cenários que desfrutam dos benefícios de desempenho da tecnologia:

- [Visão geral e cenários de uso](../../relational-databases/in-memory-oltp/overview-and-usage-scenarios.md)
 
 Observe que [!INCLUDE[hek_2](../../includes/hek-2-md.md)] é a tecnologia do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para melhoria de desempenho do processamento de transações. Para obter a tecnologia do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que melhora o desempenho de consulta de relatório e analítica, veja [Guia de índices columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md).
  
 Várias melhorias foram feitas no OLTP in-memory do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)], bem como do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. A área de superfície do Transact-SQL foi aumentada para facilitar a migração de aplicativos de banco de dados. O suporte para operações de ALTER para tabelas com otimização de memória e procedimentos armazenados compilados nativamente foi adicionado para facilitar a manutenção de aplicativos.
  
> [!NOTE]  
>  **Experimente**  
>   
>  O OLTP in-memory está disponível nas camadas Premium e Comercialmente Crítica de bancos de dados SQL do Azure e em pools elásticos. Para começar a usar o OLTP in-memory, bem como o Columnstore no Banco de Dados SQL do Azure, veja [Otimizar o desempenho usando tecnologias in-memory no Banco de Dados SQL](https://azure.microsoft.com/documentation/articles/sql-database-in-memory/).  
  

## <a name="in-this-section"></a>Nesta seção  
 Esta seção inclui os seguintes tópicos:  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Início rápido 1: tecnologias do OLTP in-memory para um desempenho mais rápido do Transact-SQL](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)|Delve diretamente no OLTP in-memory|
|[Visão geral e cenários de uso](../../relational-databases/in-memory-oltp/overview-and-usage-scenarios.md)|Visão geral do que é o OLTP in-memory e quais são os cenários que desfrutam dos benefícios de desempenho.|
|[Requisitos para usar tabelas com otimização de memória](../../relational-databases/in-memory-oltp/requirements-for-using-memory-optimized-tables.md)|Aborda os requisitos de hardware e software, e as diretrizes para usar tabelas com otimização de memória.|  
|[Exemplos de código do OLTP in-memory](../../relational-databases/in-memory-oltp/in-memory-oltp-code-samples.md)|Contém exemplos de código que mostram como criar e usar uma tabela com otimização de memória.|  
|[Memory-Optimized Tables](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)|Apresenta tabelas com otimização de memória.|  
|[Variáveis de tabela com otimização de memória](https://msdn.microsoft.com/library/bd102e95-53e2-4da6-9b8b-0e4f02d286d3)|Exemplo de código mostrando como usar uma variável de tabela com otimização de memória em vez de uma variável de tabela tradicional para reduzir o uso de tempdb.|  
|[Índices em tabelas com otimização de memória](https://msdn.microsoft.com/library/86805eeb-6972-45d8-8369-16ededc535c7)|Incorpora índices com otimização de memória.|  
|[Procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)|Apresenta procedimentos armazenados compilados de modo nativo.|  
|[Gerenciando memória para OLTP in-memory](https://msdn.microsoft.com/library/d82f21fa-6be1-4723-a72e-f2526fafd1b6)|Compreendendo e gerenciando o uso de memória no sistema.|  
|[Criando e gerenciando armazenamento para objetos com otimização de memória](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)|A aborda os arquivos delta e de dados, que armazenam informações sobre transações em tabelas com otimização de memória.|  
|[Backup, restauração e recuperação de tabelas com otimização de memória](https://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)|Discute backup, restauração e recuperação de tabelas com otimização de memória.|  
|[Suporte ao Transact-SQL para OLTP in-memory](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)|Discute o suporte do [!INCLUDE[tsql](../../includes/tsql-md.md)] para [!INCLUDE[hek_2](../../includes/hek-2-md.md)].|  
|[Suporte de alta disponibilidade para bancos de dados do OLTP in-memory](../../relational-databases/in-memory-oltp/high-availability-support-for-in-memory-oltp-databases.md)|Discute grupos de disponibilidade e clustering de failover no [!INCLUDE[hek_2](../../includes/hek-2-md.md)].|  
|[Suporte ao SQL Server para OLTP na memória](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)|Lista a sintaxe nova e atualizada, e os recursos que oferecem suporte a tabelas com otimização de memória.|  
|[Migrando para OLTP na memória](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)|Aborda como migrar tabelas baseadas em disco para tabelas com otimização de memória.|  
| &nbsp; | &nbsp; |

## <a name="links-to-other-websites"></a>Links para outros sites

Esta seção fornece links para outros sites que contêm informações sobre OLTP in-memory no SQL Server.

- [**Vídeo** explicando o OLTP in-memory e demonstrando os benefícios de desempenho](#anchorname-17minute-video)

- [Demonstração do desempenho do OLTP in-memory v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)

-   [White paper técnico sobre as operações internas do OLTP in-memory no SQL Server](https://msdn.microsoft.com/library/mt764316.aspx)  

-   [Comparação de recursos de Columnstore e OLTP in-memory do SQL Server](https://download.microsoft.com/download/D/0/0/D0075580-6D72-403D-8B4D-C3BD88D58CE4/SQL_Server_2016_In_Memory_OLTP_and_Columnstore_Comparison_White_Paper.pdf)

-   Novidades no OLTP in-memory no SQL Server 2016, [Parte 1](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/11/12/in-memory-oltp-whats-new-in-sql2016-ctp3/) e [Parte 2](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/25/whats-new-for-in-memory-oltp-in-sql-server-2016-since-ctp3/)
  
-   [OLTP in-memory – Padrões comuns de carga de trabalho e considerações sobre migração](https://msdn.microsoft.com/library/dn673538.aspx)  
  
-   [Blog do OLTP in-memory](https://go.microsoft.com/fwlink/?LinkId=311696)  

## <a name="anchorname-17minute-video"></a> vídeo de 17 minutos, indexado

- _Título do vídeo:_ &nbsp; **OLTP in-memory no SQL Server 2016**
- _Data de publicação:_ &nbsp; 10/03/2019, em `YouTube.com`.
- _Duração:_ &nbsp; 17:32 &nbsp; &nbsp; (Confira o seguinte [**Índice**](#anchorname-index-17minute-video) para obter links para o vídeo.)
- _Hospedado por:_ &nbsp; Jos de Bruijn, gerente de programa sênior no SQL Server

### <a name="demo-can-be-downloaded"></a>A demonstração pode ser baixada

Na marcação de tempo 08:09, o vídeo executa uma demonstração duas vezes. Você pode baixar o código-fonte para a demonstração de desempenho executável usada no vídeo do seguinte link:

- [Demonstração do desempenho do OLTP in-memory v1.0, código-fonte](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)

As etapas gerais vistas no vídeo são as seguintes:

1. Primeiro, a demonstração é executada com uma tabela normal.
2. Em seguida, vemos uma edição com otimização de memória da tabela ser criada e populada usando alguns cliques no SQL Server Management Studio (SSMS.exe).
3. Em seguida, a demonstração é executada novamente com a tabela com otimização de memória. Uma enorme melhoria na velocidade é medida.

### <a name="anchorname-index-17minute-video"></a>Índice para cada seção no vídeo

| Link da marca de tempo | Título da seção |
| :------------- | :------------ |
| A.&nbsp; [00:00](https://www.youtube.com/watch?v=l5l5eophmK4&t=0) | O início. |
| <br/>B.&nbsp; [00:56](https://www.youtube.com/watch?v=l5l5eophmK4&t=56) | <br/>Por que os clientes devem se importar com o OLTP in-memory. |
| &nbsp; &nbsp; [01:03](https://www.youtube.com/watch?v=l5l5eophmK4&t=63) | O hardware moderno requer uma arquitetura moderna de sistema de banco de dados. |
| &nbsp; &nbsp; [02:10](https://www.youtube.com/watch?v=l5l5eophmK4&t=130) | Explosão nos dados gerados; as operações precisam ser instantâneas (baixa latência). |
| &nbsp; &nbsp; [03:19](https://www.youtube.com/watch?v=l5l5eophmK4&t=199) | Redução do TCO – fazer mais com os recursos que você tem. |
| <br/>C.&nbsp; [03:33](https://www.youtube.com/watch?v=l5l5eophmK4&t=213) | <br/>O que é OLTP in-memory.<br/>Desempenho otimizado usando tecnologia com otimização de memória. |
| &nbsp; &nbsp; [05:03](https://www.youtube.com/watch?v=l5l5eophmK4&t=303) | Processamento de transações até 30 vezes mais rápido. |
| &nbsp; &nbsp; [05:22](https://www.youtube.com/watch?v=l5l5eophmK4&t=322) | Os dados são totalmente duráveis; sobrevivem a falhas do servidor. |
| &nbsp; &nbsp; [06:15](https://www.youtube.com/watch?v=l5l5eophmK4&t=375) | Totalmente integrado ao SQL Server. Portanto, não há novas linguagens ou ferramentas para aprender. |
| &nbsp; &nbsp; [07:22](https://www.youtube.com/watch?v=l5l5eophmK4&t=442) | Lançado pela primeira vez no SQL Server 2014, mas com grandes melhorias em 2016. |
| &nbsp; &nbsp; [07:58](https://www.youtube.com/watch?v=l5l5eophmK4&t=558) | Disponível também no Banco de Dados SQL do Azure (na nuvem). |
| <br/>D.&nbsp; [08:09](https://www.youtube.com/watch?v=l5l5eophmK4&t=489) | <br/>Demonstração de desempenho.<br/> Executar a demonstração com uma tabela normal. |
| &nbsp; &nbsp; [09:11](https://www.youtube.com/watch?v=l5l5eophmK4&t=551) | Menu de contexto do SSMS: **Relatórios** &gt; **Análise de desempenho da transação** |
| &nbsp; &nbsp; [10:38](https://www.youtube.com/watch?v=l5l5eophmK4&t=638) | Menu de contexto do SSMS: **Orientador de otimização da memória**<br/> &nbsp; &nbsp; De fato criar uma tabela com otimização de memória usando uma tabela normal, além de migrar os dados. |
| &nbsp; &nbsp; [11:28](https://www.youtube.com/watch?v=l5l5eophmK4&t=688) | Executar a demonstração novamente, observar melhoria de 45 vezes na velocidade. |
| <br/>E.&nbsp; [12:17](https://www.youtube.com/watch?v=l5l5eophmK4&t=737) | <br/>É mais fácil usar o OLTP in-memory no SQL Server 2016 (em comparação com o 2014). |
| &nbsp; &nbsp; [12:43](https://www.youtube.com/watch?v=l5l5eophmK4&t=763) | Análise simplificada para ajudar na migração do aplicativo. |
| &nbsp; &nbsp; [13:03](https://www.youtube.com/watch?v=l5l5eophmK4&t=783) | Redução da complexidade da migração de aplicativos por meio do aumento do suporte à linguagem Transact-SQL (por exemplo, com chaves estrangeiras e gatilhos). |
| &nbsp; &nbsp; [13:56](https://www.youtube.com/watch?v=l5l5eophmK4&t=836) | Melhor capacidade de gerenciamento.<br/> &nbsp; &nbsp; Por exemplo, alterar esquema e índices, atualização automática de estatísticas. |
| <br/>F.&nbsp; [14:46](https://www.youtube.com/watch?v=l5l5eophmK4&t=886) | <br/>Melhor escalabilidade. |
| &nbsp; &nbsp; [15:12](https://www.youtube.com/watch?v=l5l5eophmK4&t=912) | Grandes tabelas com otimização de memória (até 2 TB por banco de dados). |
| &nbsp; &nbsp; [15:34](https://www.youtube.com/watch?v=l5l5eophmK4&t=934) | Dimensionamento ainda melhor. |
| &nbsp; &nbsp; [16:41](https://www.youtube.com/watch?v=l5l5eophmK4&t=1001) | Faça mais com os recursos que você já tem! |
| <br/>G.&nbsp; [16:53](https://www.youtube.com/watch?v=l5l5eophmK4&t=1013) | <br/>Comentários finais. (Termina em 17:32.) |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Confira também  
 [Recursos de banco de dados](../../relational-databases/database-features.md)  
  
  
