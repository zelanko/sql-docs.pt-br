---
title: Depurar objetos de banco de dados CLR (Common Language Runtime)
description: SQL Server fornece suporte para depurar objetos Transact-SQL e CLR no banco de dados que integra SQL Server depurador com o depurador Microsoft Visual Studio.
ms.date: 10/06/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: how-to
helpviewer_keywords:
- database objects [CLR integration], debugging
- permissions [CLR integration]
- debugging [CLR integration]
- building database objects [CLR integration], debugging
- common language runtime [SQL Server], debugging
ms.assetid: 1332035c-d6ed-424d-8234-46ad21168319
author: rothja
ms.author: jroth
ms.openlocfilehash: 2a6e723c8ad5ff8c97a3b57edb554092211da4d7
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91785160"
---
# <a name="how-to-debug-clr-database-objects"></a>Como depurar objetos de banco de dados CLR

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
 
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte para depurar o [!INCLUDE[tsql](../../includes/tsql-md.md)] e objetos CLR (Common Language Runtime) no banco de dados. Os principais aspectos da depuração no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são a facilidade de configuração e uso, e a integração do depurador do SQL Server com o depurador do Microsoft Visual Studio. Além disso, a depuração funciona entre idiomas. Os usuários podem entrar diretamente em objetos CLR do [!INCLUDE[tsql](../../includes/tsql-md.md)] e vice-versa. O depurador Transact-SQL no SQL Server Management Studio não pode ser usado para depurar objetos de banco de dados gerenciados, mas você pode depurar os objetos por meio dos depuradores do Visual Studio. A depuração de objetos de banco de dados gerenciados no Visual Studio oferece suporte a todos os recursos de depuração comuns, tais como as instruções de "depuração parcial" e "depuração completa" dentro de rotinas executadas no servidor. Os depuradores podem definir pontos de interrupção, inspecionar a pilha de chamadas, inspecionar variáveis e modificar valores de variáveis durante a depuração. 

> [!NOTE]
> O Visual Studio .NET 2003 não pode ser usado para programação de integração CLR ou depuração. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece o .NET Framework pré-instalado, e o Visual Studio .NET 2003 não pode usar os assemblies do .NET Framework 2.0.  
  
## <a name="debugging-permissions-and-restrictions"></a>Restrições e permissões de depuração

A depuração é uma operação altamente privilegiada e, portanto, somente os membros da função de servidor fixa **sysadmin** podem fazer isso no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
As seguintes restrições se aplicam durante a depuração:  
  
- A depuração de rotinas de CLR é restrita a uma instância de depurador de cada vez. Essa limitação se aplica pois a execução do código de CLR inteira fica congelada quando um ponto de interrupção é atingido; a execução só prossegue quando o depurador sai do ponto de interrupção. Porém, você pode continuar depurando o [!INCLUDE[tsql](../../includes/tsql-md.md)] em outras conexões. Embora a depuração do [!INCLUDE[tsql](../../includes/tsql-md.md)] não congele outras execuções no servidor, ela pode colocar outras conexões em espera quando mantém um bloqueio.  
  
- As conexões existentes não podem ser depuradas, apenas as conexões novas, pois o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exige informações sobre o cliente e o ambiente do depurador para poder fazer a conexão.  
  
Devido às restrições anteriores, recomendamos que o [!INCLUDE[tsql](../../includes/tsql-md.md)] e o código CLR sejam depurados em um servidor de teste, e não em um servidor de produção.  
  
## <a name="overview"></a>Visão geral

A depuração no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] segue um modelo por conexão. Um depurador só pode detectar e depurar atividades para a conexão do cliente à qual ele está anexado. Como a funcionalidade do depurador não é limitada pelo tipo de conexão, pode-se depurar conexões do protocolo TDS e HTTP. Porém, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não permite a depuração de conexões existentes. A depuração oferece suporte a todos os recursos de depuração comuns dentro de rotinas executadas no servidor. A interação entre um depurador e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ocorre através do COM (Component Object Model) distribuído.  
  
