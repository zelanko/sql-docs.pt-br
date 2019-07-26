---
title: Erros e solução de problemas de script R
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 268b3df72d468170fbefae2557892c49fd15515c
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470300"
---
# <a name="r-scripting-errors-in-sql-server"></a>Erros de script do R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo documenta vários scripts do gerrors ao executar o código R no SQL Server. A lista não é abrangente. Há muitos pacotes e os erros podem variar entre as versões do mesmo pacote. É recomendável postar erros de script no [Fórum de Machine Learning Server](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR), que dá suporte aos componentes de Machine Learning usados no R Services (no banco de dados), Microsoft R Client e Microsoft R Server.

**Aplica-se a:** SQL Server 2016 R Services, SQL Server 2017 Serviços de Machine Learning


## <a name="valid-script-fails-in-t-sql-or-in-stored-procedures"></a>O script válido falha no T-SQL ou em procedimentos armazenados

Antes de encapsular o código R em um procedimento armazenado, é uma boa ideia executar o código R em um IDE externo ou em uma das ferramentas de R, como RTerm ou RGui. Usando esses métodos, você pode testar e depurar o código usando as mensagens de erro detalhadas que são retornadas pelo R.

No entanto, às vezes, o código que funciona perfeitamente em um IDE ou utilitário externo pode falhar ao ser executado em um procedimento armazenado ou em um contexto de computação SQL Server. Se isso acontecer, há uma variedade de problemas a serem procurados antes que você possa pressupor que o pacote não funciona em SQL Server.

1. Verifique se o Launchpad está em execução.

2. Examine as mensagens para ver se os dados de entrada ou de saída contêm colunas com tipos de dados incompatíveis ou sem suporte. Por exemplo, consultas em um banco de dados SQL geralmente retornam GUIDs ou RowGuids, ambos sem suporte. Para obter mais informações, consulte [bibliotecas e tipos de dados do R](r/r-libraries-and-data-types.md).

3. Examine as páginas de ajuda para funções individuais do R para determinar se todos os parâmetros têm suporte para o contexto de computação SQL Server. Para obter ajuda do scaler, use os comandos de ajuda de R embutidos ou consulte a [referência do pacote](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler).

Se o tempo de execução do R estiver funcionando, mas o script retornar erros, recomendamos que você tente depurar o script em um ambiente de desenvolvimento de R dedicado, como Ferramentas do R para Visual Studio.

Também recomendamos que você revise e reescreva um pouco o script para corrigir quaisquer problemas com tipos de dados que possam surgir quando você mover dados entre o R e o mecanismo de banco de dados. Para obter mais informações, consulte [bibliotecas e tipos de dados do R](r/r-libraries-and-data-types.md).

Além disso, você pode usar o pacote sqlrutils para agrupar o script R em um formato que é mais facilmente consumido como um procedimento armazenado. Para obter mais informações, consulte:
* [pacote sqlrutils](r/ref-r-sqlrutils.md)
* [Criar um procedimento armazenado usando sqlrutils](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="script-returns-inconsistent-results"></a>O script retorna resultados inconsistentes

Os scripts do R podem retornar valores diferentes em um contexto de SQL Server, por vários motivos:

- A conversão implícita de tipo é executada automaticamente em alguns tipos de dados, quando os dados são passados entre SQL Server e R. Para obter mais informações, consulte [bibliotecas e tipos de dados do R](r/r-libraries-and-data-types.md).

- Determine se o bit de bits é um fator. Por exemplo, geralmente há diferenças nos resultados de operações matemáticas para bibliotecas de ponto flutuante de 32 bits e 64 bits.

- Determine se os NaNs foram produzidos em qualquer operação. Isso pode invalidar os resultados.

- Pequenas diferenças podem ser amplificadas quando você assume um recíproco de um número próximo de zero.

- Os erros de arredondamento acumulados podem causar coisas como valores menores que zero em vez de zero.

## <a name="implied-authentication-for-remote-execution-via-odbc"></a>Autenticação implícita para execução remota via ODBC

Se você se conectar ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] computador para executar comandos do R usando as funções **RevoScaleR** , poderá receber um erro ao usar chamadas ODBC que gravam dados no servidor. Esse erro ocorre somente quando você está usando a autenticação do Windows.

O motivo é que as contas de trabalho criadas para o R Services não têm permissão para se conectar ao servidor. Portanto, as chamadas ODBC não podem ser executadas em seu nome. O problema não ocorre com logons do SQL porque, com logons do SQL, as credenciais são passadas explicitamente do cliente R para a instância de SQL Server e, em seguida, para o ODBC. No entanto, o uso de logons do SQL também é menos seguro do que usar a autenticação do Windows.

Para permitir que suas credenciais do Windows sejam passadas com segurança de um script que é iniciado remotamente, SQL Server deve emular suas credenciais. Esse processo é chamado de _autenticação implícita_. Para fazer isso funcionar, as contas de trabalho que executam scripts R ou Python no computador SQL Server devem ter as permissões corretas.

1. Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] como um administrador na instância em que você deseja executar o código R.

2. Execute o script a seguir. Certifique-se de editar o nome do grupo de usuários, se você alterou o padrão e os nomes do computador e da instância.

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

## <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>Evite limpar o espaço de trabalho enquanto estiver executando o R em um contexto de computação do SQL

Embora a limpeza do espaço de trabalho seja comum quando você trabalha no console do R, ela pode ter consequências indesejadas em um contexto de computação do SQL.

`revoScriptConnection`é um objeto no espaço de trabalho do R que contém informações sobre uma sessão de R que é chamada de SQL Server. No entanto, se o código R incluir um comando para limpar o espaço de `rm(list=ls())`trabalho (como), todas as informações sobre a sessão e outros objetos no espaço de trabalho do R também serão apagadas.

Como alternativa, evite a limpeza indiscriminado de variáveis e outros objetos enquanto você estiver executando o R no SQL Server. Você pode excluir variáveis específicas usando a função **remover** :

```R
remove('name1', 'name2', ...)
```

Se houver várias variáveis a serem excluídas, sugerimos que você salve os nomes das variáveis temporárias em uma lista e, em seguida, execute as coletas de lixo periódicas na lista.



## <a name="next-steps"></a>Próximas etapas

[Solução de problemas Serviços de Machine Learning e questões conhecidas](machine-learning-troubleshooting-faq.md)

[Coleta de dados para solução de problemas de aprendizado de máquina](data-collection-ml-troubleshooting-process.md)

[Perguntas frequentes sobre atualização e instalação](r/upgrade-and-installation-faq-sql-server-r-services.md)

[Solucionar problemas de conexões do Database Engine](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
