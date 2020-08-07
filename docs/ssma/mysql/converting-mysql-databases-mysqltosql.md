---
title: Convertendo bancos de dados MySQL (MySQLToSQL) | Microsoft Docs
description: Saiba como converter objetos do banco de dados MySQL em objetos SQL Server ou do banco de dados SQL do Azure com o SSMA, depois de conectar e definir opções de mapeamento de projeto e de dados.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ac21850b-fb32-4704-9985-5759b7c688c7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c6f8e53a13d5950138f71ed9b4858419eb70f07f
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823281"
---
# <a name="converting-mysql-databases-mysqltosql"></a>Converter bancos de dados MySQL (MySQLToSQL)
Depois de ter se conectado ao MySQL, conectado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure e defina opções de mapeamento de projeto e de dados, você pode converter objetos de banco de dados MySQL em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure objetos de banco.  
  
## <a name="the-conversion-process"></a>O processo de conversão  
A conversão de objetos de banco de dados usa as definições de objeto do MySQL, converte-as em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos semelhantes ou SQL Azure e, em seguida, carrega essas informações nos metadados do SSMA. Ele não carrega as informações na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Em seguida, você pode exibir os objetos e suas propriedades usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure Gerenciador de metadados.  
  
Durante a conversão, o SSMA imprime as mensagens de saída no painel de saída e as mensagens de erro no painel de Lista de Erros. Use as informações de saída e erro para determinar se você precisa modificar seus bancos de dados MySQL ou seu processo de conversão para obter os resultados de conversão desejados.  
  
