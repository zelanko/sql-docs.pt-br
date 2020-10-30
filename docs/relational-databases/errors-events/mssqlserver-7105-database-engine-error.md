---
description: MSSQLSERVER_7105
title: MSSQLSERVER_7105
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7105 (Database Engine error)
ms.assetid: ''
author: rgward
ms.author: ramakoni
ms.openlocfilehash: bfcd8763c649f83bb9e72881c6facda29917f7b8
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418675"
---
# <a name="mssqlserver_7105"></a>MSSQLSERVER_7105
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|7105|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|TXT_PGNOTEXIST|
|Texto da mensagem|A ID de banco de dados %d, página %S_PGID, slot %d para o nó do tipo de dados LOB não existe. Em geral, isso é causado por transações que podem ler dados não confirmados em uma página de dados. Execute DBCC CHECKTABLE|
||

## <a name="explanation"></a>Explicação

Uma consulta poderá receber a Mensagem 7105 quando não for possível acessar dados LOB (Objeto Grande) referenciados por uma linha de página do banco de dados.

Como esse erro é de nível de gravidade 22, a conexão é encerrada pelo servidor. Essa mensagem de erro também é gravada no arquivo SQL ERRORLOG e no Log de Eventos do Aplicativo do Windows com a EventID = 7105.

## <a name="possible-causes"></a>Possíveis causas

Esse erro pode ocorrer devido a um dos seguintes motivos:

- Há um problema de banco de dados corrompido em uma página de banco de dados ou dentro das estruturas da página LOB referenciada pela página de banco de dados.
- A consulta que apresenta a falha está usando a dica de consulta `READ UNCOMMITTED ISOLATION LEVEL` ou `NOLOCK`.
- Há um problema dentro do Mecanismo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que causa uma falha na consulta com esse erro.

