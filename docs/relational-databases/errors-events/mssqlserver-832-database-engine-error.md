---
description: MSSQLSERVER_832
title: MSSQLSERVER_832
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 832 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 846ce27ff8e7d9560a6d4cc691d1523fddd913fa
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418660"
---
# <a name="mssqlserver_832"></a>MSSQLSERVER_832
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|832|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|B_CONSTPAGECHANGED|
|Texto da mensagem|Uma página que deveria ser constante foi alterada (soma de verificação esperada: \<expected value>, soma de verificação real: \<actual value>, banco de dados \<dbid>, arquivo \'<filename>', página \<pageno>). Geralmente, isso indica falha na memória ou outro dano no hardware ou no sistema operacional.|
||

## <a name="explanation"></a>Explicação

Um fator externo fez com que uma página de banco de dados fosse modificada fora do código normal do mecanismo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado para alteração das páginas de banco de dados.  As condições podem ser:  

- Um thread em execução no processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que faz gravações incorretas em uma página de banco de dados. Isso costuma ser chamado de "scribbler"
- Um problema de hardware ou sistema operacional em que a memória que fez backup da página de banco de dados está incorreta, foi modificada ou danificada  

Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detecta esse comportamento, o erro 832 é gerado.

## <a name="user-action"></a>Ação do usuário

Para encontrar a causa do erro, considere o uso destas opções:

- Você deve executar as verificações normais de hardware ou do sistema para determinar se há um problema de memória, CPU ou outro relacionado ao hardware. Verifique se todas as atualizações do sistema operacional e de hardware, bem como todos os drivers do sistema, foram aplicados ao sistema. Considere a possibilidade de executar diagnósticos de fabricação de hardware, incluindo testes relacionados à memória.
- Avalie quais DLLs "externas" podem ter sido carregadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que talvez causem esse problema, incluindo procedimentos armazenados estendidos, objetos COM ou outras DLLs, que podem estar modificando incorretamente a memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reservada para páginas de banco de dados.  

Sempre que você receber esse erro, considere imediatamente a possibilidade de executar `DBCC CHECKDB` no banco de dados referenciado pelo \<dbid> na mensagem de erro.

## <a name="more-information"></a>Mais informações

Esse erro é detectado pela tarefa em segundo plano, geralmente chamada de LazyWriter. (O "comando" para essa tarefa é visto como LAZY WRITER). Portanto, esse erro não é retornado para um aplicativo cliente. O erro será gravado no Log de Eventos do Aplicativo do Windows como EventID = 832.  

Somente as páginas que não estão atualmente modificadas no cache (ou "sujas") são verificadas. É por isso que a mensagem usa o termo "constante": porque a página nunca foi alterada desde que foi lida do disco. Além disso, a página foi lida como "limpa" do disco porque tem um valor de soma de verificação e não teve uma falha de soma de verificação (Mensagem 824). No entanto, a página podia ser modificada em algum ponto após esse erro e, em seguida, gravada em disco com a modificação incorreta. Se esse erro ocorrer, uma nova soma de verificação será calculada com base em todas as modificações antes de ela ser gravada em disco. Portanto, a página pode estar danificada em disco, mas uma leitura seguinte do disco pode não disparar uma falha de soma de verificação. É importante executar `DBCC CHECKDB` em qualquer banco de dados referenciado por esse erro.  

É possível que, até mesmo, `DBCC CHECKDB` não relate um erro para uma página nesse estado depois de ela ser gravada em disco. Isso ocorre porque a modificação incorreta pode estar em locais da página que não contêm dados nem nenhuma informação importante de estrutura de página ou linha, ou elas podem ser modificações em dados que não podem ser detectados por CHECKDB.  

Leia também mais detalhes e informações sobre a Mensagem 832 no white paper [Fundamentos de E/S do SQL Server, Capítulo 2](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10)).
