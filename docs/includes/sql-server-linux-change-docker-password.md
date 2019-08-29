---
ms.openlocfilehash: 4803a99e0fb1435b545ec775b2a8abe063d9fd8d
ms.sourcegitcommit: cbbb210c0315f9e2be2b9cd68db888ac53429814
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69890914"
---
A conta **SA** é um administrador do sistema na instância do SQL Server que é criada durante a instalação. Depois de criar o contêiner do SQL Server, a variável de ambiente `MSSQL_SA_PASSWORD` especificada é detectável executando `echo $MSSQL_SA_PASSWORD` no contêiner. Para fins de segurança, altere sua senha SA:

1. Escolha uma senha forte para usar no usuário de SA.

1. Use `docker exec` para executar o utilitário **sqlcmd** para alterar a senha por meio de uma instrução Transact-SQL. Substituir `<YourStrong!Passw0rd>` e `<YourNewStrong!Passw0rd>` com seus próprios valores de senha:

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourStrong!Passw0rd>' \
      -Q 'ALTER LOGIN SA WITH PASSWORD="<YourNewStrong!Passw0rd>"'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourStrong!Passw0rd>" `
      -Q "ALTER LOGIN SA WITH PASSWORD='<YourNewStrong!Passw0rd>'"
   ```
