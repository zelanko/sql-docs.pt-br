---
ms.openlocfilehash: 70c86c40f290c26db5bcbc3526d66466c20504d8
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68214889"
---
A conta **SA** é um administrador do sistema na instância do SQL Server que é criada durante a instalação. Depois de criar o contêiner do SQL Server, a variável de ambiente `MSSQL_SA_PASSWORD` especificada é detectável executando `echo $MSSQL_SA_PASSWORD` no contêiner. Para fins de segurança, altere sua senha SA.

1. Escolha uma senha forte para usar no usuário de SA.

1. Use `docker exec` para executar **sqlcmd** para alterar a senha usando o Transact-SQL. Substituir `<YourStrong!Passw0rd>` e `<YourNewStrong!Passw0rd>` com seus próprios valores de senha.

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
