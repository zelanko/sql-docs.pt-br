---
description: MSSQLSERVER_5180
title: MSSQLSERVER_5180
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5180 (Database Engine error)
ms.assetid: ''
author: rgward
ms.author: ramakoni
ms.openlocfilehash: cbdc30c1e05d50bb20df3f9e3ebf54097c770743
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418659"
---
# <a name="mssqlserver_5180"></a>MSSQLSERVER_5180
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|5180|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|DSK_BAD_FCB_FILEID|
|Texto da mensagem|Não foi possível abrir o FCB (File Control Bank) devido à ID de arquivo inválida %d no banco de dados '%.*ls'. Verifique o local do arquivo. Execute DBCC CHECKDB.|
||

## <a name="explanation"></a>Explicação

Uma consulta ou uma operação pode falhar com um erro 5180 quando uma ID de arquivo inválida é referenciada pelo [!INCLUDE[ssDENoVersion](../../includes/ssdenoversion_md.md)]. Este é um exemplo:

> Mensagem 5180, Nível 22, Estado 1, Linha 1  
Não foi possível abrir o FCB (File Control Bank) devido à ID de arquivo inválida %d no banco de dados '%.*ls'. Verifique o local do arquivo. Execute DBCC CHECKDB.

Como o erro é gerado com a gravidade 22, a sessão do usuário será desconectada. Essa mensagem de erro é gravada no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e no Log de Eventos do Aplicativo do Windows com EventID = 5180.

## <a name="possible-causes"></a>Possíveis causas

O [!INCLUDE[ssDENoVersion](../../includes/ssdenoversion-md.md)] referencia a uma ID de arquivo em muitas situações diferentes, principalmente ao referenciar uma ID de página (pois a ID de arquivo é a primeira parte da ID de página). Se, por algum motivo, a ID de arquivo que está sendo referenciada for < 0 ou não for uma ID de arquivo válida em um banco de dados (de acordo com as IDs de arquivo válidas listadas em exibições do catálogo do sistema, como sys.database_files), um erro 5180 poderá ser recebido.

Uma das possíveis causas é que uma ID de arquivo armazenada não é válida. Como o registro encaminhado em uma linha referencia outra página, quando essa página é acessada e a ID de arquivo é inválida, um erro 5180 pode ser recebido. Essa condição é um erro de banco de dados corrompido na página com o registro encaminhado. (Neste exemplo, `DBCC CHECKDB` relata a Mensagem 8993).

Outro exemplo é uma ID de arquivo inválida como parte de uma ID de página, como armazenado no cabeçalho da página de a ID da página seguinte ou anterior. Esse campo é usado para vincular uma série de páginas, como em um índice clusterizado. Se a ID de arquivo for inválida para a página seguinte ou anterior, quando o mecanismo precisar referenciar isso a fim de ir para essas páginas, um erro 5180 poderá ser recebido. (Neste exemplo, `DBCC CHECKDB` relata a Mensagem 8981).

Se o problema não for uma ID de arquivo inválida devido a uma ID de página armazenada corrompida, o problema poderá estar no [!INCLUDE[ssDENoVersion](../../includes/ssdenoversion-md.md)].

## <a name="user-action"></a>Ação do usuário

Se você receber esse erro, execute `DBCC CHECKDB` no banco de dados, conforme listado na mensagem de erro. Se você receber erros, faça a restauração de um backup válido conhecido. Caso não possa fazer a restauração de um backup, a outra opção será usar a opção de reparo `DBCC CHECKDB`, conforme recomendado pela saída. Na maioria dos casos, um reparo desse tipo de erro resultará em uma perda de dados. Para obter mais informações sobre como usar e as causas de problemas de banco de dados corrompido, confira o artigo: [Como solucionar problemas de consistência de banco de dados relatados por DBCC CHECKDB](https://support.microsoft.com/kb/2015748).

Se `DBCC CHECKDB` não relatar nenhum erro e o problema continuar ocorrendo, entre em contato com o suporte técnico da Microsoft para obter assistência. Esteja preparado para fornecer a consulta que apresenta o erro 5180. Confira a seção [Mais informações](#more-information) para saber como determinar a consulta que apresentou o erro.

## <a name="more-information"></a>Mais informações

O FCB (bloco de controle de arquivo) é uma estrutura de memória interna que acompanha as informações importantes sobre o arquivo associado ao banco de dados. Uma ID de arquivo é usada para identificar exclusivamente um FCB para um banco de dados. Se o mecanismo do servidor tentar referenciar uma ID de arquivo que é inválida, a estrutura do FCB não poderá ser localizada, o que dispara a condição de erro 5180.

Para descobrir qual consulta apresentou esse erro, use as seguintes técnicas:

- Para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 e versões posteriores, veja se a sessão de system_health tem um registro do erro, que deverá incluir o texto da consulta. Confira o recurso para obter mais informações sobre a sessão de system_health: [Suporte ao SQL Server 2008: a sessão de system_health](https://techcommunity.microsoft.com/t5/sql-server-support/supporting-sql-server-2008-the-system-health-session/ba-p/315509).
- Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler e capture o `SQL:BatchStarting`, o `RPC:Starting` e os eventos de exceção. Encontre a consulta que precede o evento de exceção para 5180 da sessão associada ao evento de exceção.
