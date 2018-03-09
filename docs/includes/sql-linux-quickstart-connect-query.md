## <a name="connect-locally"></a>Conectar-se localmente

As etapas a seguir usam o **sqlcmd** para conectar-se localmente à nova instância do SQL Server.

1. Execute o **sqlcmd** com parâmetros para o nome do SQL Server (-S), o nome de usuário (-U) e a senha (-P). Neste tutorial, você está se conectando localmente, portanto, o nome do servidor é `localhost`. O nome de usuário é `SA` e a senha é a mesma fornecida para a conta SA durante a instalação.

   ```bash
   sqlcmd -S localhost -U SA -P '<YourPassword>'
   ```

   > [!TIP]
   > É possível omitir a senha na linha de comando para receber uma solicitação para inseri-la.

   > [!TIP]
   > Se depois você decidir se conectar remotamente, especifique o nome do computador ou endereço IP do parâmetro **-S** e verifique se a porta 1433 está aberta no firewall.

1. Se isso funcionar, você será levado a um prompt de comando **sqlcmd**: `1>`.

1. Se houver uma falha de conexão, primeiro, tente diagnosticar o problema da mensagem de erro. Em seguida, examine as [recomendações de solução de problemas de conexão](../linux/sql-server-linux-troubleshooting-guide.md#connection).

## <a name="create-and-query-data"></a>Criar e consultar dados
As seções a seguir descrevem como usar o **sqlcmd** para criar um novo banco de dados, adicionar dados e executar uma consulta simples.

### <a name="create-a-new-database"></a>Criar um novo banco de dados

As etapas a seguir criam um novo banco de dados denominado `TestDB`.

1. No prompt de comando **sqlcmd**, cole o seguinte comando Transact-SQL para criar um banco de dados de teste:

   ```sql
   CREATE DATABASE TestDB
   ```

1. Na próxima linha, grave uma consulta para retornar o nome de todos os bancos de dados do servidor:

   ```sql
   SELECT Name from sys.Databases
   ```

1. Os dois comandos anteriores não foram executados imediatamente. Digite `GO` em uma nova linha para executar os comandos anteriores:

   ```sql
   GO
   ```

### <a name="insert-data"></a>Inserir dados

Em seguida, crie uma nova tabela, `Inventory`, e insira duas novas linhas.

1. No prompt de comando **sqlcmd**, altere o contexto para o novo banco de dados `TestDB`:

   ```sql
   USE TestDB
   ```

1. Criar nova tabela denominada `Inventory`:

   ```sql
   CREATE TABLE Inventory (id INT, name NVARCHAR(50), quantity INT)
   ```

1. Inserir dados na nova tabela:

   ```sql
   INSERT INTO Inventory VALUES (1, 'banana', 150); INSERT INTO Inventory VALUES (2, 'orange', 154);
   ```

1. Digite `GO` para executar os comandos anteriores:

   ```sql
   GO
   ```

### <a name="select-data"></a>Selecionar dados

Agora, execute uma consulta para retornar da tabela `Inventory`.

1. No prompt de comando **sqlcmd**, digite uma consulta que retorna linhas de tabela `Inventory` em que a quantidade é maior que 152:

   ```sql
   SELECT * FROM Inventory WHERE quantity > 152;
   ```

1. Execute o comando:

   ```sql
   GO
   ```

### <a name="exit-the-sqlcmd-command-prompt"></a>Saia do prompt de comando sqlcmd

Para encerrar a sessão **sqlcmd**, digite `QUIT`:

```sql
QUIT
```

## <a name="connect-from-windows"></a>Conecte-se do Windows

As ferramentas do SQL Server no Windows se conectam às instâncias do SQL Server no Linux da mesma forma que se conectam a qualquer instância remota do SQL Server.

Se você tiver um computador Windows que pode se conectar a um computador Linux, tente as mesmas etapas deste tópico de um prompt de comando do Windows executando o **sqlcmd**. Apenas certifique-se de que está utilizando o nome de destino do computador Linux ou o endereço IP em vez do localhost e de que a porta TCP 1433 está aberta. Se houver problemas ao se conectar do Windows, consulte [recomendações de solução de problemas de conexão](../linux/sql-server-linux-troubleshooting-guide.md#connection).

Para outras ferramentas que executam o Windows, mas se conectam ao SQL Server no Linux, consulte:

- [SSMS (SQL Server Management Studio)](../linux/sql-server-linux-develop-use-ssms.md)
- [Windows PowerShell](../linux/sql-server-linux-manage-powershell.md)
- [SSDT (SQL Server Data Tools)](../linux/sql-server-linux-develop-use-ssdt.md)

## <a name="additional-resources"></a>Recursos adicionais

Para outros cenários de instalação, veja os seguintes recursos:

|||
|---|---|
| [Atualizar](../linux/sql-server-linux-setup.md#upgrade) | Saiba como atualizar uma instalação existente do SQL Server no Linux |
| [Desinstalação](../linux/sql-server-linux-setup.md#uninstall) | Desinstalar o SQL Server no Linux |
| [Instalação autônoma](../linux/sql-server-linux-setup.md#unattended) | Saiba como gerar o script da instalação sem prompts |
| [Instalação offline](../linux/sql-server-linux-setup.md#offline) | Saiba como baixar manualmente os pacotes para instalação offline |

Para explorar outras maneiras de se conectar e gerenciar o SQL Server, explore as seguintes ferramentas:

|||
|---|---|
| [Visual Studio Code](../linux/sql-server-linux-develop-use-vscode.md) | Um editor de código da GUI de plataforma cruzada que executam instruções Transact-SQL com a extensão mssql. |
| [Operações do SQL Server Studio](../sql-operations-studio/index.md) | Um utilitário de gerenciamento de banco de dados de GUI de plataforma cruzada. |
| [mssql-cli](https://github.com/dbcli/mssql-cli/tree/master/doc) | Uma interface de linha de comando de plataforma cruzada para a execução de comandos Transact-SQL. |
| [SQL Server Management Studio](../linux/sql-server-linux-develop-use-ssms.md) | Um utilitário de gerenciamento de banco de dados de GUI baseada no Windows que pode se conectar e gerenciar instâncias do SQL Server no Linux. |

Para saber mais sobre como escrever consultas e instruções em Transact-SQL, veja [Tutorial: Escrever instruções de Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md).

> [!TIP]
> Para obter respostas para perguntas frequentes, consulte o [SQL Server nas perguntas frequentes sobre o Linux](../linux/sql-server-linux-faq.md).

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Explore os tutoriais para SQL Server no Linux](../linux/sql-server-linux-migrate-restore-database.md)