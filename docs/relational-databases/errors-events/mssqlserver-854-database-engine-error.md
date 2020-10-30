---
description: MSSQLSERVER_854
title: MSSQLSERVER_854
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 854 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: f0bf9061b452329280f0625bcc1339469372f4df
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418671"
---
# <a name="mssqlserver_854"></a>MSSQLSERVER_854
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|854|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|HARDWARE_MEMORY_SCRUBBER|
|Texto da mensagem|O computador dá suporte à recuperação de erros de memória. A proteção de memória do SQL está habilitada para a recuperação de corrupção de memória|
||

## <a name="explanation"></a>Explicação

Essa mensagem indica que o hardware no sistema operacional dá suporte à capacidade de recuperação de erros de memória. Em computadores com um hardware mais recente e que executem o Windows Server 2012 ou uma versão posterior, o hardware pode notificar o sistema operacional e os aplicativos de que as páginas de memória (páginas do sistema operacional) estão marcadas como inválidas ou danificadas. Aplicativos como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem registrar essas notificações de páginas de memória inválidas usando o seguinte conjunto de APIs:

- `GetMemoryErrorHandlingCapabilities`
- `RegisterBadMemoryNotification`
- `BadMemoryCallbackRoutine`

O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] adiciona suporte para essas notificações no Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e versões posteriores. Durante a inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verifica se o hardware dá suporte a esse novo recurso. Além disso, você receberá a seguinte mensagem no log de erros:

> \<Datetime> O Computador do Servidor dá suporte à recuperação de erros de memória. A proteção de memória do SQL está habilitada para a recuperação de corrupção de memória.

## <a name="user-action"></a>Ação do usuário

Verifique se você está recebendo outros erros, como 855 e 856, e execute a ação corretiva apropriada.

## <a name="more-information"></a>Mais informações

Use o sinalizador de rastreamento 849 do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para impedir que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se registre no sistema operacional para receber notificações de erros de memória. No entanto, lembre-se de que a habilitação o sinalizador de rastreamento 849 impedirá o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de receber notificações de memória inválida do sistema operacional. Portanto, não recomendamos que você use esse sinalizador de rastreamento em circunstâncias típicas.
