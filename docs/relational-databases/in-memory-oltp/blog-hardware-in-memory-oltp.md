---
title: Hardware para OLTP in-memory do SQL | Microsoft Docs
description: Saiba mais sobre as considerações de hardware para o desempenho do OLTP in-memory no SQL Server. O OLTP in-memory usa a memória e o disco de maneiras diferentes das tabelas baseadas em disco.
ms.custom: ''
ms.date: 03/28/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017
ms.openlocfilehash: 09483122764de51b565693d85c3ae8efa9a8c570
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465347"
---
# <a name="hardware-considerations-for-in-memory-oltp-in-sql-server"></a>Considerações sobre hardware para OLTP in-memory no SQL Server

O OLTP in-memory usa a memória e o disco de maneiras diferentes das tabelas baseadas em disco tradicionais. A melhoria de desempenho gerada pelo OLTP in-memory depende do hardware que você usa. Nesta postagem no blog, discutimos diversas considerações sobre hardware e fornecemos diretrizes gerais para o hardware a ser usado com o OLTP in-memory.

> [!NOTE]
> Este artigo foi publicado em um blog em 1º de agosto de 2013 pela equipe do Microsoft SQL Server 2014. A página da Web do blog que está sendo desativada.
>
> [OLTP in-memory do SQL Server](./in-memory-oltp-in-memory-optimization.md)

<!--
    Here was the link to the blog. This blog was captured into this new article on 2018/11/30, by GeneMi (MightyPen).
    https://cloudblogs.microsoft.com/sqlserver/2013/08/01/hardware-considerations-for-in-memory-oltp-in-sql-server-2014/
    At least one pre-existing article that contained the obsolete blog link was:
        relational-databases\in-memory-oltp\sample-database-for-in-memory-oltp.md
-->

## <a name="cpu"></a>CPU

O OLTP in-memory não exige um servidor de alto nível para ser compatível com a elevada taxa de transferência da carga de trabalho do OLTP. É recomendável usar um servidor de nível médio com dois soquetes na CPU. Por causa da maior taxa de transferência gerada pelo OLTP in-memory, provavelmente dois soquetes serão o suficiente para suas necessidades empresariais.

É recomendável para ativar o hiper-threading com o OLTP in-memory. Com algumas cargas de trabalho OLTP, houve ganhos de desempenho de até 40% ao usar o hyper-threading.

## <a name="memory"></a>Memória

Todas as tabelas com otimização de memória residem totalmente na memória. Portanto, é necessário ter memória física suficiente para as próprias tabelas e para sustentar a carga de trabalho executada no banco de dados. A quantidade de memória realmente necessária depende da carga de trabalho, mas como ponto de partida, você provavelmente desejará memória disponível suficiente para cerca de duas vezes o tamanho dos dados. Você também precisará de memória suficiente para o pool de buffers caso a carga de trabalho também opere em tabelas baseadas em disco tradicionais.

Para determinar a quantidade de memória usada por uma determinada tabela com otimização de memória, execute a seguinte consulta:

```sql
select object_name(object_id), * from sys.dm_db_xtp_table_memory_stats;
```

Os resultados mostrarão a memória usada para tabelas com otimização de memória e seus índices. Os dados da tabela incluem os dados do usuário, bem como todas as versões de linha mais antigas que ainda são necessárias, que executam transações ou que não ainda foram limpas pelo sistema. A memória usada pelos índices de hash é constante e não depende do número de linhas na tabela.

Ao usar o OLTP in-memory, é importante lembrar que todo o banco de dados não precisa caber na memória. É possível ter um banco de dados de vários terabytes e ainda se beneficiar do OLTP in-memory, desde que o tamanho dos dados frequentes (por exemplo, tabelas com otimização de memória) não exceda 256 GB. O número máximo de arquivos de dados do ponto de verificação que o SQL Server pode gerenciar em um único banco de dados individual é 4 mil, sendo que cada arquivo precisa ter 128 MB. Embora isso resulte em um máximo teórico de 512 GB, para garantir que o SQL Server possa acompanhar a mesclagem de arquivos do ponto de verificação e não atinja o limite de 4 mil arquivos, disponibilizamos até 256 GB. Esse limite se aplica somente às tabelas com otimização de memória. Não há limitação de tamanho para as tabelas baseadas em disco tradicionais no mesmo banco de dados do SQL Server.

As NDTs (tabelas com otimização de memória não duráveis), por exemplo, tabelas com otimização de memória com DURABILITY=SCHEMA_ONLY, não persistem no disco. Embora as NDTs não sejam limitadas pelo número de arquivos do ponto de verificação, somente há suporte para 256 GB. As considerações para unidades de log e dados no restante desta postagem não se aplicam às tabelas não duráveis, porque os dados só existem na memória.

## <a name="log-drive"></a>Unidade de log

Os registros de log que pertencem às tabelas com otimização de memória são gravados no log de transações do banco de dados, junto com outros registros de log do SQL Server.

É sempre importante colocar o arquivo de log em uma unidade com baixa latência, de modo que as transações não precisem esperar muito e para evitar a contenção na E/S do log. O sistema será executado na velocidade do componente mais lento (Lei de Amdahl). É necessário garantir que, ao executar o OLTP in-memory, o dispositivo de E/S do log não se transforme em um gargalo. É recomendável usar um dispositivo de armazenamento com baixa latência, pelo menos SSD.

As tabelas com otimização de memória usam menos largura de banda de log que as tabelas baseadas em disco, porque elas não registram operações de índice nem registros UNDO. Isso pode ajudar a aliviar a contenção de E/S de log.

## <a name="data-drive"></a>Unidade de dados

A persistência de tabelas com otimização de memória que usam arquivos do ponto de verificação utiliza E/S de streaming. Portanto, esses arquivos não precisam de uma unidade com baixa latência ou de E/S aleatórias rápidas. Em vez disso, o fator principal para essas unidades é a velocidade de E/S sequencial e a largura de banda do HBA (adaptador de barramento do host). Portanto, você não precisa de SSDs para os arquivos do ponto de verificação. É possível inseri-los em eixos de alto desempenho (por exemplo, SAS), desde que a velocidade de E/S sequencial atenda às suas necessidades.

O principal fator para determinar o requisito de velocidade é o RTO (Objetivo do Tempo de Recuperação) na reinicialização do servidor. Durante a recuperação do banco de dados, todos os dados nas tabelas com otimização de memória precisam ser lidos do disco, na memória. A recuperação do banco de dados ocorre na velocidade de leitura sequencial do subsistema de E/S. O disco é o gargalo.

Para atender aos requisitos de RTO, é recomendável distribuir os arquivos do ponto de verificação em vários discos, adicionando diversos contêineres ao grupo de arquivos MEMORY_OPTIMIZED_DATA. O SQL Server é compatível com o carregamento paralelo de arquivos do ponto de verificação de várias unidades – a recuperação ocorre na velocidade agregada das unidades.

Em termos de capacidade de disco, é recomendável ter um tamanho de duas a três vezes maior que o disponível para as tabelas com otimização de memória.

## <a name="see-also"></a>Confira também

[Banco de dados de exemplo para OLTP in-memory](sample-database-for-in-memory-oltp.md)