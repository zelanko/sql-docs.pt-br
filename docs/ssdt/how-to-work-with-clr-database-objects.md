---
title: Trabalhar com objetos de banco de dados CLR
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.allowsqlclrdebugging
ms.assetid: 4a28d43d-eb5e-444d-aace-5df691f38709
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: f8aa504554cc973e5babbfe3c8512f59932fa147
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75226726"
---
# <a name="how-to-work-with-clr-database-objects"></a>Como trabalhar com objetos de banco de dados CLR

Além da linguagem de programação Transact\-SQL, você pode usar as linguagens .NET Framework para criar objetos de banco de dados que recuperam e atualizam dados. Objetos de banco de dados que são gravados em código gerenciado são chamados objetos de banco de dados CLR (Common Language Runtime) do SQL Server. Para obter uma explicação das vantagens de usar objetos de banco de dados CLR hospedados no SQL Server e também para saber como escolher entre o Transact\-SQL e o CLR, confira [Vantagens da integração CLR](../relational-databases/clr-integration/clr-integration-overview.md) e [Vantagens de usar código gerenciado para criar objetos de bancos de dados](https://msdn.microsoft.com/library/k2e1fb36.aspx).  
  
Para criar um objeto de banco de dados CLR usando o SQL Server Data Tools, crie um projeto de banco de dados e adicione um objeto de banco de dados CLR a ele. Ao contrário de versões anteriores do Visual Studio, você não precisa criar um projeto CLR separado e depois adicionar uma referência a ele do projeto de banco de dados. Quando você compila e publica o projeto de banco de dados, publica automaticamente os objetos CLR no projeto ao mesmo tempo. Depois que você publicar esses objetos CLR, eles poderão ser chamados e executados como qualquer outro objeto de banco de dados.  
  
As páginas de propriedades CLR e Compilação CLR contêm muitas configurações para usar objetos de bancos de dados CLR em seu projeto. Especificamente, a página de propriedades CLR tem uma configuração de nível de permissão para definir permissões no assembly CLR. Ela também tem a configuração "Gerar DDL" para controlar se a DDL dos objetos de banco de dados CLR adicionados ao projeto é gerada. A página de propriedades Compilação CLR contém todas as opções do compilador que você pode definir para configurar a compilação de código CLR no projeto. Para acessar essas páginas de propriedades, clique com o botão direito do mouse no projeto em **Gerenciador de Soluções** e selecione **Propriedades**.  
  
Para habilitar a depuração de objetos de banco de dados CLR, abra o **Pesquisador de Objetos do SQL Server**. Clique com o botão direito do mouse no servidor que contém os artefatos do banco de dados CLR que você deseja depurar e escolha **Permitir Depuração SQL/CLR**. Uma caixa de mensagem é exibida com o aviso: 'Observe que durante a depuração, todos os threads gerenciados no servidor serão interrompidos. Deseja habilitar a depuração SQL CLR neste servidor?". Quando você estiver depurando objetos de banco de dados CLR, a interrupção da execução interromperá todos os threads no servidor, afetando outros usuários. Por esse motivo, você não deve depurar aplicativos para objetos de banco de dados CLR em um servidor de produção. Você também deve observar que, depois de iniciar a depuração, será tarde demais para alterar as configurações no **Pesquisador de Objetos do SQL Server**. As alterações feitas no **Pesquisador de Objetos do SQL Server** não entrarão em vigor até que a próxima sessão de depuração seja iniciada.  
  
Para saber mais sobre os requisitos de compilação de objetos de banco de dados CLR, consulte [Criar objetos de banco de dados com a integração CLR (Common Language Runtime)](https://msdn.microsoft.com/library/ms131046.aspx).  
  
> [!WARNING]  
> Os procedimentos a seguir usam entidades criadas em procedimentos anteriores nas seções [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md) e [Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md).  
  
### <a name="to-add-a-clr-database-object-to-your-project"></a>Para adicionar um objeto de banco de dados ao seu projeto  
  
1.  Clique com o botão direito do mouse no projeto de banco de dados **TradeDev** no **Gerenciador de Soluções**, selecione **Adicionar** e **Novo Item**.  
  
2.  Selecione o modelo **C# SQL CLR** e, em seguida, **Função Definida pelo Usuário SQL CLR**. Aceite o nome padrão e clique em **Adicionar**.  
  
3.  Adicione o código a seguir ao corpo da classe. Esta função valida um número de telefone norte-americano. Deve conter 3 caracteres numéricos, opcionalmente incluídos em parênteses, seguidos por um conjunto de 3 caracteres numéricos e um conjunto de 4 caracteres numéricos. Exemplos de formatos suportados são (425) 555-0123, 425-555-0123, 425 555 0123 e 1-425-555-0123.  
  
    ```  
  
    [SqlFunction(IsDeterministic = true, IsPrecise = true)]  
    public static SqlBoolean validatePhone(SqlString phone)  
    {  
        string aNorthAmericanPhoneNumberPattern = @"^[01]?[- .]?(\([2-9]\d{2}\)|[2-9]\d{2})[- .]?\d{3}[- .]?\d{4}$";  
        if (!phone.IsNull)  
        {  
           Regex regex = new Regex(aNorthAmericanPhoneNumberPattern);  
           return regex.IsMatch(phone.Value);  
        }  
        return true;  
     }  
    ```  
  
4.  Observe que `Regex` está sublinhado em vermelho. Clique com o botão direito do mouse em `Regex` e selecione **Resolver**, depois, **usando System.Text.RegularExpressions**.  
  
5.  Se você estiver desenvolvendo em uma instância de servidor do Microsoft SQL Server 2012, poderá ignorar esta etapa. Caso contrário, o SQL Server 2005 e SQL Server 2008 somente dão suporte a projetos de banco de dados que são compilados com as versões 2.0, 3.0 ou 3.5 do .NET Framework. Para ter certeza de que a plataforma de destino do .NET está definida corretamente, clique com o botão direito do mouse no projeto de banco de dados **TradeDev** no **Gerenciador de Soluções** e selecione **Propriedades**. Na página de propriedades do **SQLCLR**, altere a **Plataforma de destino** para **.NET Framework 3.5** ou inferior. Clique em **Sim** na tela final para fechar e reabrir o projeto.  
  
6.  Clique com o botão direito do mouse no projeto **TradeDev** e selecione **Compilar** para compilar o projeto.  
  
7.  Clique duas vezes em Suppliers.sql e selecione **Exibir Designer** para abrir a tabela Suppliers no Designer de Tabela.  
  
8.  Clique na linha vazia na Grade de Colunas para adicionar uma nova coluna à tabela. Insira **telefone** para o campo **Nome**, **nvarchar (128)** para **Tipo de Dados** e deixe o campo **Permitir Nulos** marcado.  
  
9. Clique com o botão direito do mouse no nó **Verificar Restrições** no Painel Contexto e selecione **Adicionar Nova Restrição de Verificação**.  
  
10. Substitua a definição padrão da restrição no Painel de Script pelo seguinte.  
  
    ```  
    CONSTRAINT [CK_Suppliers_CheckPhone] CHECK (dbo.validatePhone(phone)=1),  
    ```  
  
    Isto garantirá que qualquer entrada para o novo campo de telefone será marcada usando o CLR UDF adicionado previamente.  
  
11. Pressione F5 para criar e implantar o projeto no banco de dados local.  
  
### <a name="to-use-clr-database-objects"></a>Para usar objetos de banco de dados CLR  
  
1.  No **Pesquisador de Objetos do SQL Server**, navegue até o banco de dados local onde você implantou seu projeto.  
  
2.  Por padrão, a integração CLR é desabilitada no SQL Server. Para usar objetos CLR, você deve habilitar a integração CLR. Para fazer isso, use a opção "clr habilitado" do procedimento armazenado sp_configure. Para saber mais, confira o [tópico da opção de clr habilitado](../relational-databases/clr-integration/clr-integration-enabling.md).  
  
    Clique com o botão direito do mouse no banco de dados e selecione **Nova Consulta**. No painel de consulta, cole o código a seguir e pressione o botão **Executar Consulta**.  
  
    ```  
  
    sp_configure 'clr enabled', 1;  
    GO  
    RECONFIGURE;  
    GO  
    ```  
  
3.  Clique com o botão direito do mouse na tabela Fornecedores e selecione **Exibir Dados**.  
  
4.  Insira **5** para **id**, **Contoso** para **nome**, deixe o campo **Endereço** vazio e **425 3122 1222** para **telefone**. Saia do campo **telefone** e observe que surge uma mensagem indicando que a instrução `INSERT` está em conflito com sua restrição de verificação existente, que verifica a entrada do campo **telefone** usando um padrão de telefone predefinido.  
  
5.  Altere sua entrada para **425 312 1222** e saia do campo. Observe que a entrada é aceita dessa vez.  
  
## <a name="see-also"></a>Consulte Também  
[Vantagens da integração CLR](../relational-databases/clr-integration/clr-integration-overview.md)  
[Vantagens de usar código gerenciado para criar objetos de banco de dados](https://msdn.microsoft.com/library/k2e1fb36.aspx)  
[Criando objetos de banco de dados com a integração CLR (Common Language Runtime)](https://msdn.microsoft.com/library/ms131046.aspx)  
  
