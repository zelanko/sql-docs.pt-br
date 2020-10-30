---
description: MSSQLSERVER_855
title: MSSQLSERVER_855
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 855 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: c65a48247359437c6680141b60c5e54463b03991
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418670"
---
# <a name="mssqlserver_855"></a>MSSQLSERVER_855
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|855|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|BAD_MEMORY_OUTSIDE_BPOOL|
|Texto da mensagem|Foi detectada uma corrupção de memória de hardware incorrigível. O sistema pode se tornar instável. Verifique o log de eventos do Windows para obter mais detalhes|
||

## <a name="explanation"></a>Explicação

Essa mensagem indica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detectou uma página de memória inválida em um objeto armazenado em cache fora do pool de buffers. Ela é gerada em sistemas que dão suporte à capacidade de recuperação de erros de memória. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não consegue se recuperar desses cenários e registra essa mensagem em log.

## <a name="user-action"></a>Ação do usuário

Você deve executar verificações de hardware ou do sistema para determinar se há problemas de memória ou de CPU. Verifique se todas as atualizações do sistema operacional e de hardware, bem como todos os drivers do sistema, foram aplicados ao sistema. Considere a possibilidade de executar diagnósticos de fabricação de hardware, incluindo testes relacionados à memória. Sempre que você receber esse erro, considere a possibilidade de executar o `DBCC CHECKDB` em todos os bancos de dados dessa instância.

## <a name="more-information"></a>Mais informações

Em computadores com um hardware mais recente e que executem o Windows Server 2012 ou uma versão posterior, o hardware pode notificar o sistema operacional e os aplicativos de que as páginas de memória (páginas do sistema operacional) estão marcadas como inválidas ou danificadas. Aplicativos como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem registrar essas notificações de páginas de memória inválidas usando o seguinte conjunto de APIs:

- `GetMemoryErrorHandlingCapabilities`
- `RegisterBadMemoryNotification`
- `BadMemoryCallbackRoutine`

O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] adiciona suporte para essas notificações no Microsoft [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versões posteriores. Durante a inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verifica se o hardware dá suporte a esse novo recurso. Além disso, você receberá a seguinte mensagem no log de erros:

> \<Datetime> O Computador do Servidor dá suporte à recuperação de erros de memória. A proteção de memória do SQL está habilitada para a recuperação de corrupção de memória.

Atualmente, somente o pool de buffers executa uma ação quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recebe essas notificações. Quando ele recebe uma notificação, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisa iterar em todo o pool de buffers e descobrir o endereço de cada buffer alocado. Em seguida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa a API `QueryWorkingSetEX` para verificar se as páginas de memória que dão suporte à página de dados estão marcadas como inválidas. A estrutura de saída `PSAPI_WORKING_SET_EX_BLOCK` que corresponde a essa página de memória terá o membro inválido definido como 1 se houver algum dano relatado.

Se essa página de dados ou esse pool de buffers não estiver alterado no momento ou não estiver processando a E/S, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá descartar e cancelar a confirmação da página de dados. Em seguida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registrará em log a seguinte mensagem:

> O SQL Server detectou uma corrupção de memória de hardware no banco de dados '%ls', ID de arquivo: %u, ID de página: %u, endereço de memória: 0x%I64x e recuperou a página com êxito.

Quando as consultas exigirem essa página de dados novamente, o pool de buffers poderá ler a página de dados do disco e levar o conteúdo mais uma vez para o pool de buffers. Também é possível que a versão em disco da página esteja em um estado danificado. Nesse caso, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá registrar em log erros adicionais, como o erro 824.

Se a página inválida for usada não pelo pool de buffers, mas por outra estrutura ou outro objeto armazenado em cache, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registrará em log a seguinte mensagem:

> Foi detectada uma corrupção de memória de hardware incorrigível. O sistema pode se tornar instável. Verifique o log de eventos do Windows para obter mais detalhes.

Se o servidor estiver relatando erros de memória, você deverá entrar em contato com o fornecedor do hardware do computador e executar as ações apropriadas, como executar o diagnóstico de memória, atualizar o BIOS e o firmware e substituir os módulos de memória inválidos.

Use o sinalizador de rastreamento 849 do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para impedir que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se registre no sistema operacional para receber notificações de erros de memória. No entanto, lembre-se de que a habilitação o sinalizador de rastreamento 849 impedirá o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de receber notificações de memória inválida do sistema operacional. Portanto, não recomendamos que você use esse sinalizador de rastreamento em circunstâncias típicas.

Além disso, lembre-se de que, por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] receberá essas notificações em um hardware compatível.

Esteja ciente também de que, quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se registra para receber essas notificações de erros de memória, o processo do sistema de gravador lento não executa verificações de páginas constantes. Para obter mais informações sobre verificações de páginas constantes, confira [Como solucionar a Mensagem 832 (página constante alterada) no SQL Server](https://support.microsoft.com/help/2015759).
