---
title: Tela 3 do Assistente de Fonte de Dados (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1775d89587522e1ad1036d2f0c514c9439b9403b
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80927916"
---
# <a name="data-source-wizard-screen-3"></a>Tela 3 do Assistente de Fonte de Dados

Especifique o banco de dados padrão, várias opções ANSI a serem usadas pelo driver e o nome de um servidor espelho.

## <a name="options"></a>Opções

### <a name="change-the-default-database-to"></a>Alterar o banco de dados padrão para

Especifica o nome do banco de dados padrão de qualquer conexão feita com o uso desta fonte de dados. Quando essa caixa é desmarcada, as conexões usam o banco de dados padrão definido para a ID de logon no servidor. Quando essa caixa está marcada, o banco de dados nomeado na caixa substitui o padrão definido para a ID de logon. Se a caixa **Anexar nome de arquivo de banco de dados** tiver o nome de um arquivo primário, o banco de dados descrito pelo arquivo primário será anexado como um banco de dados usando-se o nome do banco de dados especificado na caixa **Alterar o banco de dados padrão para**.

Usar o banco de dados padrão para a ID de logon é mais eficiente do que especificar um banco de dados padrão na fonte de dados ODBC.

### <a name="mirror-server"></a>Servidor espelho

Especifica o nome do parceiro de failover do banco de dados a ser espelhado. Se um nome de banco de dados não for exibido na caixa **Alterar o banco de dados padrão para** ou o nome exibido for o banco de dados padrão, a caixa **Servidor Espelho** ficará indisponível.

Se desejar, você pode especificar um nome da entidade do servidor (SPN) para o servidor espelho. O SPN do servidor espelho é usado para autenticação mútua entre cliente e servidor.

### <a name="attach-database-filename"></a>Anexar o nome de arquivo do banco de dados

Especifica o nome do arquivo primário de um banco de dados anexável. Esse banco de dados é anexado e usado como o banco de dados padrão da fonte de dados. Especifique o caminho completo e o nome de arquivo do arquivo primário. O nome do banco de dados especificado na caixa **Alterar o banco de dados padrão para** é usado como o nome do banco de dados anexado.

### <a name="use-ansi-quoted-identifiers"></a>Usar identificadores ANSI entre aspas

Especifica que QUOTED_IDENTIFIERS seja definido como ativado quando o driver ODBC para SQL Server se conectar. Quando essa caixa de seleção está marcada, o SQL Server impõe regras ANSI em relação a aspas. Aspas duplas só podem ser usadas para identificadores, como nomes de coluna e tabela. Cadeias de caracteres devem ser colocadas entre aspas simples:

```
SELECT "LastName"
FROM "Person.Contact"
WHERE "LastName" = 'O''Brien'
```

Quando essa caixa de seleção não está marcada, os aplicativos que usam identificadores entre aspas, como o utilitário Microsoft Query fornecido com o Microsoft Excel, encontram erros quando geram instruções SQL com identificadores entre aspas.

### <a name="use-ansi-nulls-paddings-and-warnings"></a>Usar nulos, preenchimentos e avisos ANSI

Especifica que as opções ANSI_NULLS, ANSI_WARNINGS e ANSI_PADDINGS sejam definidas como ativadas quando o driver ODBC para SQL Server se conectar.

Com ANSI_NULLS definida, o servidor impõe regras ANSI referentes à comparação de colunas para NULL. A sintaxe ANSI "IS NULL" ou "IS NOT NULL" deve ser usada para todas as comparações NULL. Não há suporte para a sintaxe Transact-SQL "= NULL".

Com a opção ANSI_WARNINGS definida, o SQL Server emite mensagens de aviso para condições que violam regras ANSI, mas não violam as regras de Transact-SQL. Exemplos desses erros são dados truncados na execução de uma instrução INSERT ou UPDATE ou um valor nulo encontrado durante uma função de agregação. 

Com a opção ANSI_PADDING definida, espaços em branco à direita em valores **varchar** e zeros à direita em valores **varbinary** não são cortados automaticamente.

### <a name="application-intent"></a>Intenção do aplicativo

Declara o tipo de carga de trabalho de aplicativo ao conectar-se a um servidor. Os valores possíveis são **ReadOnly** e **ReadWrite**.

### <a name="multi-subnet-failover"></a>Failover de várias sub-redes.

Se o aplicativo estiver se conectando a um AG (grupo de disponibilidade) de recuperação de desastre de alta disponibilidade (Grupos de Disponibilidade AlwaysOn) em sub-redes diferentes, habilite **Failover de várias sub-redes.** configura o Driver ODBC para SQL Server para fornecer mais rapidez na detecção do servidor ativo (atualmente) e na conexão a ele.

### <a name="transparent-network-ip-resolution"></a>Resolução IP de Rede Transparente.

Altera o comportamento de **Failover de várias sub-redes** para permitir uma reconexão mais rápida durante o failover. Veja [Usando resolução de IP de rede transparente](../../../connect/odbc/using-transparent-network-ip-resolution.md) para obter mais informações.

### <a name="column-encryption"></a>Criptografia de Coluna.

Habilita a descriptografia automática e a criptografia de transferências de dados para e de colunas criptografadas com o recurso [Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) disponível no SQL Server 2016 e posterior.

### <a name="use-fmtonly-metadata-discovery"></a>Use a descoberta de metadados FMTONLY:

Use o método de descoberta de metadados SET FMTONLY herdado ao se conectar ao SQL Server 2012 ou mais recente. Habilite isso somente ao usar consultas não compatíveis com [sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md), como as que contêm tabelas temporárias. 

### <a name="next"></a>Próximo

Prossegue para a próxima tela do assistente.

### <a name="back"></a>Voltar

Retorna para a tela anterior do assistente.

## <a name="next-steps"></a>Próximas etapas

[Tela 2 do Assistente de Fonte de Dados](../../../connect/odbc/windows/dsn-wizard-2.md)

[Tela 4 do Assistente de Fonte de Dados](../../../connect/odbc/windows/dsn-wizard-4.md)
