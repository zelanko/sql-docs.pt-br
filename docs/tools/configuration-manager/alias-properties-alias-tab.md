---
title: Propriedades do alias (guia Alias)
description: Use a guia Alias da caixa de diálogo Propriedades para configurar um alias para que você possa usar um nome alternativo ao se conectar a uma instância do SQL Server.
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 2d1498e2-129c-4ce7-88e5-408e4037243c
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 65558dcdc06b42f3f475fae1b0041909bdff8967
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481707"
---
# <a name="ltaliasgt-properties-alias-tab"></a>Propriedades de &lt;alias&gt; (guia Alias)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

O alias é um nome alternativo que pode ser usado para fazer uma conexão. Ele encapsula os elementos necessários de uma cadeia de conexão, expondo-os com um nome escolhido pelo usuário. Use a página **Alias** na caixa de diálogo de **\<**Alias name**> Propriedades** para exibir ou especificar os elementos da cadeia de conexão de um Alias.

## <a name="options"></a>Opções

**Nome do Alias**

O nome (alias) que você deseja usar para se referir a essa conexão.  

**Nome do Pipe** / **Número da Porta**  

Elementos adicionais da cadeia de conexão. O nome desta caixa varia de acordo com o protocolo selecionado. Consulte os tópicos listados abaixo para obter exemplos.  

**Protocolo**

O protocolo usado para a conexão.

**Servidor**

O nome da instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo conectada.  

## <a name="see-also"></a>Consulte Também

- [Criando uma cadeia de conexão válida usando o protocolo de memória compartilhada](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)
- [Criando uma cadeia de conexão válida usando TCP/IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)
- [Criando uma cadeia de conexão válida usando pipes nomeados](/previous-versions/sql/sql-server-2016/ms189307(v=sql.130))