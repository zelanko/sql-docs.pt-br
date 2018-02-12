---
title: Tela do Assistente de 3 (Driver ODBC para SQL Server) da fonte de dados | Microsoft Docs
ms.custom: 
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a0a97971dcd8a16a2ac15b1013dbbe96a43f21c0
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2018
---
# <a name="data-source-wizard-screen-3"></a>Tela de Assistente de fonte de dados 3

Especifique o banco de dados padrão, várias opções ANSI a serem usadas pelo driver e o nome de um servidor espelho.

## <a name="options"></a>Opções

### <a name="change-the-default-database-to"></a>Alterar o banco de dados padrão

Especifica o nome do banco de dados padrão de qualquer conexão feita com o uso desta fonte de dados. Quando essa caixa é desmarcada, as conexões usam o banco de dados padrão definido para a ID de logon no servidor. Quando essa caixa está marcada, o banco de dados nomeado na caixa substitui o padrão definido para a ID de logon. Se o **anexar o nome de arquivo de banco de dados** caixa tem o nome de um arquivo primário, o banco de dados descrito pelo arquivo primário é anexado como um banco de dados usando o nome do banco de dados especificado no **alterar o banco de dados padrão para**caixa.

Usar o banco de dados padrão para a ID de logon é mais eficiente do que especificar um banco de dados padrão na fonte de dados ODBC.

### <a name="mirror-server"></a>Servidor espelho

Especifica o nome do parceiro de failover do banco de dados a ser espelhado. Se um nome de banco de dados não é mostrado no **alterar o banco de dados padrão** caixa ou o nome exibido é o banco de dados padrão, **servidor espelho** está esmaecido.

Se desejar, você pode especificar um nome da entidade do servidor (SPN) para o servidor espelho. O SPN do servidor espelho é usado para autenticação mútua entre cliente e servidor.

### <a name="attach-database-filename"></a>Anexar o nome de arquivo de banco de dados

Especifica o nome do arquivo primário de um banco de dados anexável. Esse banco de dados é anexado e usado como o banco de dados padrão da fonte de dados. Especifique o caminho completo e o nome de arquivo do arquivo primário. O nome do banco de dados especificado no **alterar o banco de dados padrão** caixa é usada como o nome do banco de dados anexado.

### <a name="use-ansi-quoted-identifiers"></a>Usar identificadores ANSI entre aspas

Especifica que QUOTED_IDENTIFIERS será ativado quando o driver ODBC do SQL Server se conecta. Quando essa caixa de seleção é selecionada, o SQL Server impõe regras de ANSI em relação a aspas. Aspas duplas só podem ser usadas para identificadores, como nomes de coluna e tabela. Cadeias de caracteres devem ser colocadas entre aspas simples:

```
SELECT "LastName"
FROM "Person.Contact"
WHERE "LastName" = 'O''Brien'
```

Quando essa caixa de seleção não está marcada, os aplicativos que usam identificadores entre aspas, como o utilitário Microsoft Query fornecido com o Microsoft Excel, encontram erros quando geram instruções SQL com identificadores entre aspas.

### <a name="use-ansi-nulls-paddings-and-warnings"></a>Usar nulos, preenchimentos e avisos ANSI

Especifica as opções ANSI_NULLS, ANSI_WARNINGS e ANSI_PADDINGS serão ativadas quando o Driver ODBC para SQL Server se conecta.

Com ANSI_NULLS definida, o servidor impõe regras ANSI referentes à comparação de colunas para NULL. A sintaxe ANSI "IS NULL" ou "IS NOT NULL" deve ser usada para todas as comparações NULL. Não há suporte para a sintaxe Transact-SQL "= NULL".

Com ANSI_WARNINGS ativada, o SQL Server emite mensagens de aviso para condições que violam regras ANSI, mas não violam as regras do Transact-SQL. Exemplos desses erros são dados truncados na execução de uma instrução INSERT ou UPDATE ou um valor nulo encontrado durante uma função de agregação. 

Com ANSI_PADDING definida, à direita de espaços em branco em **varchar** valores e zeros à direita em **varbinary** valores não são excluídos automaticamente.

### <a name="application-intent"></a>Intenção do aplicativo

Declara o tipo de carga de trabalho de aplicativo ao conectar-se a um servidor. Os valores possíveis são **ReadOnly** e **ReadWrite**.

### <a name="multi-subnet-failover"></a>Failover de várias sub-redes.

Se seu aplicativo estiver se conectando ao grupo de disponibilidade de (grupos de disponibilidade AlwaysOn) de recuperação de desastres alta disponibilidade (AG) em sub-redes diferentes, habilitando **failover de várias sub-redes.** configura o Driver ODBC para SQL Server fornecer detecção mais rápida e conexão ao servidor ativo (atualmente).

### <a name="transparent-network-ip-resolution"></a>Resolução IP de rede transparente.

Altera o comportamento da **failover de várias sub-redes** para permitir a reconexão mais rápida durante o failover. Consulte [usando resolução de IP de rede transparente](../../../connect/odbc/using-transparent-network-ip-resolution.md) para obter mais informações.

### <a name="column-encryption"></a>Criptografia de coluna.

Permite que a descriptografia automática e a criptografia de transferências de dados para e de colunas criptografadas com a [sempre criptografado](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) recurso disponível no SQL Server 2016 e posterior.

### <a name="use-fmtonly-metadata-discovery"></a>Use a descoberta de metadados FMTONLY:

Use o método de descoberta de metadados de SET FMTONLY herdado ao conectar-se ao SQL Server 2012 ou mais recente. Habilitar essa opção apenas ao usar consultas não oferece suporte para [sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md), como aqueles que contêm tabelas temporárias. 

### <a name="next"></a>Próximo

Vai para a próxima tela do assistente.

### <a name="back"></a>Voltar

Retorna para a tela anterior do assistente.

## <a name="next-steps"></a>Próximas etapas

[Tela 2 do Assistente de fonte de dados](../../../connect/odbc/windows/dsn-wizard-2.md)

[Tela de Assistente de fonte de dados 4](../../../connect/odbc/windows/dsn-wizard-4.md)
