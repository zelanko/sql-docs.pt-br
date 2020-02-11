---
title: Emular variáveis do pacote do Oracle
description: Descreve como o Assistente de Migração do SQL Server (SSMA) para Oracle emula variáveis de pacote Oracle no SQL Server.
authors: nahk-ivanov
ms.service: ssma
ms.devlang: sql
ms.topic: article
ms.date: 1/22/2020
ms.author: alexiva
ms.openlocfilehash: 9a8ca5c7dfdda98e1c005c3851d061957cf67449
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "76762820"
---
# <a name="emulating-oracle-package-variables"></a>Emular variáveis do pacote do Oracle

O Oracle dá suporte ao encapsulamento de variáveis, tipos, procedimentos armazenados e funções em um pacote. Ao converter pacotes do Oracle, você precisa converter:

* Procedimentos e funções – públicos e privados
* variáveis
* Cursores
* Rotinas de inicialização

Este artigo descreve como Assistente de Migração do SQL Server (SSMA) para Oracle converte variáveis de pacote em SQL Server.

## <a name="conversion-basics"></a>Noções básicas de conversão

Para armazenar variáveis de pacote, o SSMA para Oracle usa procedimentos armazenados que residem em `ssma_oracle` um esquema especial `ssma_oracle.db_storage` juntamente com a tabela. Esta tabela é filtrada `SPID` pelo (identificador de sessão) e pelo tempo de logon. Essa filtragem permite que você Diferencie entre variáveis de diferentes sessões.

No início de cada procedimento de pacote convertido, o SSMA coloca uma chamada `ssma_oracle.db_check_init_package` para o procedimento especial, que verifica se o pacote foi inicializado e o inicializa, se necessário. Cada procedimento de inicialização limpa a tabela de armazenamento e define valores padrão para cada variável de pacote.

## <a name="example"></a>Exemplo

Considere o exemplo a seguir para converter várias variáveis de pacote:

```sql
CREATE OR REPLACE PACKAGE MY_PACKAGE
IS
    space varchar(1) := ' ';
    unitname varchar(128) := 'My Simple Package';
    ts date := sysdate;
END;
```

O SSMA converte-o no seguinte código Transact-SQL:

```sql
CREATE PROCEDURE dbo.MY_PACKAGE$SSMA_Initialize_Package
AS
BEGIN
    EXECUTE ssma_oracle.db_clean_storage

    EXECUTE ssma_oracle.set_pv_varchar
        DB_NAME(),
        'DBO',
        'MY_PACKAGE',
        'SPACE',
        ' '

    EXECUTE ssma_oracle.set_pv_varchar
        DB_NAME(),
        'DBO',
        'MY_PACKAGE',
        'UNITNAME',
        'My Simple Package'

    DECLARE
        @temp datetime2

    SET @temp = sysdatetime()

    EXECUTE sysdb.ssma_oracle.set_pv_datetime2
      DB_NAME(),
      'DBO',
      'MY_PACKAGE',
      'TS',
      @temp
END
```

## <a name="emulating-get-and-set-methods-for-package-variables"></a>Emulando métodos get e Set para variáveis de pacote

O Oracle `Get` usa `Set` e métodos para as variáveis de pacote, para evitar permitir que outros subprogramas os leiam e gravem diretamente. Se houver um requisito para manter algumas variáveis disponíveis entre as chamadas do subprograma na mesma sessão, essas variáveis serão tratadas como variáveis globais.

Para superar essa regra de escopo, o SSMA para Oracle usa procedimentos `ssma_oracle.set_pv_varchar` armazenados como para cada tipo de variável. Para acessar essas variáveis, o SSMA usa um conjunto de `get_*` `set_*` procedimentos e funções independentes de transação.

| Tipo de dados no Oracle | Procedimento `Set` do SSMA           |
| ------------------- | ------------------------------ |
| VARCHAR             | `ssma_oracle.set_pv_varchar`   |
| DATE                | `ssma_oracle.set_pv_datetime2` |
| CHAR                | `ssma_oracle.set_pv_varchar`   |
| INT                 | `ssma_oracle.set_pv_float`     |
| FLOAT               | `ssma_oracle.set_pv_float`     |

Para distinguir entre variáveis de diferentes sessões, o SSMA armazena as variáveis junto com `SPID` seu (identificador de sessão) e o tempo de logon da sessão. Assim, `get_*` os `set_*` procedimentos e mantêm as variáveis independentes das sessões que as executam.
