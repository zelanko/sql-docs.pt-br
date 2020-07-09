---
title: Escrevendo páginas | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- pages
ms.assetid: 409c8753-03c4-436d-839c-6a5879971551
author: pmasl
ms.author: pelopes
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c5ffdb81cd5c1242a6a97dcb978683488c5a755b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85998308"
---
# <a name="writing-pages"></a>Gravando páginas
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

A E/S de uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] inclui gravações lógicas e físicas. Uma gravação lógica acontece quando os dados são modificados em uma página no cache do buffer. Uma gravação física acontece quando a página é gravada do [cache do buffer](../relational-databases/memory-management-architecture-guide.md) no disco.

Quando uma página é modificada no cache do buffer, ela não é gravada imediatamente de volta no disco. Em vez disso, a página é marcada como suja. Isso significa que uma página pode ter mais de uma gravação lógica feita antes de ser gravada fisicamente no disco. Para cada gravação lógica, um registro de log de transações é inserido no cache de log que registra a modificação. Os registros de log devem ser gravados no disco antes de a página suja associada ser removida do cache do buffer e gravada no disco. O SQL Server usa uma técnica conhecida como log write-ahead que evita escrever uma página suja antes do registro de log associado ser gravado no disco. Isso é essencial ao funcionamento correto do gerenciador de recuperação. Para saber mais, veja [Log de transações write-ahead](../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md).

A ilustração a seguir mostra o processo de gravação de uma página de dados modificada.

![Writing_Pages](../relational-databases/media/writing-pages.gif)

Quando o gerenciador de buffer grava uma página, procura páginas suja adjacentes que podem ser incluídas em uma única operação de coleta e gravação. As páginas adjacentes têm IDs de página consecutivas e são do mesmo arquivo; as páginas não precisam ser contíguas na memória. A pesquisa continua para frente e para trás até acontecer um dos seguintes eventos:

 * Uma página limpa é encontrada.
 * 32 páginas são encontradas.
 * Uma página suja é encontrada e cujo LSN (número de sequência de log) ainda não foi liberado no log.
 * Uma página que não pode ser travada imediatamente é encontrada.

Dessa forma, o conjunto inteiro de páginas pode ser gravado no disco com uma única operação gather-write. 

Um pouco antes de uma página ser gravada, o formulário de proteção de página especificado no banco de dados é adicionado à página. Se a proteção de página interrompida for adicionada, a página deverá ser travada como EX (exclusivamente) para a E/S. Isso porque a proteção de página interrompida modifica a página, tornando-a inadequada para ser lida por qualquer outro thread. Se a proteção da página de soma de verificação for adicionada, ou o banco de dados não usar nenhuma proteção de dados, a página será travada com uma trava UP (atualizada) para a E/S. Essa trava evita que alguém modifique a página durante a gravação, mas ainda permite que os leitores a utilizem. Para saber mais sobre opções de proteção de página de E/S de disco, veja [Gerenciamento de buffer](../relational-databases/memory-management-architecture-guide.md).

Uma página suja é gravada no disco de três formas: 

* Gravação lenta   
 O gravador lento é um processo de sistema que mantém buffers livres disponíveis ao remover páginas usadas raramente do cache do buffer. As páginas sujas são gravadas primeiramente no disco. 

* Gravação adiantada   
 O processo de gravação ávida grava páginas de dados de alterações associadas com operações não registradas, como inserção em massa e seleção em. Esse processo permite a criação e a gravação em paralelo de páginas novas. Ou seja, a operação de chamada não precisa esperar até o término da operação inteira antes de gravar as páginas no disco.

* Ponto de verificação   
 O processo de ponto de verificação examina o cache do buffer periodicamente para buffers com páginas de um banco de dados especificado e grava todas as páginas sujas no disco. Os pontos de verificação economizam tempo durante uma recuperação posterior, pois criam um ponto em que todas as páginas sujas são gravadas no disco. O usuário pode solicitar uma operação de ponto de verificação usando o comando CHECKPOINT, ou o [!INCLUDE[ssDE](../includes/ssde-md.md)] pode gerar pontos de verificação automáticos com base na quantidade de espaço de log usado e o tempo decorrido desde o último ponto de verificação. Além disso, um ponto de verificação é gerado quando ocorrem determinadas atividades. Por exemplo, quando um arquivo de dados ou de log é adicionado ou removido de um banco de dados, ou quando a instância do SQL Server é interrompida. Para saber mais, veja [Pontos de verificação e a parte ativa do log](../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md).

Os processos de gravação lenta, gravação adiantada e ponto de verificação não esperam a conclusão da operação de E/S. Eles sempre usam a E/S assíncrona (ou sobreposta) e continuam com outro trabalho, verificando o êxito da E/S posteriormente. Isso permite ao SQL Server maximizar os recursos de CPU e de E/S para as tarefas apropriadas.

## <a name="see-also"></a>Consulte Também
[Guia de arquitetura de página e extensões](../relational-databases/pages-and-extents-architecture-guide.md)   
 [Lendo Páginas](../relational-databases/reading-pages.md)
