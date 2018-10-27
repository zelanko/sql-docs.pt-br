### <a id="sampledata"></a> Carregar dados de exemplo

Tutoriais de cluster de big data do SQL Server usam um conjunto comum de dados de exemplo. Use as seguintes etapas para configurar os dados de exemplo no seu cluster de big data:

1. Se você não tem as ferramentas de linha de comando do SQL Server (**sqlcmd** e **bcp**) pela primeira vez instalado, instalar essas ferramentas com um dos links:

   * **Windows**: [ferramentas de linha de comando de instalar o SQL Server no Windows](https://www.microsoft.com/download/details.aspx?id=53591)
   * **Linux**: [ferramentas de linha de comando de instalar o SQL Server no Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup-tools)

1. Baixe o arquivo de backup de exemplo [tpcxbb_1gb.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak) em seu computador.

1. Navegue até o cluster de big data do SQL Server 2019 [diretório de exemplos](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster).

1. Baixe o [bootstrap-exemplo-db.sql](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql) script Transact-SQL.

1. Baixe e execute um dos seguintes scripts de dois exemplo na linha de comando:

   * **Windows**: [bootstrap-exemplo-db.cmd](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd)
   * **Linux**: [bootstrap-exemplo-db.sh](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh)

   > [!TIP]
   > Você pode obter instruções de uso ao executar o script sem parâmetros.

O script restaura o banco de dados de exemplo para a instância mestre do SQL Server e também carrega dados em HDFS no pool de armazenamento.