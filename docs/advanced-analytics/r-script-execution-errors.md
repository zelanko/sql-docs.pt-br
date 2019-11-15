---
title: Solucionar problemas de scripts do R
description: Este artigo documenta vários erros de script ao executar o código R no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d1cfd06fd881c4749879365feda14e3cfcb877a9
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727506"
---
# <a name="r-scripting-errors-in-sql-server"></a>Erros de script do R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo documenta vários erros de script ao executar o código R no SQL Server. A lista não é completa. Existem muitos pacotes e os erros podem variar entre as versões do mesmo pacote. É recomendável publicar erros de script no [fórum do Machine Learning Server](https://social.msdn.microsoft.com/Forums/home?category=MicrosoftR), que dá suporte aos componentes de aprendizado de máquina usados no R Services (no banco de dados), no Microsoft R Client e no Microsoft R Server.

## <a name="valid-script-fails-in-t-sql-or-in-stored-procedures"></a>O script válido falha no T-SQL ou nos procedimentos armazenados

Antes de encapsular o código R em um procedimento armazenado, é uma boa ideia executar o código R em um IDE externo ou em uma das ferramentas do R, como RTerm ou RGui. Ao usar esses métodos, você pode testar e depurar o código usando as mensagens de erro detalhadas que são retornadas pelo R.

No entanto, às vezes o código que funciona perfeitamente em um IDE ou utilitário externo pode falhar ao ser executado em um procedimento armazenado ou em um contexto de computação do SQL Server. Se isso acontecer, existem diversos problemas a serem procurados antes de supor que o pacote não funciona no SQL Server.

1. Verifique se a Launchpad está em execução.

2. Examine as mensagens para ver se os dados de entrada ou de saída contêm colunas com tipos de dados incompatíveis ou sem suporte. Por exemplo, consultas em um Banco de Dados SQL geralmente retornam GUIDs ou RowGUIDs, ambos sem suporte. Para obter mais informações, confira [Tipos de dados e bibliotecas do R](r/r-libraries-and-data-types.md).

3. Examine as páginas de ajuda para funções individuais do R para determinar se todos os parâmetros têm suporte para o contexto de computação do SQL Server. Para obter ajuda do ScaleR, use os comandos da Ajuda do R embutidos ou confira a [Referência de Pacote](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler).

Se o runtime do R estiver funcionando, mas o script retornar erros, recomendamos tentar depurar o script em um ambiente de desenvolvimento do R dedicado, como Ferramentas do R para Visual Studio.

Também recomendamos examinar e reescrever um pouco o script para corrigir quaisquer problemas com tipos de dados que possam surgir ao mover dados entre o R e o mecanismo de banco de dados. Para obter mais informações, confira [Tipos de dados e bibliotecas do R](r/r-libraries-and-data-types.md).

Além disso, você pode usar o pacote sqlrutils para agrupar o script R em um formato mais facilmente consumido como um procedimento armazenado. Para obter mais informações, consulte:
* [Pacote sqlrutils](r/ref-r-sqlrutils.md)
* [Criar um procedimento armazenado usando sqlrutils](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="script-returns-inconsistent-results"></a>O script retorna resultados inconsistentes

Os scripts do R podem retornar valores diferentes em um contexto do SQL Server por vários motivos:

- A conversão implícita de tipo é executada automaticamente em alguns tipos de dados quando os dados são passados entre o SQL Server e o R. Para obter mais informações, confira [Tipos de dados e bibliotecas do R](r/r-libraries-and-data-types.md).

- Determine se o número de bit é um fator. Por exemplo, geralmente há diferenças nos resultados de operações matemáticas para bibliotecas de ponto flutuante de 32 bits e de 64 bits.

- Determine se os NaNs foram produzidos em qualquer operação. Isso pode invalidar os resultados.

- Pequenas diferenças podem ser amplificadas quando você usa um recíproco de um número próximo de zero.

- Os erros de arredondamento acumulados podem causar coisas como valores menores que zero, em vez de zero.

## <a name="implied-authentication-for-remote-execution-via-odbc"></a>Autenticação implícita para execução remota via ODBC

Se você conectar-se ao computador [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para executar comandos do R usando as funções **RevoScaleR**, poderá receber um erro ao usar chamadas ODBC que gravam dados no servidor. Esse erro ocorre somente quando você está usando a autenticação do Windows.

O motivo é que as contas de trabalho criadas para o R Services não têm permissão para se conectar ao servidor. Portanto, não é possível executar as chamadas ODBC em seu nome. O problema não ocorre com logons do SQL porque, com logons do SQL, as credenciais são passadas explicitamente do cliente R para a instância do SQL Server e, em seguida, para o ODBC. No entanto, usar logons do SQL também é menos seguro do que usar a autenticação do Windows.

Para permitir que suas credenciais do Windows sejam passadas com segurança de um script iniciado remotamente, o SQL Server deve emular suas credenciais. Esse processo é chamado de _autenticação implícita_. Para fazer isso funcionar, as contas de trabalho que executam scripts do R ou do Python no computador SQL Server devem ter as permissões corretas.

1. Abra o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] como administrador na instância em que você deseja executar o código R.

2. Execute o script a seguir. Edite o nome do grupo de usuários, caso tenha alterado o padrão e os nomes do computador e da instância.

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

## <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>Evite limpar o workspace enquanto estiver executando o R em um contexto de computação do SQL

Embora a limpeza do workspace seja comum ao trabalhar no console do R, ela poderá trazer consequências indesejadas em um contexto de computação do SQL.

O `revoScriptConnection` é um objeto no workspace do R que contém informações sobre uma sessão do R chamada por meio do SQL Server. No entanto, se o código R incluir um comando para limpar o workspace (como `rm(list=ls())`), todas as informações sobre a sessão e outros objetos no workspace do R também serão limpos.

Como alternativa, evite a limpeza indiscriminada de variáveis e outros objetos ao executar o R no SQL Server. Você pode excluir variáveis específicas usando a função **remover**:

```R
remove('name1', 'name2', ...)
```

Se houver diversas variáveis a serem excluídas, sugerimos salvar os nomes das variáveis temporárias em uma lista e executar a coleta de lixo periódica.



## <a name="next-steps"></a>Próximas etapas

[Solução de problemas dos Serviços de Machine Learning e problemas conhecidos](machine-learning-troubleshooting-faq.md)

[Coleta de dados para a solução de problemas de aprendizado de máquina](data-collection-ml-troubleshooting-process.md)

[Perguntas frequentes sobre atualização e instalação](r/upgrade-and-installation-faq-sql-server-r-services.md)

[Solucionar problemas de conexões de mecanismo de banco de dados](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
