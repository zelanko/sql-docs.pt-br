---
title: Erros de script do R no SQL Server Machine Learning e R Services | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 941a8bbc5e7326d87dcdba8c822fb2c3f2190900
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51695434"
---
# <a name="r-scripting-errors-in-sql-server"></a>Erros de script do R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo documenta várias gerrors. inittabem durante a execução de código R no SQL Server. A lista não é abrangente. Há muitos pacotes e erros podem variar entre as versões do mesmo pacote. É recomendável publicar erros de script na [Fórum do Machine Learning Server](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR), que oferece suporte para os componentes usados no R Services (no banco de dados), o Microsoft R Client e Microsoft R Server de aprendizado de máquina.

**Aplica-se a:** SQL Server 2016 R Services, SQL Server 2017 serviços de Machine Learning


## <a name="valid-script-fails-in-t-sql-or-in-stored-procedures"></a>Falha de script válida em T-SQL ou em procedimentos armazenados

Antes de encapsular seu código R em um procedimento armazenado, é recomendável executar o código R em um IDE externo ou em uma das ferramentas do R, como RTerm ou RGui. Usando esses métodos, você pode testar e depurar o código usando as mensagens de erro detalhadas que são retornadas pelo R.

No entanto, às vezes, códigos que funcionam perfeitamente em um IDE externo ou o utilitário podem falhar ao executar em um procedimento armazenado ou o contexto de computação em um SQL Server. Se isso acontecer, há uma variedade de problemas para procurar antes que você pode presumir que o pacote não funciona no SQL Server.

1. Verifique se o Launchpad estiver em execução.

2. Examine as mensagens para ver se os dados de entrada ou dados de saída contém colunas com tipos de dados incompatíveis ou sem suporte. Por exemplo, consultas em um banco de dados SQL geralmente retornam GUIDs ou RowGUIDs, que não têm suporte. Para obter mais informações, consulte [tipos de dados e bibliotecas de R](r/r-libraries-and-data-types.md).

3. Examine as páginas de ajuda para funções R individuais determinar se todos os parâmetros têm suporte para o contexto de computação do SQL Server. Para obter ajuda de ScaleR, use os comandos de ajuda embutida R ou consulte [referência de pacote](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler).

Se o tempo de execução de R está funcionando, mas o script retorna erros, recomendamos que você tente depurar o script em um ambiente de desenvolvimento dedicado do R, como as ferramentas do R para Visual Studio.

Também recomendamos que você analise e ligeiramente reescreva o script para corrigir quaisquer problemas com tipos de dados que podem surgir quando você move dados entre R e o mecanismo de banco de dados. Para obter mais informações, consulte [tipos de dados e bibliotecas de R](r/r-libraries-and-data-types.md).

Além disso, você pode usar o pacote de sqlrutils para agrupar seu script R em um formato que seja mais facilmente consumido como um procedimento armazenado. Para obter mais informações, consulte:
* [Gerar um procedimento armazenado para código R usando o pacote sqlrutils](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
* [Criar um procedimento armazenado usando sqlrutils](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="script-returns-inconsistent-results"></a>Script retorna resultados inconsistentes

Scripts de R podem retornar valores diferentes em um contexto do SQL Server, por vários motivos:

- Conversão implícita de tipo é executado automaticamente em alguns tipos de dados, quando os dados são passados entre o SQL Server e R. Para obter mais informações, consulte [tipos de dados e bibliotecas de R](r/r-libraries-and-data-types.md).

- Determine se o número de bits é um fator. Por exemplo, geralmente há diferenças nos resultados de operações matemáticas para bibliotecas de ponto flutuante 32 bits e 64 bits.

- Determine se NaNs foram produzidos em qualquer operação. Isso pode invalidar os resultados.

- Pequenas diferenças podem ser aumentadas quando você pega um recíproco de um número próximo de zero.

- Erros de arredondamento acumulados podem causar coisas como valores que são menor que zero, em vez de zero.

## <a name="implied-authentication-for-remote-execution-via-odbc"></a>Autenticação implícita para execução remota por meio de ODBC

Se você se conectar à [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] comandos de computador para executar o R usando o **RevoScaleR** funções, você poderá receber um erro ao usar chamadas ODBC que gravam dados no servidor. Esse erro ocorre somente quando você estiver usando a autenticação do Windows.

O motivo é que as contas de trabalho que são criadas para o R Services não tem permissão para se conectar ao servidor. Portanto, as chamadas ODBC não podem ser executadas em seu nome. O problema não ocorre com logons do SQL Server porque, com logons do SQL Server, as credenciais são passadas explicitamente do cliente R para a instância do SQL Server e, em seguida, para o ODBC. No entanto, também é menos segura do que usando a autenticação do Windows usar logons do SQL Server.

Para habilitar suas credenciais do Windows a ser passado com segurança a partir de um script que tiver iniciado remotamente, SQL Server deve emular suas credenciais. Esse processo é denominado _autenticação implícita_. Para fazer isso funcionar, as contas de trabalho que executam scripts R ou Python no computador do SQL Server devem ter as permissões corretas.

1. Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] como um administrador na instância onde você deseja executar o código R.

2. Execute o script a seguir. Certifique-se de editar o nome de grupo do usuário, se você tiver alterado o padrão e os nomes de computador e da instância.

    ```SQL
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

## <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>Evitar a limpeza do espaço de trabalho durante a execução do R em um contexto de computação do SQL

Embora a limpar o espaço de trabalho é comum quando você trabalha no console do R, ele pode ter consequências não intencionais em um SQL contexto de computação.

`revoScriptConnection` é um objeto no espaço de trabalho R que contém informações sobre uma sessão do R que é chamada a partir do SQL Server. No entanto, se seu código R inclui um comando para limpar o espaço de trabalho (como `rm(list=ls())`), todas as informações sobre a sessão e outros objetos no espaço de trabalho do R também serão limpos.

Como alternativa, evite a limpeza indiscriminada de variáveis e outros objetos durante a execução do R no SQL Server. Você pode excluir variáveis específicas usando o **remover** função:

```R
remove('name1', 'name2', ...)
```

Se houver várias variáveis a serem excluídas, sugerimos que você salve os nomes das variáveis temporárias em uma lista e, em seguida, realizar coletas de lixo periódica na lista.



## <a name="next-steps"></a>Próximas etapas

[Problemas conhecidos e solução de problemas de serviços de aprendizado de máquina](machine-learning-troubleshooting-faq.md)

[Coleta de dados para solução de problemas de aprendizado de máquina](data-collection-ml-troubleshooting-process.md)

[Perguntas frequentes sobre atualização e instalação](r/upgrade-and-installation-faq-sql-server-r-services.md)

[Solucionar problemas de conexões do mecanismo de banco de dados](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