## <a name="setting-conversion-options"></a>Configurando opções de conversão  
Antes de converter objetos, examine as opções de conversão do projeto na caixa de diálogo **configurações do projeto** . Usando essa caixa de diálogo, você pode definir como o SSMA converte tabelas e índices. Para obter mais informações, consulte [configurações do projeto &#40;conversão&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
## <a name="conversion-results"></a>Resultados da conversão  
A tabela a seguir mostra quais objetos MySQL são convertidos e os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos resultantes:  
  
|Objetos MySQL|Objetos SQL Server resultantes|  
|-|-|  
|Tabelas com objetos dependentes, como índices|O SSMA cria tabelas com objetos dependentes. A tabela é convertida com todos os índices e restrições. Os índices são convertidos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos separados.<br /><br />O **mapeamento de tipo de dados espaciais** só pode ser executado no nível de nó de tabela.<br /><br />Para obter mais informações sobre as configurações de conversão de tabela, consulte [configurações de conversão](conversion-settings-mysqltosql.md)|  
|Funções|Se a função puder ser convertida diretamente em Transact-SQL, o SSMA criará uma função. Em alguns casos, a função deve ser convertida em um procedimento armazenado. Isso pode ser feito usando a **conversão de função** nas configurações do projeto. Nesse caso, o SSMA cria um procedimento armazenado e uma função que chama o procedimento armazenado.<br /><br />**Opções fornecidas:**<br /><br />Converter de acordo com as configurações do projeto<br /><br />Converter em função<br /><br />Converter em procedimento armazenado<br /><br />Para obter mais informações sobre configurações de conversão de função, consulte [configurações de conversão](conversion-settings-mysqltosql.md)|  
|Procedimentos|Se o procedimento puder ser convertido diretamente em Transact-SQL, o SSMA criará um procedimento armazenado. Em alguns casos, um procedimento armazenado deve ser chamado em uma transação autônoma. Nesse caso, o SSMA cria dois procedimentos armazenados: um que implementa o procedimento e outro usado para chamar o procedimento armazenado de implementação.|  
|Conversão de banco de dados|Os bancos de dados como objetos MySQL não são convertidos diretamente pelo SSMA para MySQL. Os bancos de dados MySQL são tratados mais como um nome de esquema e todos os parâmetros físicos são perdidos durante a conversão. O SSMA para MySQL usa o mapeamento de bancos de dados [MySQL para SQL Server esquemas &#40;&#41;MySQLToSQL](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md) para mapear objetos do banco de dados MySQL para o par apropriado de banco de dados/esquema SQL Server.|  
|Conversão de gatilho|**O SSMA cria gatilhos com base nas seguintes regras:**<br /><br />Os gatilhos BEFORE são convertidos em em vez de gatilhos T-SQL<br /><br />Os gatilhos AFTER são convertidos em após os gatilhos T-SQL com ou sem iterações por linha.|  
|Exibir conversão|O SSMA cria exibições com objetos dependentes|  
|Conversão de instrução|-Cada objeto de instrução SQL pode conter uma única instrução MySQL (como DDL, DML e outros tipos de instruções) ou iniciar... Bloco END.<br />-   **Conversão de várias instruções: início... **A instrução SQL de conversão end Block também pode conter um Begin... FINALIZAr bloco como um em definição de procedimento, função ou gatilho. Esses blocos devem ser convertidos da mesma maneira que estão sendo convertidos para os objetos de instrução do MySQL únicos.|  
  
## <a name="converting-mysql-database-objects"></a>Convertendo objetos de banco de dados MySQL  
Para converter objetos do banco de dados MySQL, primeiro selecione os objetos que deseja converter e, em seguida, faça com que o SSMA execute a conversão. Para exibir mensagens de saída durante a conversão, no menu **Exibir** , selecione **saída**.  
  
**Para converter objetos MySQL em sintaxe SQL Server ou SQL Azure**  
  
1.  No Gerenciador de metadados do MySQL, expanda o servidor MySQL e, em seguida, expanda **bancos de dados**.  
  
2.  Selecione os objetos a serem convertidos:  
  
    -   Para converter todos os esquemas, marque a caixa de seleção ao lado de **bancos de dados**.  
  
    -   Para converter ou omitir um banco de dados, marque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para converter ou omitir uma categoria de objetos, expanda um esquema e marque ou desmarque a caixa de seleção ao lado da categoria.  
  
    -   Para converter ou omitir objetos individuais, expanda a pasta categoria e marque ou desmarque a caixa de seleção ao lado do objeto.  
  
3.  Para converter todos os objetos selecionados, clique com o botão direito do mouse em **bancos de dados** e selecione **converter esquema**.  
  
    Você também pode converter objetos individuais ou categorias de objetos clicando com o botão direito do mouse no objeto ou em sua pasta pai e, em seguida, selecionando **converter esquema**.  
  
## <a name="viewing-conversion-problems"></a>Exibindo problemas de conversão  
Alguns objetos MySQL podem não ser convertidos. Você pode determinar as taxas de êxito da conversão exibindo o relatório de conversão de resumo.  
  
**Para exibir um relatório de resumo**  
  
1.  No Gerenciador de metadados do MySQL, selecione **bancos de dados**.  
  
2.  No painel direito, selecione a guia **relatório** .  
  
    Este relatório mostra o relatório de avaliação de resumo para todos os objetos de banco de dados que foram avaliados ou convertidos. Você também pode exibir um relatório de resumo para objetos individuais:  
  
    -   Para exibir o relatório de um esquema individual, selecione o banco de dados no Gerenciador de metadados do MySQL.  
  
    -   Para exibir o relatório de um objeto individual, selecione o objeto no Gerenciador de metadados do MySQL. Objetos que têm problemas de conversão têm um ícone de erro vermelho.  
  
Para objetos que falharam na conversão, você pode exibir a sintaxe que resultou na falha de conversão.  
  
**Para exibir problemas de conversão individuais**  
  
1.  No Gerenciador de metadados do MySQL, expanda **bancos de dados**.  
  
2.  Expanda o banco de dados que mostra um ícone de erro vermelho.  
  
3.  No banco de dados, expanda uma pasta que tem um ícone de erro vermelho.  
  
4.  Selecione o objeto que tem um ícone de erro vermelho.  
  
5.  No painel direito, clique na guia **relatório** .  
  
6.  Na parte superior da guia **relatório** está uma lista suspensa. Se a lista Mostrar **estatísticas**, altere a seleção para **origem**.  
  
    O SSMA exibirá o código-fonte e vários botões imediatamente acima do código.  
  
7.  Clique no botão **próximo problema** . Este é um ícone de erro vermelho com uma seta que aponta para a direita.  
  
    O SSMA irá destacar o primeiro código-fonte problemático encontrado no objeto atual.  
  
Para cada item que não pôde ser convertido, você precisa determinar o que deseja fazer com esse objeto:  
  
-   Você pode modificar o objeto no banco de dados MySQL para remover ou revisar o código problemático. Para carregar o código atualizado no SSMA, você precisará atualizar os metadados. Para obter mais informações, consulte [conectando-se ao MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   Você pode excluir o objeto da migração. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure Gerenciador de metadados e Gerenciador de metadados MySQL, desmarque a caixa de seleção ao lado do item antes de carregar os objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure e migrar dados do MySQL.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração é [carregar objetos de banco de dados convertidos em SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/loading-converted-database-objects-into-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados MySQL para SQL Server-banco de MySQLToSql SQL do Azure &#40;&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
