---
title: Depurando objetos de banco de dados CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- database objects [CLR integration], debugging
- permissions [CLR integration]
- debugging [CLR integration]
- building database objects [CLR integration], debugging
- common language runtime [SQL Server], debugging
ms.assetid: 1332035c-d6ed-424d-8234-46ad21168319
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 70b092f81030c7905fe1d771844369f2d59317b9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62919014"
---
# <a name="debugging-clr-database-objects"></a>Depurando objetos de banco de dados CLR
  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oferece suporte para depurar o [!INCLUDE[tsql](../../../includes/tsql-md.md)] e objetos CLR (Common Language Runtime) no banco de dados. Os principais aspectos da depuração no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] são a facilidade de configuração e uso, e a integração do depurador do SQL Server com o depurador do Microsoft Visual Studio. Além disso, a depuração funciona entre idiomas. Os usuários podem entrar diretamente em objetos CLR do [!INCLUDE[tsql](../../../includes/tsql-md.md)] e vice-versa. O depurador Transact-SQL no SQL Server Management Studio não pode ser usado para depurar objetos de banco de dados gerenciados, mas você pode depurar os objetos por meio dos depuradores do Visual Studio. A depuração de objetos de banco de dados gerenciados no Visual Studio oferece suporte a todos os recursos de depuração comuns, tais como as instruções de "depuração parcial" e "depuração completa" dentro de rotinas executadas no servidor. Os depuradores podem definir pontos de interrupção, inspecionar a pilha de chamadas, inspecionar variáveis e modificar valores de variáveis durante a depuração. Observe que o Visual Studio .NET 2003 não pode ser usado na programação de integração ou na depuração do CLR. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornece o .NET Framework pré-instalado, e o Visual Studio .NET 2003 não pode usar os assemblies do .NET Framework 2.0.  
  
 Para obter mais informações sobre como depurar código gerenciado usando o Visual Studio, consulte o "[Debugging Managed Code](https://go.microsoft.com/fwlink/?LinkId=120377)" tópico na documentação do Visual Studio.  
  
## <a name="debugging-permissions-and-restrictions"></a>Depurando permissões e restrições  
 A depuração é uma operação altamente privilegiada e, portanto, somente os membros da **sysadmin** função de servidor fixa têm permissão para fazer isso no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 As seguintes restrições se aplicam durante a depuração:  
  
-   A depuração de rotinas de CLR é restrita a uma instância de depurador de cada vez. Essa limitação se aplica pois a execução do código de CLR inteira fica congelada quando um ponto de interrupção é atingido; a execução só prossegue quando o depurador sai do ponto de interrupção. Porém, você pode continuar depurando o [!INCLUDE[tsql](../../../includes/tsql-md.md)] em outras conexões. Embora a depuração do [!INCLUDE[tsql](../../../includes/tsql-md.md)] não congele outras execuções no servidor, ela pode colocar outras conexões em espera quando mantém um bloqueio.  
  
-   As conexões existentes não podem ser depuradas, apenas as conexões novas, pois o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] exige informações sobre o cliente e o ambiente do depurador para poder fazer a conexão.  
  
 Devido às restrições anteriores, recomendamos que o [!INCLUDE[tsql](../../../includes/tsql-md.md)] e o código CLR sejam depurados em um servidor de teste, e não em um servidor de produção.  
  
## <a name="overview-of-debugging-managed-database-objects"></a>Visão geral da depuração de objetos de banco de dados gerenciados  
 A depuração no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] segue um modelo por conexão. Um depurador só pode detectar e depurar atividades para a conexão do cliente à qual ele está anexado. Como a funcionalidade do depurador não é limitada pelo tipo de conexão, pode-se depurar conexões do protocolo TDS e HTTP. Porém, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não permite a depuração de conexões existentes. A depuração oferece suporte a todos os recursos de depuração comuns dentro de rotinas executadas no servidor. A interação entre um depurador e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ocorre através do COM (Component Object Model) distribuído.  
  
 Para obter mais informações e cenários sobre a depuração de procedimentos armazenados gerenciados, funções, gatilhos, tipos definidos pelo usuário e agregações, consulte o "[depuração de banco de dados do SQL Server CLR Integration](https://go.microsoft.com/fwlink/?LinkId=120378)" tópico no Visual Studio documentação.  
  
 O protocolo de rede TCP/IP deve estar habilitado na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para permitir o uso do Visual Studio no desenvolvimento remoto, na depuração e no desenvolvimento. Para obter mais informações sobre como habilitar o protocolo TCP/IP no servidor, consulte [configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md).  
  
