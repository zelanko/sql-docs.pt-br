---
title: Notas sobre mssql-tools em Linux e macOS
description: Saiba quais são as novidades e mudanças em versões lançadas das Ferramentas do Microsoft SQL Server.
ms.custom: ''
ms.date: 07/13/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: v-zhangw
ms.author: v-zhangw
manager: kenvh
ms.openlocfilehash: 85f7115dbf138055df83a7bb07e5a78f505b5794
ms.sourcegitcommit: 6f49804b863fed44968ea5829e2c26edc5988468
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/05/2020
ms.locfileid: "87812348"
---
# <a name="release-notes-for-the-microsoft-sql-server-tools-on-linux-and-macos"></a>Notas sobre a versão das Ferramentas do Microsoft SQL Server em Linux e macOS

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este artigo lista e descreve o que há de novo nas versões com controle de versão das Ferramentas do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] SQL Server em Linux e macOS.

## <a name="17611-july-2020"></a>17.6.1.1, julho de 2020

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Analisador de linha de comando sqlcmd atualizado | Correção de bugs nos quais ocorreu um comportamento inesperado ao usar determinadas opções em diferentes ordens. |
| Mensagens de erro do sqlcmd atualizadas | Correção de várias inconsistências no modo como os erros no sqlcmd eram retornados. |
| Corrigida a opção -Y do sqlcmd | Corrigido um problema em que a opção -Y era ineficaz |
| Corrigido o truncamento de nome de coluna do sqlcmd | Corrigido o problema em que os nomes das colunas eram truncados incorretamente |
| Códigos de saída do sqlcmd no Linux | Corrigido o problema em que o código de saída do processo estava ausente no Linux |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre como se conectar com o [BCP](connecting-with-bcp.md) e o [SQLCMD](connecting-with-sqlcmd.md)!