Confira as seções Resolução e [Mais informações](#more-information) para determinar a causa do seu problema específico e a solução apropriada.

## <a name="user-action"></a>Ação do usuário

1. Como a mensagem indica, a primeira etapa a ser realizada é executar `DBCC CHECKDB` no banco de dados ou `DBCC CHECKTABLE` na tabela em que o problema foi encontrado.

    - A ID do banco de dados é fornecida na mensagem.
    - Para descobrir a tabela afetada exata sem executar `DBCC CHECKDB`, você precisará descobrir quais tabelas foram acessadas pela consulta que apresentou o erro. Um desses métodos é usar o SQL Profiler para rastrear a consulta. No entanto, no [!INCLUDE[sskatmai](../../includes/sskatmai-md.md)] e no [!INCLUDE[sskatmai](../../includes/sskatmai-md.md)] R2, você poderá encontrar a consulta usando a sessão de system_health dos Eventos Estendidos. Confira este link para obter mais informações sobre como usar a sessão de system_health: [Usar a sessão de system_health](/sql/relational-databases/extended-events/use-the-system-health-session).

    - Assim como ocorre com qualquer problema de consistência de banco de dados, você pode resolver esses erros fazendo a restauração de um backup válido conhecido que não contenha esse problema.

    - No entanto, se você não conseguir fazer a restauração por meio de um backup, siga as recomendações referentes a `DBCC CHECKDB` ou `DBCC CHECKTABLE` para reparar esses erros. É possível que isso resulte na perda de dados. Para obter mais informações sobre como usar CHECKDB e as causas dos problemas de banco de dados corrompido, confira o artigo: [Como solucionar problemas de consistência de banco de dados relatados por DBCC CHECKDB](https://support.microsoft.com/kb/2015748).
  
1. É possível que esse erro seja recebido porque a consulta que acessa a tabela usava um nível de isolamento igual a `READ UNCOMMITTED` ou a dica de consulta `NOLOCK` (também conhecida como leitura suja).

   - Se `DBCC CHECKDB` ou `DBCC CHECKTABLE` não mostrar nenhum erro associado a essa tabela e aos dados LOB, a causa mais provável será o uso de uma leitura não suja. Se esse for o caso para seu aplicativo, você precisará evitar o uso de uma leitura suja ou repetir a consulta.
  
   - Se você achar que essa é a causa do erro, não haverá nenhum problema real de consistência de banco de dados.

## <a name="more-information"></a>Mais informações

Se o banco de dados corrompido for a causa desse problema, `DBCC CHECKDB` e/ou `DBCC CHECKTABLE` deverá relatar erros. No entanto, esses comandos não relatarão a Mensagem 7105. Os erros que você receber de CHECKDB dependerão do que está danificado na referência às estruturas de LOB ou nas próprias estruturas LOB.

- Se a linha da página de banco de dados não referenciar corretamente uma página LOB válida, você poderá ver erros como estes:

    > Mensagem 8929, Nível 16, Estado 1, Linha 1  
    ID de objeto 2137058649, ID de índice 0, ID de partição 72057594038910976, ID de unidade de alocação 72057594039828480 (tipo de dados em linha): Erros encontrados em dados fora da linha com a ID 131203072 de propriedade do registro de dados identificado por RID = (1:179:1)  
    Mensagem 8964, Nível 16, Estado 1, Linha 1  
    Erro de tabela: ID de objeto 2137058649, ID de índice 0, ID de partição 72057594038910976, ID de unidade de alocação 72057594039894016 (tipo de dados LOB). O nó de dados fora da linha na página (1:177), slot 1, ID de texto 131203072 não está referenciado.  
    Mensagem 8965, Nível 16, Estado 1, Linha 1  
    Erro de tabela: ID de objeto 2137058649, ID de índice 0, ID de partição 72057594038910976, ID de unidade de alocação 72057594039894016 (tipo de dados LOB). O nó de dados fora da linha na página (255:177), slot 1, ID de texto 131203072 é referenciado pela página (1:179), slot 1, mas não foi visto na verificação  

- Diferentes cenários para o problema podem resultar em uma combinação diferente de erros. Neste exemplo:  

    > A página de banco de dados 1:179, slot 1, está referenciando uma página LOB que não é uma página válida no banco de dados (página 255:177). A página (1:177) é uma página LOB válida, mas nunca foi referenciada por nenhuma página de banco de dados. Portanto, nessa situação, o problema é que a linha no slot 1 da página 1:179 referencia a página 255:177 em vez da 1:177.

- O segredo para determinar se os erros de `DBCC CHECKDB` estão relacionados a problemas da página LOB é procurar as frases 'dados fora da linha' e 'tipo de dados LOB'.

    > A Mensagem 8929 é um erro relacionado à página de banco de dados que referencia as páginas LOB.  
A Mensagem 8964 é um erro que indica que uma página LOB não foi referenciada por nenhuma página de banco de dados.  
A Mensagem 8965 é um erro que indica que as páginas LOB foram referenciadas por uma página de banco de dados, mas não existem como uma página válida

    Em muitas situações envolvendo esses tipos de erros, o reparo resultará na exclusão das linhas que apontam para os dados LOB e os próprios dados LOB. O algoritmo de reparo tentará apenas remover os fragmentos LOB que afetam as linhas do banco de dados em questão, mas isso não pode ser garantido em todas as situações, dependendo do que está danificado na 'estrutura de árvore' LOB.

- No exemplo mostrado aqui, as mensagens retornadas por um CHECKTABLE usando `REPAIR_ALLOW_DATA_LOSS` são semelhantes a:

    > Reparar: Registro excluído para a ID de objeto 2137058649, ID de índice 0, ID de partição 72057594038910976, ID de unidade de alocação 72057594039828480 (tipo de dados em linha), na página (1:179), slot 1. Os índices serão recriados.  
    Reparar: Coluna de dados fora da linha excluída com ID 131203072, para ID de objeto 2137058649, ID de índice 0, ID de partição 72057594038910976, ID de unidade de alocação 72057594039894016 (tipo de dados LOB) na página (1:177), slot 1.  
    Mensagem 8929, Nível 16, Estado 1, Linha 1  
    ID de objeto 2137058649, ID de índice 0, ID de partição 72057594038910976, ID de unidade de alocação 72057594039828480 (tipo de dados em linha): Erros encontrados em dados fora da linha com a ID 131203072 de propriedade do registro de dados identificado por RID = (1:179:1)  
            O erro foi corrigido.  
    Mensagem 8964, Nível 16, Estado 1, Linha 1  
    Erro de tabela: ID de objeto 2137058649, ID de índice 0, ID de partição 72057594038910976, ID de unidade de alocação 72057594039894016 (tipo de dados LOB). O nó de dados fora da linha na página (1:177), slot 1, ID de texto 131203072 não está referenciado.  
            O erro foi corrigido.  
    Mensagem 8965, Nível 16, Estado 1, Linha 1  
    Erro de tabela: ID de objeto 2137058649, ID de índice 0, ID de partição 72057594038910976, ID de unidade de alocação 72057594039894016 (tipo de dados LOB). O nó de dados fora da linha na página (255:177), slot 1, ID de texto 131203072 é referenciado pela página (1:179), slot 1, mas não foi visto na verificação.  
            Não foi possível reparar este erro

    A última mensagem que indica `Could not repair this error` é equivocada. O erro foi reparado porque a linha da página de banco de dados que apontava para a página inválida (255:177) foi excluída.