#### <a name="to-debug-a-managed-database-object"></a>Para depurar um objeto de banco de dados gerenciado  
  
1.  Abra o Microsoft Visual Studio, crie um novo projeto do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e estabeleça uma conexão com um banco de dados em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
2.  Crie um tipo novo. Na **Gerenciador de soluções**, clique com botão direito no projeto, selecione **Add** e **Novo Item...** Dos **Adicionar Novo Item** janela, selecione **procedimento armazenado**, **função definida pelo usuário**, **tipo definido pelo usuário**,  **Disparador**, **agregada**, ou **classe**. Especifique um nome para o arquivo de origem do novo tipo e clique em **adicionar**.  
  
3.  Adicione código para o tipo novo no editor de texto. Para obter um código de exemplo de um procedimento armazenado de exemplo, consulte a seção correspondente mais adiante nesse tópico.  
  
4.  Adicione um script que testa o tipo. Na **Gerenciador de soluções**, expanda o **TestScripts** directory clique duas vezes em **Test. SQL** para abrir o arquivo de origem do script de teste padrão. Adicione o script de teste, aquele que invoca o código a ser depurado, no editor de texto. Veja um script de exemplo a seguir.  
  
5.  Coloque um ou mais pontos de interrupção no código fonte. Clique duas vezes em uma linha de código no editor de texto, dentro da função ou rotina que você deseja depurar, e selecione **ponto de interrupção** e **Inserir ponto de interrupção**. O ponto de interrupção é adicionado, destacando a linha de código em vermelho.  
  
6.  No **Debug** menu, selecione **iniciar depuração** para compilar, implantar e testar o projeto. O script de teste em Test.sql será executado e o objeto de banco de dados gerenciado será invocado.  
  
7.  Quando a seta amarela que designa o ponteiro de instrução aparece no ponto de interrupção, há uma pausa na execução do código e você pode começar a depurar seu objeto de banco de dados gerenciado. Você pode **Step Over** da **depurar** menu para avançar o ponteiro de instrução para a próxima linha de código. O **Locals** janela é usada para observar o estado dos objetos destacados no momento pelo ponteiro de instrução. As variáveis podem ser adicionadas para o **inspeção** janela. O estado de variáveis inspecionadas pode ser observado na sessão de depuração inteira, e não apenas quando a variável está na linha de código destacada no momento pelo ponteiro de instrução. Selecione Continuar no menu Depurar para avançar o ponteiro de instrução até o próximo ponto de interrupção ou para concluir a execução da rotina se não houver mais pontos de interrupção.  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir retorna a versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para o chamador.  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void GetVersion()  
   {  
   using(SqlConnection connection = new SqlConnection("context connection=true"))   
   {  
      connection.Open();  
      SqlCommand command = new SqlCommand("select @@version",  
                                           connection);  
      SqlContext.Pipe.ExecuteAndSend(command);  
      }  
   }  
}  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
Partial Public Class StoredProcedures   
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub GetVersion()  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT @@VERSION", connection)  
            SqlContext.Pipe.ExecuteAndSend(command)  
        End Using  
    End Sub  
End Class  
```  
  
 O script de teste a seguir invoca o procedimento armazenado GetVersion, definido anteriormente.  
  
```  
EXEC GetVersion  
```  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos de programação da Integração CLR &#40;Common Language Runtime&#41;](common-language-runtime-clr-integration-programming-concepts.md)  
  
  