Para obter mais informações e cenários sobre como depurar procedimentos armazenados gerenciados, funções, gatilhos, tipos definidos pelo usuário e agregações, consulte [SQL Server depuração do banco de dados de integração CLR](https://go.microsoft.com/fwlink/?LinkId=120378) na documentação do Visual Studio.  
  
O protocolo de rede TCP/IP deve estar habilitado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para permitir o uso do Visual Studio no desenvolvimento remoto, na depuração e no desenvolvimento. Para obter mais informações sobre como habilitar o protocolo TCP/IP no servidor, consulte [Configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md).  
  
## <a name="debugging-steps"></a>Etapas de depuração

Use as etapas a seguir para depurar um objeto de banco de dados CLR no Microsoft Visual Studio:

1. Abra Microsoft Visual Studio e crie um novo projeto de SQL Server. Você pode usar a instância do SQL LocalDB que vem com o Visual Studio.

2. Criar um novo tipo CLR SQL (C#):

   1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto e selecione **Adicionar**, **novo item...**. 
   1. Na janela **Adicionar novo item** , selecione o **procedimento armazenado SQL CLR C#**, **função definida pelo usuário**SQL CLR c#, **tipo definido pelo usuário SQL CLR C#**, **gatilho SQL CLR c#**, **agregação SQL CLR c#** ou **classe**.
   1. Especifique um nome para o arquivo de origem do novo tipo e, em seguida, selecione **Adicionar**.

3. Adicione código para o tipo novo no editor de texto. Para obter o código de exemplo de um procedimento armazenado de exemplo, consulte a seção de exemplo a seguir neste artigo.

4. Adicione um script que testa o tipo: 

   1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Adicionar**, **script...**. 
   1. Na janela **Adicionar novo item** , selecione **script (não em compilação)** e especifique um nome, como `Test.sql` . Selecione o botão **Adicionar**.
   1. Em **Gerenciador de soluções**, clique duas vezes no `Test.sql` nó para abrir o arquivo de origem do script de teste padrão.
   1. Adicione o script de teste (um que invoca o código a ser depurado) ao editor de texto. Consulte o exemplo na próxima seção para obter um script de exemplo.

5. Coloque um ou mais pontos de interrupção no código fonte. Clique com o botão direito do mouse em uma linha de código no editor de texto na função ou rotina que você deseja depurar. Selecione **ponto**de interrupção, **Inserir ponto de interrupção**. O ponto de interrupção é adicionado, destacando a linha de código em vermelho.

6. No menu **depurar** , selecione **Iniciar Depuração** para compilar, implantar e testar o projeto. O script de teste em `Test.sql` é executado e o objeto de banco de dados gerenciado é invocado.

7. Quando a seta amarela (designando o ponteiro de instrução) aparece no ponto de interrupção, a execução de código é pausada. Em seguida, você pode depurar o objeto de banco de dados gerenciado:

   1. Use **passar sobre** o menu **depurar** para avançar o ponteiro de instrução para a próxima linha de código.
   1. Use a janela **locais** para observar o estado dos objetos realçados no momento pelo ponteiro de instrução.
   1. Adicionar variáveis à janela de **inspeção** . Você pode observar o estado das variáveis observadas em toda a sessão de depuração, mesmo quando a variável não estiver na linha de código realçada no momento pelo ponteiro de instrução. 
   1. Selecione **continuar** no menu **depurar** para avançar o ponteiro de instrução para o próximo ponto de interrupção ou para concluir a execução da rotina se não houver mais pontos de interrupção.
  
## <a name="example-code"></a>Código de exemplo

O exemplo a seguir retorna a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o chamador.  
  
```csharp
using System.Data.SqlClient;
using Microsoft.SqlServer.Server;

public class StoredProcedures
{
    [Microsoft.SqlServer.Server.SqlProcedure]
    public static void GetVersion()
    {
        using (var connection = new SqlConnection("context connection=true"))
        {
            connection.Open();
            var command = new SqlCommand("select @@version", connection);
            SqlContext.Pipe.ExecuteAndSend(command);
        }
    }
}
```

## <a name="example-test-script"></a>Exemplo de script de teste

O script de teste a seguir mostra como invocar o `GetVersion` procedimento armazenado definido no exemplo anterior.  
  
```sql
EXEC GetVersion  
```  

## <a name="next-steps"></a>Próximas etapas
  
Para obter mais informações sobre como depurar código gerenciado usando o Visual Studio, consulte [depuração de código gerenciado](https://go.microsoft.com/fwlink/?LinkId=120377) na documentação do Visual Studio.  

Para obter mais informações, consulte [conceitos de programação de integração do Common Language Runtime](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
